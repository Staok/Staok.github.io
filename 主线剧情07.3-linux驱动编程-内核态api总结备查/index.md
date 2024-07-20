# 【主线剧情07.3】Linux驱动编程-内核态API总结备查


# 驱动程序 中的 设备相关 和 常用内核态 API 总结备查

多处网搜和引用，做了良好的整理，侵删。

本文对应的驱动源代码在 github/gitee 仓库里：并且 [在 Github 上的原版文章日后可能会更新](https://github.com/Staok/ARM-Linux-Study)，但这里不会跟进。[文章的 Gitee 仓库地址，Gitee 访问更流畅](https://gitee.com/staok/ARM-Linux-Study)。

## 驱动模块编译和插入与系统版本一致性的重要说明

编译驱动程序：

首先编译一次内核（只一次），再编译驱动程序，因为编译后者需要用到前者编译后产生的一些文件，二者要使用同一套编译器工具链。

即使是不同的编译器，编译后的固件、模块的编排格式都有差异！

插入驱动模块：

编译驱动时用到的内核和编译器，与要插入的系统的内核的编译器尽量一致，即 内核版本号一致 和 编译器工具链一致，最好 内核源码、编译器 这些 始终 都是同一套东西！

如果 SoC 板子上 运行的 内核 和 编译驱动时候用到的内核源码的版本不一致，应尽量一致，这种情况也可以插入模块，但是会提示可能会有不兼容的不可预知状况！

如果 SoC 板子上 运行的 内核 和 编译驱动时候用到的内核源码的版本一致，**但是编译器不同！这种情况模块是不能插入的**，因为不同编译器的编排固件的格式会有差别，这时应该重新编译内核源码，把得到的 内核固件 zImage 、设备树 和 所有模块 都替换 SoC 板子上的。，就可以解决问题。

## 驱动程序和应用程序开源协议说明

驱动必须得采用和 Linux 内核一样的协议 GPL，

因此驱动程序必须随 Linux 源码一样开源，

好多商家为规避开源自己的核心代码，就将核心代码写在应用程序里面，应用程序不用开源，

由而 应用程序写很复杂 而 驱动写的较简单，由此避开自己的核心代码 带上 GPL 协议。

------

## 内核 API 查询

- [Linux内核API|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api) 极其好！！！
- .etc（用到时候慢慢补充）

## 驱动程序内的

### 主次设备号相关

在内核中，用dev_t类型(其实就是一个32位的无符号整数)的变量来保存设备的**主次设备号**，其中高12位表示**主设备号**，低20位表示**次设备号**。

设备获得主次设备号有两种方式：一种是手动给定一个32位数，并将它与设备联系起来(即用某个函数注册)；另一种是调用系统函数给设备动态分配一个主次设备号。

与主次设备号相关的3个宏：

```c
#define MAJOR(dev)    ((dev)>>8)
#define MINOR(dev)    ((dev) & 0xff)
#define MKDEV(ma,mi)  ((ma)<<8 | (mi))
```

- MAJOR(dev_t dev)：根据设备号 dev 获得主设备号。
- MINOR(dev_t dev)：根据设备号 dev 获得次设备号。
- MKDEV(int major, int minor)：根据主设备号 major 和次设备号 minor 构建 dev_t 类型设备号。

### register_chrdev / unregister_chrdev

[Linux内核API register_chrdev|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-register_chrdev.html)。

```c
int register_chrdev(unsigned int major, const char*name, struct file_operations *fops);
```

- 其中参数major如果等于0，则表示采用系统动态分配的主设备号；不为0，则表示静态注册，范围为 1~255。
-  name 是注册驱动的名子(出现在 `/proc/devices`)，fops 是 file_operations 结构。
-  函数register_chrdev()返回int型的结果，表示设备添加是否成功。如果成功返回0，如果失败返回-ENOMEM, ENOMEM的定义值为12。

[Linux内核API unregister_chrdev|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-unregister_chrdev.html)。

```c
static inline void unregister_chrdev(unsigned int major, const char *name);
```

- 第一个输入参数代表即将被删除的字符设备区及字符设备的主设备号，函数将根据此参数查找内核中的字符设备。
- 第二个输入参数代表设备名，但在函数的实现源码中没有用到，没有什么意义。

### 动态字符设备创建

参考 [字符设备驱动编写流程以及大概框架_辣眼睛的Developer的博客-CSDN博客](https://blog.csdn.net/softwoker/article/details/45113221)。

这里面讲另外两种创建字符设备方式：cdev 方式 和混杂方式。详情看上面这个链接。

register_chrdev_region：对于 手动/静态 给定一个主次设备号（不推荐），使用以下函数：`int register_chrdev_region(dev_t first, unsigned int count, char *name);`。其中first是我们手动给定的设备号，count是所请求的连续设备号的个数，而name是和该设备号范围关联的设备名称，它将出现在/proc/devices和sysfs中。比如，若first为0x3FFFF0，count为0x5，那么该函数就会为5个设备注册设备号，分别是0x3FFFF0、 0x3FFFF1、 0x3FFFF2、 0x3FFFF3、 0x3FFFF4。用这种方法注册设备号有一个缺点，那就是若该驱动module被其他人广泛使用，那么无法保证注册的设备号是其他人的Linux系统中未分配使用的设备号。

alloc_chrdev_region：对于动态分配设备号，使用以下函数：`int alloc_chrdev_region(dev_t *dev, unsigned int firstminor, unsigned int count, char *name);`。该函数需要传递给它指定的第一个次设备号firstminor(一般为0)和要分配的设备数count，以及设备名，调用该函数后自动分配得到的设备号保存在dev中。**次设备号可以指定，主设备号不能指定只能内核动态分配。**动态分配设备号可以避免手动指定设备号时带来的缺点，但是它却也有自己的缺点，那就是无法预知在/dev下创建设备节点是什么名字，因为动态分配设备号不能保证在每次加载驱动module时始终一致，这个缺点可以避免，因为在加载驱动module后，我们可以读取/proc/devices文件以获得Linux内核分配给该设备的主设备号。

```c
struct cdev {
	struct kobject kobj;
	struct module *owner;
	const struct file_operations *ops; // 文件操作函数
	struct list_head list;
	dev_t dev;   //设备号（包括主次设备号）
	unsigned int count;   //设备个数
};
```

100ask 的例子，01b_hello_drv 里面的：

```c
static struct cdev hello_cdev;
static struct file_operations hello_drv = {...};
...
rc = alloc_chrdev_region(&devid, 0, 1, "hello"); // 直接动态分配 dev_t 类型的设备号，其中包含了主、次涉设备号
cdev_init(&hello_cdev, &hello_drv); // cdev->ops = fops，将 &hello_drv 赋值给 &hello_cdev->ops
cdev_add(&hello_cdev, devid, 1); // 将设备号添加进cdev里的dev设备号成员，并向内核注册cdev

然后就是创建设备类 class_create 和创建设备 device_create
```

更简明的教程 [ 对 linux驱动 及 字符型设备驱动 的理解_艾特号的博客-CSDN博客](https://blog.csdn.net/lpwsw/article/details/122068121)。

更多例程：[字符设备驱动框架3：深入探讨—完整的驱动代码工程_欧阳海宾的博客-CSDN博客](https://blog.csdn.net/oyhb_1992/article/details/77596411)，看看理解就好，这个例子并不通用。

### class_create / class_destroy

[Linux内核API class_create|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-class_create.html)。[Linux内核API class_destroy|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-class_destroy.html)。

```c
class_create(owner, name);
```

> `class_create()`用于动态创建设备的逻辑类，并完成部分字段的初始化，然后将其添加进Linux内核系统中。此函数的执行效果就是在目录`/sys/class`下创建一个新的文件夹，此文件夹的名字为此函数的第二个输入参数 name。
>
> owner 一般赋值为 THIS_MODULE。

```c
void class_destroy(struct class *cls);
```

> 函数`class_destroy()`用于删除设备的逻辑类。不返回任何值。

### device_create / device_destroy

[Linux内核API device_create|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-device_create.html)。[Linux内核API device_destroy|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/device-driver-and-device-management/linux-kernel-api-device_destroy.html)。

```c
struct device *device_create(struct class *cls, struct device *parent, dev_t devt, void *drvdata, const char *fmt, ...);
```

> 函数`device_create()`用于动态地创建逻辑设备，并对新的逻辑设备类进行相应的初始化，将其与此函数的第一个参数所代表的逻辑类关联起来，然后将此逻辑设备加到Linux内核系统的设备驱动程序模型中。函数能够自动地在`/sys/devices/virtual`目录下创建新的逻辑设备目录，在`/dev`目录下创建与逻辑类对应的设备文件。
>
> 函数`device_create()`的第一个输入参数代表与即将创建的逻辑设备相关的逻辑类。即`class_create()`的返回值。
>
> 第二个输入参数代表即将创建的逻辑设备的父设备的指针，子设备与父设备的关系是：当父设备不可用时，子设备不可用，子设备依赖父设备，父设备不依赖子设备。不用时可填入 NULL。
>
> 第三个输入参数是逻辑设备的设备号。可填入 MKDEV(major, minor)。
>
> 第四个输入参数是void类型的指针，代表回调函数的输入参数。不用时可填入 NULL。
>
> 第五个输入参数是逻辑设备的设备名，即在目录`/sys/devices/virtual`创建的逻辑设备目录的目录名。可以用 printf 的格式写，比如 `"drv_%d",drv_num`。
>
> 函数`device_create()`的返回值是struct device结构体类型的指针，指向新创建的逻辑设备。

```c
void device_destroy(struct class *cls, dev_t devt);
```

> 函数**device_destroy()**：用于从Linux内核系统设备驱动程序模型中移除一个设备，并删除`/sys/devices/virtual`目录下对应的设备目录及/dev目录下对应的设备文件。
>
> 函数device_destroy()第一个输入参数是struct class类型的变量，代表与待注销的逻辑设备相关的逻辑类，用于Linux内核系统逻辑设备的查找。即`class_create()`的返回值。
>
> 第二个参数是逻辑设备的设备号，与第一个参数共同确定一个逻辑设备。可填入 MKDEV(major, minor)。

### module_init / module_exit

修饰本模块的 加载 和 卸载 时候 调用的函数。

### struct file_operations

参考：

- [file_operations结构体详细解释 - 百度文库 (baidu.com)](https://wenku.baidu.com/view/22f62ef62bea81c758f5f61fb7360b4c2e3f2ac7.html)。
- [linux内核中struct file_operations 结构体介绍_鱼思故渊的博客-CSDN博客_file_operations结构体](https://blog.csdn.net/yusiguyuan/article/details/11352155)。
- [struct file_operations_zlcchina的博客-CSDN博客](https://blog.csdn.net/zlcchina/article/details/12612207)。
- [Linux设备驱动的struct file_operations结构体中unlocked_ioctl和compat_ioctl的区别 - 简书 (jianshu.com)](https://www.jianshu.com/p/e785fa478ce7)。
- [Linux中的File_operations结构体-pudn.com](https://www.pudn.com/news/628f831fbf399b7f351e6d8a.html)。

```c
/* 在 include/linux/fs.h 文件中定义 */
struct file_operations {
    struct module *owner;
    loff_t (*llseek) (struct file *, loff_t, int);
    ssize_t (*read) (struct file *, char __user *, size_t, loff_t *);
    ssize_t (*write) (struct file *, const char __user *, size_t, loff_t *);
    ssize_t (*read_iter) (struct kiocb *, struct iov_iter *);
    ssize_t (*write_iter) (struct kiocb *, struct iov_iter *);
    int (*iterate) (struct file *, struct dir_context *);
    int (*iterate_shared) (struct file *, struct dir_context *);
    unsigned int (*poll) (struct file *, struct poll_table_struct *);
    long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
    long (*compat_ioctl) (struct file *, unsigned int, unsigned long);
    int (*mmap) (struct file *, struct vm_area_struct *);
    int (*open) (struct inode *, struct file *);
    int (*flush) (struct file *, fl_owner_t id);
    int (*release) (struct inode *, struct file *);
    int (*fsync) (struct file *, loff_t, loff_t, int datasync);
    int (*aio_fsync) (struct kiocb *, int datasync);
    int (*fasync) (int, struct file *, int);
    int (*lock) (struct file *, int, struct file_lock *);
    ssize_t (*sendpage) (struct file *, struct page *, int, size_t, loff_t *, int);
    unsigned long (*get_unmapped_area)(struct file *, unsigned long, unsigned long, unsigned long, unsigned long);
    int (*check_flags)(int);
    int (*flock) (struct file *, int, struct file_lock *);
    ssize_t (*splice_write)(struct pipe_inode_info *, struct file *, loff_t *, size_t, unsigned int);
    ssize_t (*splice_read)(struct file *, loff_t *, struct pipe_inode_info *, size_t, unsigned int);
    int (*setlease)(struct file *, long, struct file_lock **, void **);
    long (*fallocate)(struct file *file, int mode, loff_t offset, loff_t len);
    void (*show_fdinfo)(struct seq_file *m, struct file *f);
#ifndef CONFIG_MMU
    unsigned (*mmap_capabilities)(struct file *);
#endif
    ssize_t (*copy_file_range)(struct file *, loff_t, struct file *, loff_t, size_t, unsigned int);
    int (*clone_file_range)(struct file *, loff_t, struct file *, loff_t, u64);
    ssize_t (*dedupe_file_range)(struct file *, u64, u64, struct file *, u64);
};
```

重要的成员释义：

> loff_t (***llseek**) (struct file *, loff_t, int);
>
> llseek 方法用作改变文件中的当前读/写位置, 并且新位置作为(正的)返回值. loff_t 参数是一个"long offset", 并且就算在 32位平台上也至少 64 位宽. 错误由一个负返回值指示. 如果这个函数指针是 NULL（即填入 struct file_operations 结构体这个函数指针为 NULL）, seek 调用会以潜在地无法预知的方式修改 file 结构中的位置计数器( 在"file 结构" 一节中描述).
>
> ssize_t (***read**) (struct file *, char __user *, size_t, loff_t *);
>
> 用来从设备中获取数据. 在这个位置的一个空指针导致 read 系统调用以 -EINVAL("Invalid argument") 失败. 一个非负返回值代表了成功读取的字节数( 返回值是一个 "signed size" 类型, 常常是目标平台本地的整数类型).
>
> ssize_t (***write**) (struct file *, const char __user *, size_t, loff_t *);
>
> 发送数据给设备. 如果 NULL, -EINVAL 返回给调用 write 系统调用的程序. 如果非负, 返回值代表成功写的字节数.
>
> **read_iter** 和 **write_iter**
>
> 异步读 和 异步写，即完成操作之前就返回。而从4.1版本开始，关于异步读写的函数已经被read_iter和write_iter取代了。
>
> [Linux内核4.1在file_operations的read_iter和write_iter_潜行金枪鱼的博客-CSDN博客](https://blog.csdn.net/qq_41386447/article/details/117232407)。
>
> unsigned int (***poll**) (struct file *, struct poll_table_struct *);
>
> poll 方法是 3 个系统调用的后端: poll, epoll, 和 select, 都用作查询对一个或多个文件描述符的读或写是否会阻塞. poll 方法应当返回一个位掩码指示是否非阻塞的读或写是可能的, 并且, 可能地, 提供给内核信息用来使调用进程睡眠直到 I/O 变为可能. 如果一个驱动的 poll 方法为 NULL, 设备假定为不阻塞地可读可写.
>
> int (***ioctl**) (struct inode *, struct file *, unsigned int, unsigned long);
>
> ioctl 系统调用提供了发出设备特定命令的方法. 另外, 几个 ioctl 命令被内核识别而不必引用 fops 表. 如果设备不提供 ioctl 方法, 对于任何未事先定义的请求(-ENOTTY, "设备无这样的 ioctl"), 系统调用返回一个错误.
>
> int (***mmap**) (struct file *, struct vm_area_struct *);
>
> mmap 用来请求将设备内存映射到进程的地址空间. 如果这个方法是 NULL, mmap 系统调用返回 -ENODEV.
>
> int (***open**) (struct inode *, struct file *);
>
> 尽管这常常是对设备文件进行的第一个操作, 不要求驱动声明一个对应的方法. 如果这个项是 NULL, 设备打开一直成功, 但是你的驱动不会得到通知.
>
> int (***flush**) (struct file *); 很少用
>
> flush 操作在进程关闭它的设备文件描述符的拷贝时调用; 它应当执行(并且等待)设备的任何未完成的操作. 这个必须不要和用户查询请求的 fsync 操作混淆了. 当前, flush 在很少驱动中使用; SCSI 磁带驱动使用它, 例如, 为确保所有写的数据在设备关闭前写到磁带上. 如果 flush 为 NULL, 内核简单地忽略用户应用程序的请求.
>
> int (***release**) (struct inode *, struct file *);
>
> 在文件结构被释放时引用这个操作. 如同 open, release 可以为 NULL.
>
> int (***fsync**) (struct file *, struct dentry *, int);
>
> 这个方法是 fsync 系统调用的后端, 用户调用来刷新任何挂着的数据. 如果这个指针是 NULL, 系统调用返回 -EINVAL.
>
> int (***aio_fsync**)(struct kiocb *, int);
>
> 这是 fsync 方法的异步版本.
>
> int (***fasync**) (int, struct file *, int);
>
> 这个操作用来通知设备它的 FASYNC 标志的改变. 异步通知是一个高级的主题. 这个成员可以是NULL 如果驱动不支持异步通知.

### 总线平台驱动相关

参考 [Linux Platform驱动模型(一) _设备信息_Neilo_chen的博客-CSDN博客](https://blog.csdn.net/cjianeng/article/details/122776618)，[关于platform_device一些讲解_Leo丶Fun的博客-CSDN博客_platform_device](https://blog.csdn.net/weixin_38233274/article/details/109093673)。

详细用例 [Linux 设备驱动开发 —— platform设备驱动应用实例解析_zqixiao_09的博客-CSDN博客_linux设备驱动开发](https://blog.csdn.net/zqixiao_09/article/details/50888795)。[ 设备树——platform_driver_7个棋的博客-CSDN博客_platform_driver](https://blog.csdn.net/qq_40943525/article/details/110954722)。

### dts 和 device 和 driver 文件位置

dts：

> 可以在 shell 中**查看当前已经装载的设备树**：`/sys/firmware/devicetree` 目录下是以目录结构程现的dtb文件, 根节点对应base目录, 每一个节点对应一个目录, 每一个属性对应一个文件。**这些属性的值如果是字符串，可以使用cat命令把它打印出来；对于数值，可以用hexdump把它打印出来**。（一个单板启动时，u-boot先运行，它的作用是启动内核。U-boot会把内核和设备树文件都读入内存，然后启动内核。在启动内核时会把设备树在内存中的地址告诉内核。）

- driver ：/sys/bus/platform/drivers，platform 总线下注册的驱动都在这了。

- device：/sys/devices/platform。

- > platform_device 的信息：`/sys/devices/platform` 目录含有注册进内核的所有 platform_device。一个设备对应一个目录，进入某个目录后，如果它有 “driver” 子目录，就表示这个platform_device跟某个platform_driver配对了。**设备树被系统解析后生成的 platform_device 可以在这里面找到**。
  >
  > platform_driver 的信息：`/sys/bus/platform/drivers` 目录含有注册进内核的所有 platform_driver。一个driver对应一个目录，进入某个目录后，如果它有配对的设备，可以直接看到（一个平台设备只能配对一个平台驱动，一个平台驱动可以配对多个平台设备）。在装载 驱动程序中的 driver 的模块 之后就可以在 这个目录看到对应的 driver。

结构体成员只取一部分进行展示。

### platform_driver_register/unregister



#### platform_device 详细

```c
//include/linux/platform_device.h
 22 struct platform_device {                                    
 23         const char      *name;
 24         int             id;
 25         bool            id_auto;
 26         struct device   dev;
 27         u32             num_resources;
 28         struct resource *resource;
 29 
 30         const struct platform_device_id *id_entry;
 31 
 32         /* MFD cell pointer */
 33         struct mfd_cell *mfd_cell;
 34 
 35         /* arch specific additions */
 36         struct pdev_archdata    archdata;
 37 };

--23-->name就是设备的名字，注意， 模块名(lsmod)!=设备名(/proc/devices)!=设备文件名(/dev)，这个名字就是驱动方法和设备信息匹配的桥梁
--24-->表示这个platform_device对象表征了几个设备，当多个设备有共用资源的时候(MFD)，里面填充相应的设备数量，如果只是一个，填-1
--26-->父类对象(include/linux/device.h +722)，我们通常关心里面的platform_data和release,前者是用来存储私有设备信息的，后者是供当这个设备的最后引用被删除时被内核回调，注意和rmmod没关系。
--27-->资源的数量，即resource数组中元素的个数，我们用ARRAY_SIZE()宏来确定数组的大小(include/linux/kernel.h +54 #define ARRAY_SIZE(arr) (sizeof(arr) / sizeof((arr)[0]) )
--28-->资源指针，如果是多个资源就是struct resource[]数组名，

struct device {
    void   *driver_data;   /* data private to the driver */
    void   *platform_data; /* Platform specific data, device core doesn't touch it */
    struct device_node	*of_node; /* associated device tree node */ /* 支持设备树的 device 用于匹配 支持设备树的 driver */
    void	(*release)(struct device *dev);
    ...
};
struct device_node {
    const char *name;
    const char *type;
    phandle phandle;
    const char *full_name;
    struct property *properties; /* 含有 compatible 属性，用于匹配 支持设备树的 driver */
};

struct resource {  
    resource_size_t start;      //资源的起始值  
    resource_size_t end;        //资源的结束值  
    const char *name;  
    unsigned long flags;        //资源的类型，如 IORESOURCE_IO,IORESOURCE_MEM,IORESOURCE_IRQ,IORESOURCE_DMA  
    struct resource *parent, *sibling, *child;  
}; 

start表示资源开始的位置，如果是IO地址资源，就是起始物理地址，如果是中断资源，就是中断号;
end表示资源结束的位置，如果是IO地址地址，就是映射的最后一个物理地址，如果是中断资源，就不用填;
name就是这个资源的名字。
flags表示资源类型，提取函数在寻找资源的时候会对比自己传入的参数和这个成员，理论上只要和可以随便写，但是合格的工程师应该使用内核提供的宏，这些宏也在"ioport.h"中进行了定义，比如IORESOURCE_MEM表示这个资源是地址资源，IORESOURCE_IRQ表示这个资源是中断资源

//include/linux/ioport.h
#define IORESOURCE_BITS         0x000000ff      /* Bus-specific bits */
#define IORESOURCE_TYPE_BITS    0x00001f00      /* Resource type */
#define IORESOURCE_IO           0x00000100      /* PCI/ISA I/O ports */
#define IORESOURCE_MEM          0x00000200
#define IORESOURCE_REG          0x00000300      /* Register offsets */
#define IORESOURCE_IRQ          0x00000400          
#define IORESOURCE_DMA          0x00000800
#define IORESOURCE_BUS          0x00001000
...
#define DEFINE_RES_IO(_start, _size)   
#define DEFINE_RES_MEM(_start, _size)   
#define DEFINE_RES_IRQ(_irq)  
#define DEFINE_RES_DMA(_dma)   

下面是一个资源数组的实例，多个资源的时候就写成数组
struct resource res[] = {
	[0] = {
		.start	= 0x10000000,
		.end	= 0x20000000-1,
		.flags	= IORESOURCE_MEM
	},
	[1] = DEFINE_RES_MEM(0x20000000, 1024),
	[2] = {
		.start	= 10,   //中断号
		.flags	= IORESOURCE_IRQ|IRQF_TRIGGER_RISING //include/linux/interrupt.h
	},
	[3] = DEFINE_RES_IRQ(11),	
};

————————————另一个例子———————————————
static struct resource pxa27x_ohci_resources[] = {
 [0] = {
  .start  = 0x4C000000,
  .end    = 0x4C00ff6f,
  .flags  = IORESOURCE_MEM,
 },
 [1] = {
  .start  = IRQ_USBH1,
  .end    = IRQ_USBH1,
  .flags  = IORESOURCE_IRQ,
 },
};
static struct platform_device ohci_device = {
 .name  = "pxa27x-ohci",
 .id  = -1,
 .dev  = {
  .dma_mask = &pxa27x_dmamask,
  .coherent_dma_mask = 0xffffffff,
 },
 .num_resources  = ARRAY_SIZE(pxa27x_ohci_resources),  // 这里填入 struct resource 结构体数组的 结构体个数
 .resource       = pxa27x_ohci_resources,
};

———————————100ask例子———————————————————
static struct resource resources[] = {
    {
        .start = GROUP_PIN(3,1),
        .flags = IORESOURCE_IRQ,
        .name = "100ask_led_pin",
    },
    {
        .start = GROUP_PIN(5,8),
        .flags = IORESOURCE_IRQ,
        .name = "100ask_led_pin",
    },
};
static struct platform_device board_A_led_dev = {
    .name = "100ask_led",
    .num_resources = ARRAY_SIZE(resources),
    .resource = resources,
    .dev = {
        .release = led_dev_release,
    },
};
```

```c
/**
 *注册：把指定设备添加到内核中平台总线的设备列表，等待匹配,匹配成功则回调驱动中probe；
 */
int platform_device_register(struct platform_device *);

/**
 *注销：把指定设备从设备列表中删除，如果驱动已匹配则回调驱动方法和设备信息中的release；
 */
void platform_device_unregister(struct platform_device *);

// 通常，我们会将platform_device_register写在模块加载的函数中，将platform_device_unregister写在模块卸载函数中。
```

#### platform_driver 详细

```c
struct platform_driver {
	int (*probe)(struct platform_device *); /* driver 与 device 匹配成功之后调用该函数，一般进行获取资源和创建设备 */
	int (*remove)(struct platform_device *);
	void (*shutdown)(struct platform_device *);
	int (*suspend)(struct platform_device *, pm_message_t state);
	int (*resume)(struct platform_device *);
	struct device_driver driver;
	const struct platform_device_id *id_table;
};

struct platform_device_id {
	char name[PLATFORM_NAME_SIZE];
	kernel_ulong_t driver_data
			__attribute__((aligned(sizeof(kernel_ulong_t))));
};

struct device_driver {
	const char		*name; /* drvier 名字，用于 device 匹配 */
	struct bus_type		*bus;
 
	struct module		*owner;
	const char		*mod_name;	/* used for built-in modules */
 
	bool suppress_bind_attrs;	/* disables bind/unbind via sysfs */
 
	const struct of_device_id	*of_match_table; /* 用于支持设备树的 driver 匹配支持设设备树的 device */
	const struct acpi_device_id	*acpi_match_table;
 
	int (*probe) (struct device *dev);
	int (*remove) (struct device *dev);
	void (*shutdown) (struct device *dev);
	int (*suspend) (struct device *dev, pm_message_t state);
	int (*resume) (struct device *dev);
	const struct attribute_group **groups;
 
	const struct dev_pm_ops *pm;
 
	struct driver_private *p;
};

struct of_device_id
{
    undefined
    char name[32];
    char type[32];
    char compatible[128]; // 用于 device 和 driver 的 match
    const void *data;
};

———————100ask例子———————————
static struct platform_driver chip_demo_gpio_driver = {
    .probe      = chip_demo_gpio_probe, /* 创建设备 device_create，记录资源 */
    .remove     = chip_demo_gpio_remove, /* 删除设备 device_destroy */
    .driver     = {
        .name   = "100ask_led", /* 驱动名称，显示在 /sys/bus/platform/drivers */
    },
};
```



#### platform_get_xxx 获取资源

可参考 [linux （platform_driver）平台设备驱动常用API函数 (icode9.com)](https://www.icode9.com/content-3-637874.html)。

```c
struct resource *platform_get_resource(struct platform_device *dev, unsigned int type, unsigned int num);

功能：通过探测函数中有设备指针获得设备结构中的指定类型的资源结构地址。 这个函数是在驱动层的探测函数使用
参数： 
    dev ： 设备指针 ，实际就是探测函数参数
	type： 资源类型
	num：同类资源进行重新编号后的下标编号，和设备层中的资源数组不相同。（要注意这一点）
返回值：设备层资源结构数组中对应的资源结构首地址。 NULL:失败

unsigned int type决定资源的类型，unsigned int num决定type类型的第几份资源（从0开始）。即使同类型资源在资源数组中不是连续排放也可以定位得到该资源。
比如第一份IORESOURCE_IRQ类型资源在resource[2]，而第二份在resource[5]，那platform_get_resource(pdev,IORESOURCE_IRQ,0);可以定位第一份IORESOURCE_IRQ资源；platform_get_resource(pdev,IORESOURCE_IRQ,1);可以定位第二份IORESOURCE_IRQ资源。
```

```c
int platform_get_irq(struct platform_device *dev, unsigned int num);

功能： 通过设备指针获得设备结构中的指定编号的中断资源起始编号
参数：
	dev ：设备指针 ，实际就是探测函数参数
	num：同类资源进行重新编号后的下标编号，和设备层中的资源数组不相同。（要注意这一点）
返回值： >0 ：中断资源中的起始编号； -ENXIO：失败
```

```c
struct resource *platform_get_resource_byname(struct platform_device *dev,unsigned int type, const char *name);

功能：通过设备指针获得设备结构中的指定名字指定类型的资源结构内存地址
参数：
	dev ：设备指针 ，实际就是探测函数参数
	name：资源名
返回值：设备层资源结构数组中对应的资源结构首地址。 NULL:失败
```

```c
int platform_get_irq_byname(struct platform_device *dev, const char *name);

功能：通过设备指针获得设备结构中的指定名字的中断资源起始编号
参数：
	dev ：设备指针 ，实际就是探测函数参数
	name：中断资源名
返回值： >0 ：中断资源中的起始编号； -ENXIO：失败
```

###  ioctl

可以参考：

- [ ioctl函数详解（参数详解，驱动unlocked_ioctl使用、命令码如何封装）_相望@于江湖的博客-CSDN博客_ioctl函数参数](https://blog.csdn.net/weixin_39035140/article/details/110917841)。
- [Linux驱动学习6（ioctl的实现） - 灰信网（软件开发博客聚合） (freesion.com)](https://www.freesion.com/article/264147699/)。
- [（八）linux驱动之ioctl的使用 - 灰信网（软件开发博客聚合） (freesion.com)](https://www.freesion.com/article/7803425739/)。
- [linux驱动开发(四)：ioctl()函数_精致的螺旋线的博客-CSDN博客_ioctl函数linux](https://blog.csdn.net/baidu_38797690/article/details/123690825)。

### 等待队列 wait_queue

可参考：

- [小白学Linux——等待队列（waitqueue）_蚝油生菜的博客-CSDN博客_linux等待队列](https://blog.csdn.net/qq_36413391/article/details/118972155)。源码分析。
- `基本字符设备驱动程序-输入` 文件夹内`基本字符设备驱动程序获取数据的说明.md` 中的 `休眠-唤醒 机制` 一节。里面有说明都有什么 API，并且有程序例子。

初始化

```c
用一个宏，定义静态的
static DECLARE_WAIT_QUEUE_HEAD(gpio_key_wait);

或用函数，动态的
wait_queue_head_t wq;
init_waitqueue_head (&wq);

static inline void init_waitqueue_head(wait_queue_head_t *q)
{
	q->lock = SPIN_LOCK_UNLOCKED;
	INIT_LIST_HEAD(&q->task_list);
}
```

> **wait_event(wq, condition)**：调用wait_event宏定义后进程进入睡眠状态直到传入的条件为真。该进程进入睡眠状态(TASK_UNINTERRUPTIBLE)，直到条件为真。每次唤醒等待队列wq时都会检查条件。休眠，直到condition为真；  退出的唯一条件是condition为真，信号也不能打断。
>
> **wait_event_interruptible(wq, condition)**：调用wait_event_interruptible宏定义后进程进入睡眠状态直到传入的条件为真。该进程进入睡眠状态(TASK_INTERRUPTIBLE)，直到条件为真或者收到信号。每次唤醒等待队列wq时都会检查条件。如果睡眠期间被信号中断，该函数将返回 -ERESTARTSYS，如果条件为真，则返回0。休眠，直到condition为真；  休眠期间是可被打断的，可以被信号打断。
>
> **wake_up(x)**：从处于不可中断睡眠状态的等待队列中唤醒一个进程。  唤醒x队列中状态为 “TASK_INTERRUPTIBLE” 或 “TASK_UNINTERRUPTIBLE” 的线程，只唤醒其中的一个线程。
>
> **wake_up_interruptible(x)**：从处于可中断睡眠状态的等待队列中唤醒一个进程。唤醒x队列中状态为 “TASK_INTERRUPTIBLE” 的线程，只唤醒其中的一个线程。

## 其它用到的 设备相关API

### copy_from_user / copy_to_user

内核空间 的数据与 应用/用户进程 的数据相互之间的拷贝。

- [初步解析内核函数copy_to_user和copy_from_user_江东风又起的博客-CSDN博客_copy_to_user](https://blog.csdn.net/ysgjiangsu/article/details/50017737)。
- [linux系统中copy_to_user()函数和copy_from_user()函数的用法_fxfreefly的博客-CSDN博客_copytouser函数](https://blog.csdn.net/bhniunan/article/details/104088763)。

```c
unsigned long copy_from_user(void *to, const void __user *from, unsigned long n);
/* 失败返回没有被拷贝的字节数，成功返回 0 */

unsigned long copy_to_user(void __user *to, const void *from, unsigned long n);
/* 成功返回 0，失败返回没有拷贝成功的数据字节数 */
```

### ioremap / iounmap 

用来将物理地址映射到一个虚拟地址，内核进程通过该虚拟地址访问到实际物理地址，安全。

把物理地址phys_addr开始的一段空间(大小为size)，映射为虚拟地址；返回值是该段虚拟地址的首地址。

`virt_addr = ioremap(phys_addr, size);`

实际上，它是按页(4096字节)进行映射的，是整页整页地映射的。

假设phys_addr = 0x10002，size=4，ioremap的内部实现是：

a. phys_addr按页取整，得到地址0x10000

b. size按页取整，得到4096

c. 把起始地址0x10000，大小为4096的这一块物理地址空间，映射到虚拟地址空间，

  假设得到的虚拟空间起始地址为0xf0010000

d. 那么phys_addr = 0x10002对应的virt_addr = 0xf0010002

### EXPORT_SYMBOL

变量或函数的导出，表示这些变量对内核公开，其它模块可以访问到，否则访问是 NULL。

使用方法：

1. 就在 驱动程序 .h 文件里面 声明所有要 导出的 函数、变量 和结构体结构（不是结构体变量的定义，而是结构体本身定义放到 驱动程序的 .h 文件里）等，并且都加上 extern 修饰，函数除外。
2. 在驱动程序里面 定义和初始化这些函数、变量和结构体等。
3. 在 其它要用到 这些 函数和变量的 模块 的驱动文件里面 include 前面的驱动程序 .h 文件，然后就可以直接调用了。

> a.c编译为a.ko，里面定义了func_a；如果它想让b.ko使用该函数，那么a.c里需要导出此函数。即 如果 a.c, b.c 分别编译出两个 .ko，即 a.ko 和 b.ko，则需使用这个来导出。并且，使用时要先加载a.ko。如果先加载b.ko，会有类似如下“Unknown symbol”的提示。
>
> 如果 a.c, b.c 编译在一起，编译出一个 .ko，则无需使用这个来导出。

- [EXPORT_SYMBOL的作用是什么 (eepw.com.cn)](http://eleaction01.spaces.eepw.com.cn/articles/article/item/189093)。
- [linux export_symbol 变量,Linux的EXPORT_SYMBOL和EXPORT_SYMBOL_GPL的使用和区别_App小公主的博客-CSDN博客](https://blog.csdn.net/weixin_31899235/article/details/116876348)。

### file_inode / iminor

参考 [字符设备驱动框架2：设备文件(设备节点)如何和驱动建立联系-Linux字符设备中的两个重要结构体(file、inode)_欧阳海宾的博客-CSDN博客](https://blog.csdn.net/oyhb_1992/article/details/77110676) 就比较清楚了。

> 一般而言在驱动程序的设计中，会关系 struct file 和 struct inode 这两个结构体。
>
> 用户空间使用open()系统调用函数打开一个字符设备时（ int fd = open("dev/demo", O_RDWR) ）大致有以下过程：
>
> 1. 在虚拟文件系统VFS中的查找对应与字符设备对应 struct inode节点
> 2. 遍历字符设备列表（chardevs数组），根据inod节点中的 cdev_t设备号找到cdev对象
> 3. 创建struct file对象（系统采用一个数组来管理一个进程中的多个被打开的设备，每个文件秒速符作为数组下标标识了一个设备对象）
> 4. 初始化struct file对象，将 struct file对象中的 file_operations成员指向 struct cdev对象中的 file_operations成员（file->fops =  cdev->fops）
> 5. 回调file->fops->open函数
>
> **inode 结构体**
>
> ​     VFS inode 包含文件访问权限、属主、组、大小、生成时间、访问时间、最后修改时间等信息。它是Linux 管理文件系统的最基本单位，也是文件系统连接任何子目录、文件的桥梁。
>
> ​    内核使用inode结构体在内核内部表示一个文件。因此，它与表示一个已经打开的文件描述符的结构体(即file 文件结构)是不同的，我们可以使用多个file 文件结构表示同一个文件的多个文件描述符，但此时，所有的这些file文件结构全部都必须只能指向一个inode结构体。
>
>    inode结构体包含了一大堆文件相关的信息，但是就针对驱动代码来说，我们只要关心其中的两个域即可：
>
> 1. dev_t i_rdev;   表示设备文件的结点，这个域实际上包含了设备号。
> 2. struct cdev *i_cdev;　　struct cdev是内核的一个内部结构，它是用来表示字符设备的，当inode结点指向一个字符设备文件时，此域为一个指向inode结构的指针。
>
> **file 文件结构体**
>
> ​    在设备驱动中，这也是个非常重要的数据结构，必须要注意一点，这里的file与用户空间程序中的FILE指针是不同的，用户空间FILE是定义在C库中，从来不会出现在内核中。而struct file，却是内核当中的数据结构，因此，它也不会出现在用户层程序中。
>
> ​    file结构体指示一个已经打开的文件（设备对应于设备文件），其实系统中的每个打开的文件在内核空间都有一个相应的struct file结构体，它由内核在打开文件时创建，并传递给在文件上进行操作的任何函数，直至文件被关闭。如果文件被关闭，内核就会释放相应的数据结构。
>
>    在内核源码中，struct file要么表示为file，或者为filp(意指“file pointer”), 注意区分一点，file指的是struct file本身，而filp是指向这个结构体的指针。

参考 [Linux中的File_operations结构体-pudn.com](https://www.pudn.com/news/628f831fbf399b7f351e6d8a.html)。

> struct inode被内核用来代表一个文件，注意和struct file的区别，struct inode一个是代表文件，struct file一个是代表打开的文件
>
> struct inode包括很重要的二个成员：
>
> - dev_t i_rdev 设备文件的设备号
> - struct cdev *i_cdev 代表字符设备的数据结构
>
> struct inode结构是用来在内核内部表示文件的.同一个文件可以被打开好多次,所以可以对应很多struct file,但是只对应一个struct inode.

- 在 xxx_write() 和 xxx_read() 函数里面，实际控制一个设备类下面的哪一个设备，根据子设备号，获取通过 file_inode() 根据 file 得到文件的 inode，再用 iminor() 根据 inode 得到子/次设备号。

  ```c
  /* 提取主设备号 */
  static inline unsigned imajor(const struct inode *inode)
  {
  　　return MAJOR(inode->i_rdev);
  }
  /* 提取次设备号 */
  static inline unsigned iminor(const struct inode *inode)
  {
  　　return MINOR(inode->i_rdev);
  }
  ```

  

- 在 xxx_open() 和 xxx_close() 里面 可以根据 int minor = iminor(node); 直接获得次设备号（来或者这一个外设的哪一个具体资源）。

### devm_kzalloc / devm_kfree

这个功能分配的内存会在驱动卸载时自动释放。参考 [linux内核中的devm_kzalloc_不止冬雷和夏雪的博客-CSDN博客_devm_kzalloc](https://blog.csdn.net/wang_518/article/details/108913575)。

```c
void * devm_kzalloc (struct device * dev, size_t size, gfp_t gfp);
void devm_kfree(struct device * dev，void * p);
```

参数 dev 是 申请内存的目标设备 device，其它参数与 kzalloc一致。

以下为 request/region/release 相关 API，不常用。

参考 [linux （platform_driver）平台设备驱动常用API函数 (icode9.com)](https://www.icode9.com/content-3-637874.html)。

申请内存资源函数

- request_region
- request_mem_region
-  devm_request_region
- devm_request_mem_region

释放内存资源

- release_region
- release_ mem_region
- devm_release_region
- devm_release_mem_region

## 常用内核态 API

### 内存申请

一文说明清楚：[Linux内核空间内存申请函数kmalloc、kzalloc、vmalloc的区别【转】_danxibaoxxx的博客-CSDN博客](https://blog.csdn.net/danxibaoxxx/article/details/99357541)。

更多 API [Linux内核API 内存管理|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/linux-kernel-api-memory-management/linux-kernel-api-memory-management.html)。 [ linux中kmalloc函数详解_fulinux的博客-CSDN博客_kmalloc linux](https://fulinux.blog.csdn.net/article/details/8635234)。

#### kmalloc()

```c
#include <linux/slab.h>

void *kmalloc(size_t size, gfp_t flags);
void kfree(const void *objp);
```

> kmalloc() 申请的内存位于物理内存映射区域，而且在物理上也是连续的，它们与真实的物理地址只有一个固定的偏移，因为存在较简单的转换关系，所以对申请的内存大小有限制，**不能超过128KB**。 
>
> 较常用的 flags（分配内存的方法）：
>
> - **GFP_ATOMIC** —— 分配内存的过程是一个原子过程，分配内存的过程不会被（高优先级进程或中断）打断；
> - **GFP_KERNEL** —— 正常分配内存；
> - **GFP_DMA** —— 给 DMA 控制器分配内存，需要使用该标志（DMA要求分配虚拟地址和物理地址连续）。
> - 更多 标志位 的列举 [linux中kmalloc函数详解_fulinux的博客-CSDN博客_kmalloc函数](https://fulinux.blog.csdn.net/article/details/8635234)。

下文引自 [ linux 字符驱动 申请内存最大,Linux驱动技术(一) _内存申请_一只小短腿的博客-CSDN博客](https://blog.csdn.net/weixin_33375514/article/details/116727531)。

> GFP_KERNEL是最常用的flag，注意，使用这个flag来申请内存时，如果暂时不能满足，**会引起进程阻塞**，So，一定不要在中断处理函数、tasklet和内核定时器等非进程上下文中使用GFP_KERNEL！

#### kzalloc()

```c
#include <linux/slab.h>

/**
 * kzalloc - allocate memory. The memory is set to zero.
 * @size: how many bytes of memory are required.
 * @flags: the type of memory to allocate (see kmalloc).
 */
 static inline void *kzalloc(size_t size, gfp_t flags)
{
    return kmalloc(size, flags | __GFP_ZERO);
}

void kfree(const void *objp);
```

> kzalloc() 函数与 kmalloc() 非常相似，参数及返回值是一样的，可以说是前者是后者的一个变种，因为 kzalloc() 实际上只是额外附加了 **__GFP_ZERO** 标志。所以它除了申请内核内存外，还会**对申请到的内存内容清零**。
>
> kzalloc() 对应的内存释放函数也是 kfree()。

#### vmalloc()

```c
#include <linux/vmalloc.h>
#include <linux/init.h>
#include <linux/module.h>

void *vmalloc(unsigned long size);
void vfree(const void *addr);
```

> vmalloc() 函数则会在虚拟内存空间给出一块连续的内存区，但这片连续的虚拟内存在物理内存中并不一定连续。由于 vmalloc() 没有保证申请到的是连续的物理内存（**所以不能用来做DMA之类的操作**），**对申请的内存大小没有限制**，如果需要申请较大的内存空间就需要用此函数了。
>
> 注意：vmalloc() 和 vfree() 可以睡眠，因此不能从中断上下文调用。 
>
> vmalloc() 还会调用使用GFP_KERN的kmalloc，一定不要在中断处理函数、tasklet和内核定时器等非进程上下文中使用 vmalloc！

#### 总结

> kmalloc()、kzalloc()、vmalloc() 的共同特点是：
>
> 1. 用于申请内核空间的内存；
> 2. 内存以字节为单位进行分配；
> 3. 所分配的内存虚拟地址上连续；
>
> kmalloc()、kzalloc()、vmalloc() 的区别是：
>
> 1. kzalloc 是强制清零的 kmalloc 操作；（以下描述不区分 kmalloc 和 kzalloc）
> 2. kmalloc 分配的内存大小有限制（128KB），而 vmalloc 没有限制；
> 3. kmalloc 可以保证分配的内存物理地址是连续的，但是 vmalloc 不能保证；
> 4. kmalloc 分配内存的过程可以是原子过程（使用 GFP_ATOMIC），而 vmalloc 分配内存时则可能产生阻塞；
> 5. kmalloc 分配内存的开销小，因此 kmalloc 比 vmalloc 要快；
>
> 一般情况下，内存只有在要被 DMA 访问的时候才需要物理上连续，但为了性能上的考虑，内核中一般使用 kmalloc()，而只有在需要获得大块内存时才使用 vmalloc()。例如，当模块被动态加载到内核当中时，就把模块装载到由 vmalloc() 分配的内存上。

> 引自 100ask 手册
>
> kmalloc 分配到的内存物理地址是连续的 
>
> kzalloc 分配到的内存物理地址是连续的，内容清 0 
>
> vmalloc 分配到的内存物理地址不保证是连续的 
>
> vzalloc 分配到的内存物理地址不保证是连续的，内容清 0 

#### 内核驱动中的内存用于mmap

> 引自 100ask 手册
>
> 我们应该使用 kmalloc 或 kzalloc，这样得到的内存物理地址是连续的，在 mmap 时后 APP 才可以使用同一个基地址去访问这块内存。(如果物理地址不连续，就要执行多次 mmap了)。

> 引自 [ mmap函数_vmalloc与mmap_weixin_39611161的博客-CSDN博客](https://blog.csdn.net/weixin_39611161/article/details/111274270)。
>
> 需要映射到用户空间的内存段，不能直接利用vmalloc()分配，而应该使用**vmalloc_user()**函数。
>
> [Linux内核API vmalloc_user|极客笔记 (deepinout.com)](https://deepinout.com/linux-kernel-api/linux-kernel-api-memory-management/linux-kernel-api-vmalloc_user.html)。
>
> vmalloc_user() 的测试：[Linux内核 vmalloc_user()|酷客网 (coolcou.com)](https://www.coolcou.com/linux-kernel/linux-kernel-memory-management-api/the-linux-kernel-vmalloc-user.html)。

### likely 与 unlikely

引自 [linux内核中likely与unlikely_夜风~的博客-CSDN博客_linux unlikely](https://blog.csdn.net/u014470361/article/details/81193023)。

> 简单从表面上看 `if( likely(value) ){ }` 和 `if(unlikely(value)){ }else{ }`。
> 也就是likely和unlikely是一样的，但是实际上执行是不同的，加likely的意思是value的值为真的可能性更大一些，那么执行if的机会大，而unlikely表示value的值为假的可能性大一些，执行else机会大一些。
>
> 加上这种修饰，编译成二进制代码时likely使得if后面的执行语句紧跟着前面的程序，unlikely使得else后面的语句紧跟着前面的程序，这样就会被**cache预读取**，增加程序的**执行速度**。
>
> 用来引导gcc进行条件分支预测。在一条指令执行时，由于流水线的作用，CPU可以同时完成下一条指令的取指，这样可以提高CPU的利用率。在执行条件分支指令时，CPU也会预取下一条执行，但是如果条件分支的结果为跳转到了其他指令，那CPU预取的下一条指令就没用了，这样就降低了流水线的效率。
>
> 简单理解：
>
> - likely(x) 代表 x 是 逻辑真 的可能性比较大。
> - unlikely(x) 代表 x 是 逻辑假 的可能性比较大。

### 内核中错误处理

参考：

- [linux中ERR_PTR、PTR_ERR、IS_ERR和IS_ERR_OR_NULL_夜风~的博客-CSDN博客_linux ptr](https://blog.csdn.net/u014470361/article/details/81175817)。
- [ Linux内核使用ERR_PTR和PTR_ERR等函数来实现指针函数返回错误码_tanglinux的博客-CSDN博客](https://tanglinux.blog.csdn.net/article/details/78065586)。
- [Linux 内核IS_ERR函数 - 简书 (jianshu.com)](https://www.jianshu.com/p/7bc78698ed09)。
- [【Linux内核】Linux的errno和ERR_PTR、PTR_ERR简介_gccwdn的博客-CSDN博客](https://blog.csdn.net/u014001096/article/details/124896853)。

> linux内核中判断返回指针是否错误的内联函数主要有：**ERR_PTR、PTR_ERR、IS_ERR 和 IS_ERR_OR_NULL**等。
>
> 在写设备驱动程序的过程中，涉及到的任何一个指针，必然有三种情况：
>
> 1. **有效指针**；
> 2. **NULL，空指针**；
> 3. **错误指针，或者说无效指针**。

### 内核中对字符串的操作

具体 API 用法看 [linux内核驱动中对字符串的操作【转】 - 走看看 (zoukankan.com)](http://t.zoukankan.com/sky-heaven-p-4826009.html)。

> ```c
> #include <linux/string.h>
> 
> int strnicmp(const char *s1, const char *s2, size_t len)  
> int strcasecmp(const char *s1, const char *s2)  
> int strncasecmp(const char *s1, const char *s2, size_t n)  
> char *strcpy(char *dest, const char *src)  
> char *strncpy(char *dest, const char *src, size_t count)  
> size_t strlcpy(char *dest, const char *src, size_t size)  
> char *strcat(char *dest, const char *src)  
> char *strncat(char *dest, const char *src, size_t count)  
> size_t strlcat(char *dest, const char *src, size_t count)  
> int strcmp(const char *cs, const char *ct)  
> int strncmp(const char *cs, const char *ct, size_t count)  
> char *strchr(const char *s, int c)  
> char *strrchr(const char *s, int c)  
> char *strnchr(const char *s, size_t count, int c)  
> char *skip_spaces(const char *str)  
> char *strim(char *s)  
> size_t strlen(const char *s)  
> size_t strnlen(const char *s, size_t count)  
> char *strpbrk(const char *cs, const char *ct)  
> char *strsep(char **s, const char *ct)  
> bool sysfs_streq(const char *s1, const char *s2)  
> void *memset(void *s, int c, size_t count)  
> void *memcpy(void *dest, const void *src, size_t count)  
> void *memmove(void *dest, const void *src, size_t count)  
> int memcmp(const void *cs, const void *ct, size_t count)  
> void *memscan(void *addr, int c, size_t size)  
> char *strstr(const char *s1, const char *s2)  
> char *strnstr(const char *s1, const char *s2, size_t len)  
> void *memchr(const void *s, int c, size_t n)  
> ```

### Linux 内核常见宏的作用

[Linux内核常见宏的作用_-CSDN博客](https://blog.csdn.net/thisway_diy/article/details/84621827)。

### Linux 内核中随机数函数

参考 [了解从Linux内核中获取真随机数_Linux加油站的博客-CSDN博客_linux 真随机数](https://blog.csdn.net/m0_74282605/article/details/128017996)。

