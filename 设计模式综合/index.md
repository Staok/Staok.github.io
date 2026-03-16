# （集合）C / C++ 设计模式综合


# C / C++ 设计模式综合



本文最新原文和相关资料在 [Github](https://github.com/Staok/C-Cpp-design-patterns) / [Gitee](https://gitee.com/staok/C-Cpp-design-patterns) 仓库里，其它地方不会跟进，因此推荐到仓库里面进行查阅或下载。



# 设计模式目录

都是好文！

背景和梳理：

- [学无止境 之一 C 嵌入式设计模式（Design Patterns for Embedded Systems in C）笔记-CSDN博客](https://blog.csdn.net/zcshoucsdn/article/details/80217199)。
- [设计模式 (计算机) - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/zh-hans/设计模式_(计算机))。（需要科学上网）



设计模式目录：

- [设计模式目录：22种设计模式 (refactoringguru.cn)](https://refactoringguru.cn/design-patterns/catalog)。
- [设计模式 | 菜鸟教程 (runoob.com)](https://www.runoob.com/design-pattern/design-pattern-tutorial.html)。

- [图说设计模式 — Graphic Design Patterns (design-patterns.readthedocs.io)](https://design-patterns.readthedocs.io/zh-cn/latest/)。
- [设计模式 | design-patterns (jueee.github.io)](https://jueee.github.io/design-patterns/)。



- [快速记忆23种设计模式 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/128145128)。
- [23 种设计模式详解（全23种）_23种设计模式-CSDN博客](https://blog.csdn.net/A1342772/article/details/91349142)。
- [C++设计模式-设计模式简述_C++语言-CSDN专栏](https://download.csdn.net/blog/column/12435130/136552720)。
- [C语言和设计模式（总结篇）_设计模式c语言-CSDN博客](https://blog.csdn.net/feixiaoxing/article/details/7294900)。
- [EmbeddedSystem/DesignPattern at master · SummerGift/EmbeddedSystem (github.com)](https://github.com/SummerGift/EmbeddedSystem/tree/master/DesignPattern)。



More:

- 原文仓库中的 `设计模式介绍-仓库` 文件夹里里面有 离线了 一些优秀仓库。

- [Staok/Cpp-Learning (github.com)](https://github.com/Staok/Cpp-Learning) 里面的《C++学习总结备查》一文中的 `C++ 精品汇总`、`C++精品仓库` 之类的小节有更多网络优秀总结。



# 重构的艺术

- [重构指北——《重构，改善既有代码设计》精读本文总结自笔者的开发经验以及 Martin Fowler 的《重构，改善既有代 - 掘金 (juejin.cn)](https://juejin.cn/post/6996990620233383967)。
- [Introduction · 重构-改善既有代码的设计（笔记） (gitbooks.io)](https://zacharychang.gitbooks.io/refactoring-improving-the-design-of-existing-code/content/)。
- [《重构:改善既有代码的设计》读书笔记 (cnblogs.com)](https://www.cnblogs.com/wmyskxz/p/10990059.html)。
- [Refactoring: clean your code (refactoringguru.cn)](https://refactoringguru.cn/refactoring)。





# 设计模式详解

参考并总结 [设计模式目录：22种设计模式](https://refactoringguru.cn/design-patterns/catalog)。

更多参考 [设计模式 | 菜鸟教程](https://www.runoob.com/python-design-pattern/python-design-pattern-tutorial.html)。



---

## 创建型模式（包含实例代码）

这里直接给代码进行说明。具体设计模式描述见上面链接里面，这里给出我实现的代码结构，有一些自己的见解进行优化、融合，与经典的设计模式结构不完全一样。



### Pimpl

MyInterface.h 文件：

```c++
#pragma once

// 减少头文件包含链，大型项目编译优化。
// 隐藏第三方库依赖，减少编译依赖和暴露的实现细节。
#include <memory>

class MyInterface {
public:
    MyInterface();
    ~MyInterface();

    // 只暴露公共API。
    // 用于第三方API封装。

    int publicApi1();
    int publicApi2();

private:

    // 这个暴露公共API的头文件中不包含任何成员变量。
    // 修改 Impl 的实现不会引起 MyInterface 的重新编译，接口稳定。

    struct Impl;
    std::unique_ptr<Impl> mImpl;
};

```



MyInterfaceImpl.cpp 文件：

```c++
#include "MyInterface.h"

// ========= MyInterface 的具体声明 =========

// 这里可以引用包含一些具体的其它头文件依赖

struct MyInterface::Impl {
    int publicApi1();
    int publicApi2();
};

int MyInterface::Impl::publicApi1()
{
    return 42;
}

int MyInterface::Impl::publicApi2()
{
    return 84;
}

// ========= MyInterface 的具体实现 =========
// 基本上就是把 Impl 的方法调用转发过去。

MyInterface::MyInterface()
    : mImpl(std::make_unique<Impl>())
{
}

MyInterface::~MyInterface() = default;

int MyInterface::publicApi1() { return mImpl->publicApi1(); }

int MyInterface::publicApi2() { return mImpl->publicApi2(); }

```



### Builder

ProductBuilder.h 文件：

```c++
#pragma once

// 对于某一类产品的复杂对象构建，使用建造者/工厂模式（这里混合了常见的教程里面的概念）
// 一类产品应对应一个Builder类，负责该类产品的各个部分的设置和产品类的创建
// 并可灵活的增减和修改产品的设置和内部实现

// 其中 "// ..." 表示可以继续扩展的部分，而其余部分基本都是固定的可以不动。

// 函数执行返回值约定：
//      0 表示成功
//    < 0 表示失败
//    > 0 表示警告

#include <cstddef>
#include <cstdint>
#include <cstdio>
#include <memory>
#include <string>

// ========= 所有类型产品可以有一个共同的基类 =========

class ObjectBasic {
public:
    ObjectBasic() = default;
    virtual ~ObjectBasic() = default;

protected:
    size_t mId;
    // ...
};

// ========= 某一类产品的抽象类的定义 =========

enum class ProductType {
    ProductA,
    ProductB,

    // 可扩展更多产品类型
    // ...
};

// 产品的各个设置项，必须包含所有，方便 Builder 设置，以及未来的类实例的克隆等作用
struct ProductSettings {

    ProductType type = ProductType::ProductA;

    // 基本设置项
    // 需要都写上默认值
    int32_t partA = 0;
    double partB = 0.0;
    std::string partC = "";
    // ...

    // 如果设置项有自定义类型，则需要提供该类型的判断相等等基础操作符重载

    // 基础操作符设施
    // 重置，赋值运算符，等号运算符，等

    void reset() {
        partA = 0;
        partB = 0.0;
        partC.clear();
        // ...
    }

    bool operator==(const ProductSettings& other) const {
        return ( ( partA == other.partA ) &&
                 ( partB == other.partB ) &&
                 ( partC == other.partC ) );
                 // ...
    }
};

#define HANDLE_ISUNCHANGED(settingVar, newValue, changedExec, noChangeExec) \
    if (!(settingVar == newValue)) {    \
        settingVar = newValue;          \
        changedExec                     \
    } else {                            \
        noChangeExec                    \
    }

#define HANDLE_RET(ret, fun, retIs0ThanExec, retSmallThanExec, retLargerThanExec) \
    ret = fun;                  \
    if (ret == 0) {             \
        retIs0ThanExec          \
    } else if (ret < 0) {       \
        retSmallThanExec        \
    } else {                    \
        retLargerThanExec       \
    }

#define SET_GET_PART_IMPL(funPartName, varPartName, partType, updateFunc, printFunc) \
    virtual int32_t set##funPartName(const partType& value) {  \
        HANDLE_ISUNCHANGED(                             \
            varPartName, value,                         \
            int ret = -1;                               \
            HANDLE_RET(                                 \
                ret , updateFunc ,                      \
                return 0; ,                             \
                printFunc(#updateFunc " failed, ret=%d\n", ret); \
                return ret; ,                            \
                printFunc(#updateFunc " warning, ret=%d\n", ret); \
                return ret;                             \
            ),                                          \
            return 0;                                   \
        );                                              \
    }                                                   \
    virtual partType get##funPartName() const {                 \
        return varPartName;                             \
    }

class ProductBasic : ObjectBasic {
public:
    ProductBasic() = default;
    virtual ~ProductBasic() = default;

    // 注意如果这些 API 需要多线程使用，则需要加锁保护

    // 这里仅仅设置和获取设置值，但不生效。可以用于"克隆"来自另一个实例的设置值
    SET_GET_PART_IMPL(Settings, mSettings, ProductSettings, 0, printf); // 打印函数按需修改

    // 公共的设置项
    // 设置和获取各个部分的值，并立即生效
    // 用于单独设置某个部分，操作细节
    SET_GET_PART_IMPL(PartA, mSettings.partA, int32_t, updatePartA(), printf);
    SET_GET_PART_IMPL(PartB, mSettings.partB, double, updatePartB(), printf);
    SET_GET_PART_IMPL(PartC, mSettings.partC, std::string, updatePartC(), printf);
    // ...

    // 根据最新的 mSettings 进行整体更新，使所有设置生效（进行设置项生效，运行、显示等）。
    // 里面写上所有设置值生效函数。
    // 用于创造新实例并填入所有设置值后的一次整体更新
    // 或批量设置后再生效，减少重复更新开销
    virtual int32_t makeSettingsAvailable() {

        int32_t ret = -1;

        HANDLE_RET(
            ret , updatePartA() ,
            return 0; ,
            printf("updatePartA() failed, ret=%d\n", ret);
            return ret; ,
            printf("updatePartA() warning, ret=%d\n", ret);
            return ret; );

        HANDLE_RET(
            ret , updatePartB() ,
            return 0; ,
            printf("updatePartB() failed, ret=%d\n", ret);
            return -1; ,
            printf("updatePartB() warning, ret=%d\n", ret);
            return 1; );

        HANDLE_RET(
            ret , updatePartC() ,
            return 0; ,
            printf("updatePartC() failed, ret=%d\n", ret);
            return -1; ,
            printf("updatePartC() warning, ret=%d\n", ret);
            return 1; );

        // ...

        return 0;
    }

    // 一些公共的纯虚函数接口，由具体产品类实现
    virtual void doSomething() = 0;
    // ...

protected:
    ProductSettings mSettings;

    // 实际更新各个部分的虚函数，由具体产品类实现
    virtual int32_t updatePartA() = 0;
    virtual int32_t updatePartB() = 0;
    virtual int32_t updatePartC() = 0;
    // ...
};

class ProductNextBasic : ObjectBasic {
    // ...
};

// ========= 具体产品类的定义 =========
// 最好每个具体产品类单独放在一个头文件和源文件中（这里只留前置声明）。
// 可以用 Pimpl 模式隐藏实现细节（这里没有，对于只暴露头文件的情况需要用）。

class ProductAConcrete : public ProductBasic {
public:
    ProductAConcrete(const ProductSettings& settings) {
        mSettings = settings;
    }
    ~ProductAConcrete() override = default;

    void doSomething() override {
        // 具体实现
    }

    // ...

protected:
    int32_t updatePartA() override {
        // 具体实现
        // 根据 mSettings.partA 的值更新部分 A
        return 0;
    }

    int32_t updatePartB() override {
        // 具体实现
        // 根据 mSettings.partB 的值更新部分 B
        return 0;
    }

    int32_t updatePartC() override {
        // 具体实现
        // 根据 mSettings.partC 的值更新部分 C
        return 0;
    }

    // ...

private:
    // 具体产品类的私有成员变量

    // 如果新增新的设置项，需要在这里添加对应的成员变量的 updatePartX() 实现
    // 并添加对应设置项的 SET_GET_PART_IMPL(PartX, mSettings.PartX, std::string, updatePartX(), printf);
    // 并重写 makeSettingsAvailable()，里面先调用 ProductBasic::makeSettingsAvailable()，再调用这些新增的 updatePartX() 方法
};

class ProductBConcrete : public ProductBasic {
public:
    ProductBConcrete(const ProductSettings& settings) {
        mSettings = settings;
    }
    ~ProductBConcrete() override = default;

    void doSomething() override {
        // 具体实现
    }

    // ...

protected:
    int32_t updatePartA() override {
        // 具体实现
        // 根据 mSettings.partA 的值更新部分 A
        return 0;
    }
    int32_t updatePartB() override {
        // 具体实现
        // 根据 mSettings.partB 的值更新部分 B
        return 0;
    }

    int32_t updatePartC() override {
        // 具体实现
        // 根据 mSettings.partC 的值更新部分 C
        return 0;
    }

    // ...
};

// ========= ProductBuilder 类 =========
class ProductBuilder {
public:
    ProductBuilder() = default;
    virtual ~ProductBuilder() = default;

    std::shared_ptr<ProductBasic> createProduct(const ProductSettings& settings) {
        switch (settings.type) {
            case ProductType::ProductA:
                return std::make_shared<ProductAConcrete>(settings);
            case ProductType::ProductB:
                return std::make_shared<ProductBConcrete>(settings);
            // 可扩展更多产品类型
            // ...
            default:
                printf("Unknown ProductType: %d\n", static_cast<int>(settings.type));
                return nullptr;
        }
    }
};

// 使用例子：
// ProductBuilder builder;
// auto productA = builder.createProduct(
//     ProductSettings{
//         .type = ProductType::ProductA,
//         .partA = 10,
//         .partB = 20.5,
//         .partC = "ExampleA"
//     }
// );
// 创建的多个产品实例，可以用 ToolBox/GeneralContainer（暂未开源） 来管理。
//    简单的就用 std::vector 之类的容器 添加到 ProductBuilder 类里面 进行管理。
// 创建多个不同设置的产品实例之后，统一调用 makeSettingsAvailable() 使批量设置生效（重要）。

```



### Singleton

Singleton.h 文件：

```c++
#pragma once

// 使用例子：
// Singleton::getInst().doSomething();

class Singleton {
public:
    // 获取单例实例的静态方法
    // C++11 起，静态局部变量的初始化是线程安全的 (Meyers' Singleton)
    static Singleton& getInst();

    // 示例业务方法
    void doSomething();

    // 删除拷贝构造函数和赋值运算符，防止复制
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

private:
    // 私有构造函数，防止外部实例化
    Singleton() = default;
    ~Singleton() = default;
};

// 或者，如果一个类只需要一个全局实例，可以使用全局实例的方式实现单例模式，示例如下：
// 单例类只用 .h 文件里面 放一个 `extern class classType Global<name>Inst;` 这种方式
// （在 .cpp 里面去声明 `calss classType Global<name>Inst;`），之后全局调用 `Global<name>Inst` 即可。

```



Singleton.cpp 文件：

```c++
#include <iostream>

#include "Singleton.h"

Singleton& Singleton::getInst() {
    // 静态局部变量，第一次调用时初始化，程序结束时销毁
    // C++11 标准保证了并发环境下的线程安全性
    static Singleton instance;
    return instance;
}

void Singleton::doSomething() {
    std::cout << "Singleton instance address: " << this << " is doing something." << std::endl;
}

```



---

## 结构型模式



### 适配器(adapter) & 桥接(bridge) & 组合(composite)

适配器(adapter) 可以写为 多种信息类型之间的转换 的组件：选定一个内部的统一的格式，做例如 setIn() 和 setOut() 的方法。

如选定 jsonObj (比如 `nlohmann::json`) 作为内部的中间统一格式，就可以有 `jsonObj.setIn( jsonStr | jsonObj | xmlStr | xmlObj | yamlStr | yamlObj ... )`，以及 `jsonObj.setOut( ... )`。还可以参考 pcl 库的 各种滤波器 的使用，其中就有 `setInput()` 方法 并 重载了多种输入。



上下二者类似 ↑ ↓



桥接(bridge) 可以作为 多对多的控制或调用 的模块（模块为比组件高一个级别的层级，包括多个组件构成） 的结构：上层有多种对外接口功能，下层也有多种平台或者其它情况的各种适配，那种就可以设计一个中间层，只保留少量的、通用的接口。



类似于 ↓



组合(composite) 可以用于 信息结构呈现为树状或网状的 信息存储：将每个信息节点，用 多叉树 或者 网 的数据结构，组合到一起，再添加各种处理操作。




### 装饰器(decorator) & 外观(facade) & 代理(proxy)

这几个类似 wrap 封装一层 的结构 或 方法：比如现在有 三种 三方组件库 A、B 和 C，他们具体接口不一样但是功能行为类似，比如多种社交媒体平台接口，均有发帖和获取贴等，现在要写个上层使用统一的结构对其操作，就可以加一个 wrap 包装/封装一层，先来个比如 WrapBasic 的抽象类定义通用的必要的接口，再写 AWrap 类继承 WrapBasic 并实现 特定接口 来操作 A 库的接口，其它 B 和 C 同理。现在就有了 AWrap、BWrap 和 CWrap 三种 接口统一的 类 可供操作 三种库。



---

## 行为模式



### 行为链条(chain) & 迭代器(iterator)

行为链条(chain)：用于链式的处理逻辑，比如要进行一系列有先后的检查步骤，并要方便的可以在中间增减检查步骤：使用链表结构存储检查函数或者检查抽象类智能指针等，核心就是使用链表的数据结构，如 `std::list`。

对于链条数据结构的遍历，就需要迭代器如下。



迭代器(iterator)：搞一个对某个数据结构的指定迭代/遍历方法的迭代器类：如对于 二叉树 或 网 的数据结构有 深度优先 和 广度优先 等遍历方法。

自己实现的数据结构，需要实现基本的方法：增删改查；我再加四个：判排复遍——判空、排序（对于哈希表结构则没有）、复位（清空）和遍历。

对于遍历，可以两种：

1. 提供遍历的方法比如 `traverse(const TraverseFunction& traverse_func)`，传入一个遍历的回调函数，如下。还可以增加遍历方法指定的形参。

   ```c++
   template <typename Key, typename Value>
   void GeneralContainer<Key, Value>::traverse(const TraverseFunction& traverse_func) const
   {
       if(!traverse_func) {
           return;
       }
       std::shared_lock<std::shared_mutex> lock(mMutex);
       for (const auto& it : mList) { // 正序遍历
           traverse_func(it);
       }
   }
   ```

2. 提供这里所说的迭代器类，不同的迭代器类代表对这个数据结构的不同的遍历方法。比如 std 标准库 容器的:

   ```c++
   std::vector<int> myVector = {1, 2, 3, 4, 5};
   auto forwardIter = myVector.begin();    // forwardIter 指向 第一个 元素，forwardIter++ 则移动到第二个元素。
   auto backwardIter = myVector.rbegin();  // backwardIter 指向 最后一个 元素，backwardIter++ 则移动到倒数第二个元素。
   ```



### 中介/中央调度(mediator) & 命令(command)

中介/中央调度(mediator)：多个地方的组件请求执行动作，如果其之间有冲突，比如多个 app 要往 状态栏 弹带优先级的信息，不要各自都直接弹出，因为需要优先级高的始终在最上，因此需要一个中介或者中央调度的组件或模块，多个地方的 app 统一往这个 中介 请求弹信息，由 中介 选择 往信息栏 插入 的位置并插入、或者检查黑名单并忽略等等。

还有 GUI 程序中的弹窗场景，有的界面可以弹窗，有的界面不允许弹窗，等等还有其它设计情况，因此需要一个中介去统一接受弹窗请求并处理。



命令(command)：思想是，打包一个执行动作以及其传入参数：一个执行动作，如 GUI 程序中 用户点击一个按键，索要执行的一系列程序，封装为一个函数（多种按键有枚举等关系，或者按键为登录等需要传入参数的），需要执行动作时候，打包函数和函数实参 如用 `std::bind()`，放到一个队列中去执行。可以参考 线程池 [progschj/ThreadPool: A simple C++11 Thread Pool implementation](https://github.com/progschj/ThreadPool) 的使用方法。

如上面的中介就需要类似 命令 的方式，设置接口，处理来自其它组件的 "命令"。



### 备忘录(memento) & 访问者(visitor)

备忘录(memento)：针对需要给组件当前状态整一个快照、用于存留到历史记录中用于后面可能的再现/回放等场景，则给每个组件添加一个 比如 save() 或者 snapshot() 的方法，方法返回 保存了这个组件所有当前信息的（足够回放的）通用 Memento 类或者这个组件的一份克隆，有一个 history 类进行保存并在每次进行快照的时候增长。

参考 [C++ 备忘录模式讲解和代码示例](https://refactoringguru.cn/design-patterns/memento/cpp/example)。



访问者(visitor)：给需要被访问的类添加一个类似于 Accept(Visitor* visitor) 的函数，传入 visitor 后调用其 visitor->VisitConcreteComponentA(this);，在 VisitConcreteComponentA() 内部访问 当前类实例。

参考 [C++ 访问者模式讲解和代码示例](https://refactoringguru.cn/design-patterns/visitor/cpp/example)。



### 观察者(observer) / 发布-订阅(publisher-subscribers)

观察者订阅发布者，发布者执行发布操作（可带参数），即所有订阅这个发布者的观察者的订阅回调函数都会被执行。

发布-订阅 模式的 C++ 库，如：libsigcplusplus、KDBindings、等 信号槽 类型库，以及 dds 进程间通讯库等。



### 状态设计(state) / 有限状态机(FSM)

将组件或模块或设备的功能执行划分为一些状态以及状态之间的转移条件，画出状态转移图，即设计为 有限状态机 FSM，进行业务的编程建模。

简单的可以为 switch-case 语句进行，复杂的、功能多的可以上库，如以下库等：

- StateMachine [endurodave/StateMachine: State Machine Design in C++](https://github.com/endurodave/StateMachine)，C++，编程风格为 定义 事件 event 下 所有 状态 的 行为，以及状态进入和退出的行为等。
- UML State Machine in C [kiishor/UML-State-Machine-in-C: A minimalist UML State machine framework for finite state machine and hierarchical state machine in C](https://github.com/kiishor/UML-State-Machine-in-C)，C 语言，轻量级（可用于 mcu），表格化构建状态机，支持层级状态机。
- stateMachine [misje/stateMachine: A feature-rich, yet simple finite state machine (FSM) implementation in C](https://github.com/misje/stateMachine)，C 语言，简易简陋超轻量状态机，可用于 mcu。



FPGA 的 IP核 设计中常用 FSM 概念进行建模，有几种不同的写法，Verilog 编码 的例子可见 [HDL-FPGA-study-and-norms/FPGA学习和规范 的参考源码/具体模块/fsm 一段和三段状态机例子 at main · Staok/HDL-FPGA-study-and-norms](https://github.com/Staok/HDL-FPGA-study-and-norms/tree/main/FPGA学习和规范 的参考源码/具体模块/fsm 一段和三段状态机例子)。



### 策略(strategy) & 模板方法(template-method) / 类多态

策略(strategy)：针对需要对于一定的数据集，使用不同的策略来获取不同的结果。策略可以使用基类和衍生类的多态来实现，这样，创建不同种类的策略类实例并给到执行，就是使用了不同的策略。

参考 [C++ 策略模式讲解和代码示例](https://refactoringguru.cn/design-patterns/strategy/cpp/example)。



模板方法(template-method)：基类定义执行操作（里面包含多种子操作以及特定顺序）的一个（纯）虚函数，并定义一些子操作（（纯）虚）函数，继承这个基类的多个衍生类中，使用不同的实现重写这些执行操作的函数（不同的子操作、顺序等，以及不同的操作实现），使用类多态，做到创建不同的类实例，用于对数据执行不同的策略操作。

参考 [C++ 模板方法模式讲解和代码示例](https://refactoringguru.cn/design-patterns/template-method/cpp/example)。
