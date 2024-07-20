# 【读标准03】IEEE1451.5标准协议尝鲜实现


# 读标准03-IEEE1451.5标准协议尝鲜实现

[前面两个文章](https://staok.github.io/categories/%E8%AF%BB%E6%A0%87%E5%87%86/)里面已经详细描述了 TEDS 和 Message 的组成，这里 C 的实现分两个部分：分别对 TEDS 和 Message 的 数据结构实现 与 帧打包与解析的算法实现（第一版 2021.7）。从这个应用层协议标准原文来看，1451 协议内容相当繁杂（有关这种优缺点的论述在前两篇文章里面列举过）但是结构清晰，其类似表格化的结构可以比较顺畅的建模成编程语言的基本数据结构，并且一个编程基本哲学是设计优良的数据结构会使算法设计事半功倍。

本文描述成文时（2022.11）的程序状态、数据建模方式 和 API 设计，日后有更新只以 开源仓库内的 源码 和 其内的注释 为准，这里文章或许不跟进，只是一个程序初始版本的引导介绍。

------

## 放在前面的说明

本实现开源在 如下 Github 和 Gitee 仓库，以及对应的 系列介绍文章：

- [Staok/IEEE-1451-study: IEEE 1451 智能传感器接口标准，读原文、相关论文，学习记录，源码实现。 (github.com)](https://github.com/Staok/IEEE-1451-study)。

- [IEEE-1451-study: IEEE 1451 智能传感器接口标准，读原文、相关论文，学习记录，源码实现。 (gitee.com)](https://gitee.com/staok/IEEE-1451-study)。

  

- [小站——读标准 - 分类](https://staok.github.io/categories/读标准/)。

- [CSDN——【读IEEE 1451标准】系列](https://blog.csdn.net/staokgo/category_11531131.html)。

- [知乎——读 IEEE 1451标准 ](https://www.zhihu.com/column/c_1399448816085524480)。



内容说明：

IEEE 1451 标准特别繁琐，以下列举没有在本程序中 实现的部分（主要部分，不是全部）：
- TransducerChannel TEDS 的一些 标准源文要求 “必要” 有 的 域类没有加入到结构体中。

- 没有细致读标准源文，所以不清楚如果一个 TIM 下面挂接 多个 传感器通道，同时其种类有很多种，这种情形下该如何用 TEDS 描述（一定又相当繁琐）。

- 在下面 Message API 定义 里面可以看到只实现了 6 个左右的信息命令及其回复信息。

- 标准源文描述的功能非常全面了，但实现起来又只是纯体力活，所以 这里只实现最最最基本的功能。

     TEDS 和 Message 的 基本数据结构 在 .h 文件里面。

- 程序实现的比较早，现在看起来确实需要应先好好规划规划，一些有待改进的地方记录在 .c 文件最上面的注释里面。

## TEDS 实现

### 整体设计简述

参考 [【读标准01】IEEE1451 智能传感器接口标准介绍 - 欢迎来到 Staok - 瞰百易 (github.io)](https://staok.github.io/读标准01-ieee1451-智能传感器接口标准介绍/#teds-的格式)。

要实现四种必要的 TEDS：Meta-TEDS、TransducerChannel TEDS、User’s transducer name TEDS 和 PHY TEDS。

它们的结构均是 `4byte 的 Length` + `一个一个 TLV 域类` + `2byte 的 checksum`，其中 一个一个 域类 细看标准原文去 用结构体 打包实现，四个 TEDS 就 四个 结构体即可 完成 数据的建模。

然后用一个结构体打包以上整体，再和一个 uint8_t 数组 一同放到一个 union 联合体 里面，就可以通过 访问那个 数组 来 逐字节的 访问和处理 TEDS，发送的时候，先装填好 TEDS 结构体，然后按字节 发送那个数组 即可，接收同样，接收到一个 TEDS 二进制的大数组，直接放到 联合体 里面的 的数组的位置，那么 TEDS 二进制数据流就直接填充到 TEDS 结构体里面了。

优点就是：1、减少拷贝 或者叫 0 拷贝，提升打包发送和接收解析的效率；2、结构体易于扩展。

如果这里讲的抽象，那么下面直接看程序。 以下只以 Meta-TEDS 的构建为例，都摘自 .h 文件，其余部分思路相通，详见源程序便好。

### TEDS 头

即 TEDS identification header，详见 [01-“TEDS 头” 一节](https://staok.github.io/%E8%AF%BB%E6%A0%87%E5%87%8601-ieee1451-%E6%99%BA%E8%83%BD%E4%BC%A0%E6%84%9F%E5%99%A8%E6%8E%A5%E5%8F%A3%E6%A0%87%E5%87%86%E4%BB%8B%E7%BB%8D/#teds-%E5%A4%B4)。

```c
/*************************** TEDS 头 通用结构体 ***************************/
struct TEDS_ID_struct
{
	uint8_t Type;    		/* TEDS 头的域类号为 3 */
	uint8_t Length;  		/* 总为 4 */
	uint8_t Family;  		/* IEEE 1451.x */
	uint8_t access_code; 	/* TEDS 的代码 */
	uint8_t Version;		/* TEDS 版本，1 为初始版本，往后排 */
	uint8_t Tuple_Length;	/* TLV 中 Length 占的字节数，为 1*/
};
```

### TEDS 域类

```c
/* Meta TEDS 数据区 每一个域类一个结构体 */
struct M_TEDS_UUID_TLV_struct
{
    uint8_t Type;
    uint8_t Length;
    uint8_t Value[10];
};

struct M_TEDS_OholdOff_TLV_struct
{
    uint8_t Type;
    uint8_t Length;
    uint32_t Value;
};

struct M_TEDS_SHoldOff_TLV_struct
{
    uint8_t Type;
    uint8_t Length;
    uint32_t Value;
};

/* 等等等等，按照 标准原文 一个一个实现...特别多 */
```

### TEDS 结构体

```c
/* Meta TEDS 结构构建 */
struct Meta_TEDS_struct
{
	uint32_t Length;			/* 包括 DATA BLOCK 和 CHECKSUM 的 长度 */
	
	struct TEDS_ID_struct ID;	/* TEDS 头，Value 占 4 个字节 */
	
	struct M_TEDS_UUID_TLV_struct UUID;		    /* Globally Unique Identifier，Value 占 10 个字节 */
	struct M_TEDS_OholdOff_TLV_struct OholdOff; /* Operational time-out，整数，单位秒，Value 占 4 个字节 */
	struct M_TEDS_SHoldOff_TLV_struct SHoldOff; /* Slow-access time-out，整数，单位秒，Value 占 4 个字节 */
	struct M_TEDS_TestTime_TLV_struct TestTime;	/* Self-Test Time，整数，单位秒，Value 占 4 个字节 */
	struct M_TEDS_MaxChan_TLV_struct MaxChan;	/* Number of implemented TransducerChannels，整数，Value 占 2 个字节 */
	
	/* Group 相关内容过于复杂，略过 */

	uint16_t Checksum;			/* TEDS 校验，从 TED Length（最开头） 
					到 DATA BLOCK 的最后一个字节（本域类的上一个字节） 的加和，再用 0xFFFF 减去该加和值。 */
};
```

### TEDS 总结构

```c
/*************************** TEDS 联合体定义 ***************************/
    /* 为了可以逐字节的处理 TEDS 结构体 */

union Meta_TEDS_union
{
    struct Meta_TEDS_struct M_TEDS;
    uint8_t TEDS_load[MAX_TEDS_LOAD_SIZE];
};
```

注意，因为 `struct Meta_TEDS_struct M_TEDS;` 是与 数组 `uint8_t TEDS_load[MAX_TEDS_LOAD_SIZE];` 一同放到一个 联合体里面的，因此 前者 那个 TEDS 结构体 必须要 以 1 字节对齐，才能让 后者 数组 准确的 逐字节的 访问和处理 TEDS 结构体。源程序中使用 GNU Gcc 扩展关键字 pack 实现，具体如下。

```
#pragma pack(1) /* 让编译器做 1 字节对齐 */
... 各种结构体 ...
#pragma pack() /* 取消 1 字节对齐，恢复为默认对齐 */
```



然后就是将 四个 TEDS 联合体 与 其它信息 都放到一个大结构体里面，我喜欢做一个总的打包，结构清晰，层次分明，调试易查。

```c
/*************************** TEDS 总结构体，用户使用 ***************************/
struct TEDS_struct
{
        /* 下面 TEDS 联合、属性 结构体 和 状体 结构体 都是 指针，用于承接 .c 文件里面 例化的 实体结构体 的 地址  */
    union Meta_TEDS_union *                  M_TEDS_u;   uint32_t M_TEDS_load_Length;
    union TransducerChannel_TEDS_union *     TC_TEDS_u;  uint32_t TC_TEDS_load_Length;
    union User_Transducer_Name_TEDS_union *  UTN_TEDS_u; uint32_t UTN_TEDS_load_Length;
    union PHY_TEDS_union *                   PHY_TEDS_u; uint32_t PHY_TEDS_load_Length;

    struct TEDS_attributes_struct * M_TEDS_attr;
    struct TEDS_attributes_struct * TC_TEDS_attr;
    struct TEDS_attributes_struct * UTN_TEDS_attr;
    struct TEDS_attributes_struct * PHY_TEDS_attr;

    struct TEDS_status_struct * M_TEDS_status;
    struct TEDS_status_struct * TC_TEDS_status;
    struct TEDS_status_struct * UTN_TEDS_status;
    struct TEDS_status_struct * PHY_TEDS_status;

	/* TEDS 的名称字符串 */
    uint8_t* M_TEDS_str;
    uint8_t* TC_TEDS_str;
    uint8_t* UTN_TEDS_str;
    uint8_t* PHY_TEDS_str;
};

extern struct TEDS_struct   TEDS;
```

### TEDS 属性和状态 结构体

参考详见 [01-“TEDS 属性” 一节](https://staok.github.io/读标准01-ieee1451-智能传感器接口标准介绍/#teds-属性)。

```c
/*************************** TEDS 属性 结构体 定义 ***************************/
struct TEDS_attributes_struct
{
    uint8_t ReadOnly    :1;     /* Read-only—Set to true if TEDS may be read but not written. */
    
    uint8_t NotAvail    :1;     /* Unsupported—Set to true if TEDS is not supported by this TransducerChannel.  */
    
    uint8_t Invalid     :1;     /* Invalid—Set to true if the current TEDS image is invalid.  */
   
    uint8_t  Virtual     :1;    /* Virtual TEDS—This bit is set to true if this is a virtual 
                                TEDS. (A virtual TEDS is any TEDS that is not stored in 
                                the TIM. The responsibility for accessing a virtual TEDS 
                                is vested in the NCAP or host processor.)  */
   
    uint8_t TextTEDS    :1;     /* Text TEDS—Set to true if the TEDS is text based.  */
   
    uint8_t Adaptive    :1;     /* Adaptive—Set to true if the contents of the TEDS can be 
                                changed by the TIM or TransducerChannel without the 
                                NCAP issuing a WriteTEDS segment command.  */
   
    uint8_t MfgrDefine  :1;     /* MfgrDefine—Set to True if the contents of this TEDS are 
                                defined by the manufacturer and will only conform to the 
                                structures defined in the standard if the TextTEDS 
                                attribute is also set.   */
   
    uint8_t Reserved    :1;     /* Reserved */
};

/*************************** TEDS 状态 结构体定义 ***************************/
struct TEDS_status_struct
{
    uint8_t TooLarge        :1; /* Too Large—The last TEDS image received 
    				was too large to fit in the memory allocated to this TEDS.  */
    
    uint8_t Reserved_1      :1; /* 为 IEEE 1451 标准做保留 */
    uint8_t Reserved_2      :1;
    uint8_t Reserved_3      :1;

    uint8_t Open_4          :1; /* Open to manufacturers */
    uint8_t Open_5          :1;
    uint8_t Open_6          :1;
    uint8_t Open_7          :1;
};
```

### TEDS 各个结构实例化

在 .c 文件里面，分别 实例化 四个 TEDS 的 联合体、属性结构体 和 状态结构体（这里只放 Meta_TEDS 的）。

```c
struct TEDS_struct TEDS;

struct TEDS_attributes_struct M_TEDS_attr = 
{
    .ReadOnly = 0,
    .NotAvail = 0,
    .Invalid = 0,
    .Virtual = 0,
    .TextTEDS = 0,
    .Adaptive = 0,
    .MfgrDefine = 0,
    .Reserved = 1
};

struct TEDS_status_struct M_TEDS_status = 
{
    .TooLarge = 0,
    .Reserved_1 = 1,
    .Reserved_2 = 0,
    .Reserved_3 = 1,

    .Open_4 = 1,
    .Open_5 = 1,
    .Open_6 = 0,
    .Open_7 = 1,
};

/* 开始装填 M_TEDS 结构体 */
union Meta_TEDS_union M_TEDS_u = 
{
    /* Length 和 Checksum 会在 TEDS_init() 中自动计算装填 */

    .M_TEDS.ID.Type         = 3,    /* TEDS 头的域类号为 3 */
    .M_TEDS.ID.Length       = 4,    /* 总为 4 */
    .M_TEDS.ID.Family       = 5,    /* IEEE 1451.x */
    .M_TEDS.ID.access_code  = M_TEDS_ACCESS_CODE,   /* TEDS 的代码 */
    .M_TEDS.ID.Version      = 1,    /* TEDS 版本，1 为初始版本，往后排 */
    .M_TEDS.ID.Tuple_Length = 1,    /* TLV 中 Length 占的字节数，为 1*/

    /* Globally Unique Identifier，Value 占 10 个字节 */
    .M_TEDS.UUID.Type = 4,
    .M_TEDS.UUID.Length = 10,
    .M_TEDS.UUID.Value = {0x8d,0x4d,0x9d,0xa6,0x52,0x81,0xf7,0x00,0x00,0x00},
    
    /* Operational time-out，整数，单位秒，Value 占 4 个字节 */
    .M_TEDS.OholdOff.Type = 10,
    .M_TEDS.OholdOff.Length = 4,
    .M_TEDS.OholdOff.Value = 5,
    
    /* Slow-access time-out，整数，单位秒，Value 占 4 个字节 */
    .M_TEDS.SHoldOff.Type = 11,
    .M_TEDS.SHoldOff.Length = 4,
    .M_TEDS.SHoldOff.Value = 10,

    /* ...... */
};


```

### TEDS API

给出若干 API。

```c
void TEDS_init(void);
void TEDS_pack_up(uint8_t* dest_loader,uint32_t* length,uint8_t access_code);
void TEDS_decode(uint8_t* TEDS_load);   /* TODO ，暂不实现 */
```

```c
void TEDS_init(void)
{
    
    M_TEDS_u.M_TEDS.Length = sizeof(struct Meta_TEDS_struct) - 4;       /* 计算 TEDS 的数据区长度 */ /* 42，宇宙的终极答案，yyds */
                        /* 这个长度 只包括 TEDS 的 DATA BLOCK 和 CHECKSUM，不包括 占 4 byte 的 length */
    TEDS.M_TEDS_load_Length = M_TEDS_u.M_TEDS.Length + 4;               /* 计算 TEDS 总长度 */
    TEDS.M_TEDS_u = &M_TEDS_u;                                          /* TEDS 的 M_TEDS_u 指针填充，后面 TEDS_calc_Checksum() 要用 */
    M_TEDS_u.M_TEDS.Checksum = TEDS_calc_Checksum(M_TEDS_ACCESS_CODE);  /* 计算 Checksum  */

    /* ... 这里 略 其它 TEDS 结构体装填 代码 */

    /* 开始装填 每个 TEDS 的全名字符串 */
    TEDS.M_TEDS_str     = "Meta-TEDS";
    TEDS.TC_TEDS_str    = "TransducerChannel TEDS";
    TEDS.UTN_TEDS_str   = "User’s transducer name TEDS";
    TEDS.PHY_TEDS_str   = "PHY TEDS";

    /* 指定对应 TEDS 的 属性和状态 */
    TEDS.M_TEDS_attr = &M_TEDS_attr;
    ...

    TEDS.M_TEDS_status = &M_TEDS_status;
    ...
}
```

```c
/* TEDS 打包函数
    第一个参数给一个存放 TEDS 字节数据的空间，至少 200 个字节空间；
    第二个参数指定 有效数据长度（字节数）；
    第三个参数选择哪一个 TEDS。
*/
void TEDS_pack_up(uint8_t* dest_loader,uint32_t* length,uint8_t access_code)
{
    uint8_t* load_ptr;
    uint32_t whole_length = 0;
    
    switch (access_code)
    {
        case M_TEDS_ACCESS_CODE:
            
            whole_length = TEDS.M_TEDS_load_Length;
            
            load_ptr = TEDS.M_TEDS_u->TEDS_load;
            
            break;

        case TC_TEDS_ACCESS_CODE:
            
            whole_length = TEDS.TC_TEDS_load_Length;
            
            load_ptr = TEDS.TC_TEDS_u->TEDS_load;

            break;

        case UTN_TEDS_ACCESS_CODE:
            
            whole_length = TEDS.UTN_TEDS_load_Length;
            
            load_ptr = TEDS.UTN_TEDS_u->TEDS_load;

            break;

        case PHY_TEDS_ACCESS_CODE:
            
            whole_length = TEDS.PHY_TEDS_load_Length;
            
            load_ptr = TEDS.PHY_TEDS_u->TEDS_load;
            
            break;
        
        default:
            break;
    }

    *length = whole_length;
    memcpy(dest_loader, load_ptr, whole_length);
    
}
```



## Message 实现

参考详见 [01-“消息 的格式” 一节](https://staok.github.io/读标准01-ieee1451-智能传感器接口标准介绍/#消息-的格式)。

### 各个命令类的枚举实现

```c
/* 命令类 枚举（Command Class） */
enum Command_class_enum
{
    Reserved_Command_class = 0,
    CommonCmd,      /* 给 TIM 的通用命令（Commands common to the TIM and TransducerChannel）  */
    
    XdcrIdle,       /* 传感器 空闲状态命令（XdcrIdle，Transducer idle state commands）  */
    XdcrOperate,    /* 传感器 工作状态命令（XdcrOperate，Transducer operating state commands） */
    XdcrEither,     /* 传感器 空闲状态或工作状态命令（XdcrEither，Transducer either idle or operating state commands） */
    
    TIMsleep,       /* TIM 睡眠状态命令（TIM sleep state commands） */
    TIMActive,      /* TIM 激活状态命令（TIM active state commands） */
    AnyState,       /* TIM 任何状态命令（TIM any state commands） */
    
    ReservedClass = 8,    /* 编号 8—127 做为 1451 标准的保留 */
    ClassN = 128,         /* 编号 128—255 为用户保留，用户可以自定 */
};

/* 给 TIM 的通用命令枚举 CommonCmd（Commands common to the TIM and TransducerChannel）  */
    /* 即 Command Class 为 CommonCmd 时，Command function 具体的值 如下 */
enum CommonCmd_commands_enum
{
    Reserved_Common_command = 0,
    
    Query_TEDS,                     /* Query TEDS command（询问 TEDS 信息命令） */
    Read_TEDS_segment,
    Write_TEDS_segment,
    Update_TEDS,
    
    Run_self_test,
    
    Write_service_request_mask,
    Read_service_request_mask,
    
    Read_StatusEvent_register,
    Read_StatusCondition_register,
    Clear_StatusEvent_register, 
    Write_StatusEvent_protocol_state, 
    Read_StatusEvent_protocol_state,

    ReservedCommands = 13,       /* 编号 13–127 做为 1451 标准的保留  */
    Open_Common_commands_for_manufacturers = 128, /* 编号 128—255 为用户保留，用户可以自定 */

    /* 这里自定 TIM 初始化完毕标志 */
    TIM_ALL_TC_initiated = 130,
};

/* 传感器 空闲状态命令枚举（XdcrIdle，Transducer idle state commands）  */
    /* 即 Command Class 为 XdcrIdle 时，Command function 具体的值 如下，以此类推 */
enum XdcrIdle_commands_enum
{
    Reserved_XdcrIdle_command = 0,
    Set_TransducerChannel_data_repetition_count, 
    Set_TransducerChannel_pre_trigger_count,
    AddressGroup_definition,
    Sampling_mode,
    Data_Transmission_mode,
    Buffered_state,
    ... 等等等等 太多了...
```

### Message 结构体

```c
#pragma pack(1) /* 让编译器做 1 字节对齐 */

/* 消息/命令 帧 结构体，也用于 TIM 发送初始化完毕的消息 */
struct Message_struct
{
    uint8_t Dest_TIM_and_TC_Num[2]; /* This field gives the 16 bit TransducerChannel number for the destination of the message.  */
    
    uint8_t Command_class;
    uint8_t Command_function;
    
    uint16_t dependent_Length; /* Length is the number of command-dependent octets in this message.  */
    uint8_t dependent_load[MAX_Message_dependent_SIZE]; /* 用于暂存 command_dependent，有效长度为 dependent_Length */
};

/* 回复/响应 帧 结构体，还用于 TIM 发传感器数据 */
struct ReplyMessage_struct
{
    uint8_t Flag; /* If this octet is nonzero, it indicates that the command was successfully completed. If it is zero, the 
                    command failed and the system should check the status to determine why. */
    uint16_t dependent_Length; /* Length is the number of reply-dependent octets in this message.  */
    /* Peply_Message_struct 中的附带参数长度 dependent_Length 占俩字节，最大 65535，即一帧回复帧中 Reply dependent 的最大字节数 */
    uint8_t dependent_load[MAX_Message_dependent_SIZE]; /* 用于暂存 Reply dependent，有效长度为 dependent_Length */
    /* 这里我自己再定义，dependent 的尾部再添加两个字节，表回复对应命令的 class 和 command */
};

#pragma pack() /* 取消 1 字节对齐，恢复为默认对齐 */
```

### Message 总结构

与 TEDS 总结构 定义相似的，先与一个 以字节为单位的大数组 一同放到一个 联合体中，再来个 总体打包。

```c
/*************************** Message 和 ReplyMessage 联合体定义 ***************************/
    /* 这么做 让 Message 和 ReplyMessage 结构体可以 逐字节 处理 */

union Message_union
{
    struct Message_struct Message;
    uint8_t Message_load[MAX_Message_dependent_SIZE + 10]; 
        /* 数组空间 里面 +10 是因为 Message 结构体里面 除了 dependent 的 MAX_Message_dependent_SIZE 还有 前面几个 不超过 10 byte 的变量  */
};

union ReplyMessage_union
{
    struct ReplyMessage_struct ReplyMessage;
    uint8_t ReplyMessage_load[MAX_Message_dependent_SIZE + 10];
};
```

```c
/*************************** Message 和 ReplyMessage 总结构体，供用户用 ***************************/
struct MES_struct
{
    /* 联合指针形式，在 Message_init() 中 将 .c 中的 联合体 实体的地址赋给这里 */
    union Message_union*        Message_u;      uint32_t Message_load_Length;
    union ReplyMessage_union*   ReplyMessage_u; uint32_t ReplyMessage_load_Length;
};

extern struct MES_struct MES;
```

### Message API

给出若干 API。

```c
/* API 具体注释看 .c 文件 函数定义处，具体使用实例看 .c 最上面 注释 */

/**************************** Message init，用户使用 ****************************/
void Message_init(void);

/**************************** 根据不同命令 填充 Message 结构体 并打包数据的 API，用户使用 ****************************/
/* 打包好的消息数据在 MES.Message_u->Message_load 里面，有效数据长度为 MES.Message_load_Length */
void Message_CommonCmd_Query_TEDS_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC, uint8_t which_TEDS);
void Message_CommonCmd_Read_TEDS_segment_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC, uint8_t which_TEDS, uint32_t TEDSOffset);
void Message_XdcrIdle_Set_Data_Transmission_mode_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC,enum Data_Transmission_mode_enum mode);
void Message_XdcrOperate_Read_TC_data_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC, uint32_t Offset);
void Message_XdcrOperate_Trigger_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC);
void Message_XdcrOperate_Abort_Trigger_pack_up(uint8_t Dest_TIM, uint8_t Dest_TC);
void Message_TIM_initiated_pack_up(void);

/**************************** 消息的 发送，用户使用 ****************************/
void Message_pack_up_And_send(void);

/**************************** 解析接收到的 Message 的 API ****************************/
// void Message_decode(struct Message_struct* messageReceived,uint8_t* mes_load);

/**************************** 根据相应 Message 填充 ReplyMessage 结构体 并打包数据的 API， 的 API ****************************/
/* 打包好后的回复消息数据在 MES.ReplyMessage_u->ReplyMessage_load 里面，有效数据长度为 MES.ReplyMessage_load_Length */
// void ReplyMessage_CommonCmd_Query_TEDS_pack_up(uint8_t which_TEDS);
// void ReplyMessage_CommonCmd_Read_TEDS_segment_pack_up(uint8_t which_TEDS, uint32_t TEDSOffset);
// void ReplyMessage_XdcrIdle_Data_Transmission_mode_pack_up(void);
// void ReplyMessage_XdcrOperate_Read_TC_data_pack_up(void);
// void ReplyMessage_XdcrOperate_Trigger_pack_up(void);
// void ReplyMessage_XdcrOperate_Abort_Trigger_pack_up(void);
// void ReplyMessage_TIM_initiated_pack_up(void);

/**************************** 回复消息的 发送 ****************************/
// uint8_t ReplyMessage_send(uint8_t class, uint8_t command);

/**************************** 解析接收到的 回复消息 的 API ****************************/
void ReplyMessage_decode(struct ReplyMessage_struct* replyMessageReceived,uint8_t* received_rep_mes_load);

/**************************** ReplyMessage 服务程序，自动解析 Message 并回复，用户使用  ****************************/
void ReplyMessage_Server(uint8_t* received_mes_load);
```

具体 `void Message_init(void);` 这个 的实现如下，在 .c 文件里面：

```c
struct MES_struct MES;

/* 给 Message_u 和 ReplyMessage_u 填充默认值  */
union Message_union Message_u = 
{
    .Message.Dest_TIM_and_TC_Num[TIM_enum] = TIM_3,
    .Message.Dest_TIM_and_TC_Num[TC_enum] = TC_12,

    .Message.Command_class = CommonCmd,
    .Message.Command_function = Query_TEDS,
    .Message.dependent_Length = 1,

    .Message.dependent_load[0] = PHY_TEDS_ACCESS_CODE,
};

union ReplyMessage_union ReplyMessage_u = 
{
    .ReplyMessage.Flag = 0,
    .ReplyMessage.dependent_Length = 1,
    .ReplyMessage.dependent_load[0] = 0xAA,
};

/**************************** Message init，用户使用 ****************************/
void Message_init(void)
{
    MES.Message_u = &Message_u;
    MES.ReplyMessage_u = &ReplyMessage_u;

    /* MES 的 Message_load_Length 和 ReplyMessage_load_Length 根据不同的情景在打包发送数据的时候再填 */
}
```



## 一个实例

```
流程：
    0、NCAP 发出 WiFi 热点， TIM 们上电开机后分别自动的连上 NCAP
    0.5、TIM 给 NCAP 发送初始化完毕消息（Message_TIM_initiated）
    1、NCAP 自动询问 TIM 的 TEDS（CommonCmd_Query_TEDS），TIM 自动做回应
    2、NCAP 再自动读 TIM 的 TEDS（CommonCmd_Read_TEDS），TIM 自动做回应
    3、以上步骤均无误后，NCAP 根据一个标志位判断自动启动 TIM 还是等待上级进一步操作
        3.1、若是前者，即自动启动 TIM
            3.1.1、NCAP 根据预先设定去设 TIM 的上传数据模式（XdcrIdle_Data_Transmission_mode），TIM 自动做回应
                我这里设计三种模式：
                    OnCommand_custom：（这个暂不实现）
                        NCAP 发送 读 数据 命令 给 TIM 的时候， TIM 空闲时候则响应，开始采集 1s 数据并上传；若TIM 正在工作则继续原来的采集和上传，不予回应
                    Interval_1s：TIM 定时 上传数据，在我这里是 每秒 发送一帧数据，但上位机显示的是连续的
                    BufferHalfFull：缓冲区半满时候 上传一次数据
            3.1.2、NCAP 发送 触发命令（XdcrOperate_Trigger），TIM 按照 Interval_1s 或 BufferHalfFull 模式 上传数据
            到此，以上所有步骤都是 TIM 上电后自动完成的
            3.1.3、NCAP 发送 终止触发命令（XdcrOperate_Abort_Trigger），TIM 停止上传，停止采集
        3.2、若是后者，即等待上级进一步操作，则 NCAP 受上级的具体控制（启、停、设置模式、待机等等）
```

```c
本库使用流程：（NCAP 和 TIM 同用此库，只调用不同 API 即可）
    
    上电 TEDS 初始化，调用如下：一般是 TIM 调用
        TEDS_init();
    
    上电 Message 初始化，调用如下：一般是 NCAP 调用
        Message_init();

    发送一次命令，这里一般是 NCAP 调用的 API：
        比如 NCAP 自动 发送 询问 TIM 的 TEDS 的命令（CommonCmd_Query_TEDS），则例子如下，其他命令同理
            Message_CommonCmd_Query_TEDS_pack_up(TIM_3, TC_12, PHY_TEDS_ACCESS_CODE);
            Message_pack_up_And_send();

        NCAP 解析回复消息 API：填入接收到的回复消息字符串，接收回复消息解析，并讲结果存在 replyMessageReceived 结构体地址里
            void ReplyMessage_decode(struct ReplyMessage_struct* replyMessageReceived,uint8_t* received_rep_mes_load)

    回复消息，这里一般是 TIM 调用的 API：
        TIM 首先主动发送初始化完毕消息：
            Message_TIM_initiated_pack_up();
            Message_pack_up_And_send();

        TIM 处理 接收消息 和 自动回复消息 API：填入接收到的消息字符串，会根据已经实现的消息解码字符串和自动回应
            void ReplyMessage_Server(uint8_t* received_mes_load)
```


