# 编程经验、调试、性能和内存检查工具集合


# 编程经验、调试、性能和内存检查工具集合

程序调试、在检测工具手段上对程序评估和优化 的 综合。

尚有 一些 标记了 TODO 的地方 有待施工。没有三头六臂，很多资料 手头和脑里 都有 只是尚未没有整理出来。



> 虽抱文章，开口谁亲。且陶陶、乐尽天真。几时归去，作个闲人。对一张琴，一壶酒，一溪云。



# 编程经验

这里只总结一些精华的点、易忘的点，高频出问题的点。



顶层指导：

- 多看一些 最佳实践 的 文章 和 工程 来对自己进行提高。
- 基础语法和例子，实践的时候可举一反三使用。
- 写东西时候先多思考架构。不必一上来就写 等 情况的出现，减少后面 debug 和 重构的时间。

设计模式相关综合 [Staok/C-Cpp-design-patterns: C/C++设计模式相关优秀资料集子 (github.com)](https://github.com/Staok/C-Cpp-design-patterns)。



- 可以设计 和 使用一些自动化工具来帮助完成 重复性的操作（也避免人工操作的可能的失误，所以工具也要写的健壮一些，识别和处理一些常会出现的错误），或者 用来检查 容易出错的地方，借由机器来给脑卸去些负担。



易错注意：p.s 这些地方易错且无法静态检查出，只能运行起来碰到，目前还没有好的静态工具来检出，所以靠人来保证程序的健壮性，是良好的 程序框架设计 和 一些规则（比如不写主动抛异常）、规范 的 教育、培训、落实 来。

- 一个资源可能多个线程使用，必加锁（单纯的互斥量，或者读写锁 等，选择适当的锁类型）。

- 使用指针之前 若有必要 则 必 检查 判空（包括std::shared_ptr等类型的指针）。释放指针后必置其为 nullptr / null。动态创建的资源，尽量使用智能指针来管理。

- 会抛异常的 API 若有必要 / 尽量 加异常捕获。

  使用系统调用、库函数等，查看文档确定其是否会抛异常，处理其执行错误的情况。自己写程序可以尽量不用主动抛异常，运行出错当下解决（视情况严重性，是直接终止程序（后面依靠比较完备的测试来逐渐收敛程序 bug 来提高程序健壮性），还是及时在当下来处理错误（如给个默认值等））。

  调用有可能抛出异常的API（一般是库的），都要加 try cache 来打印 log 并处理现场。自己写的就不要抛异常了，只接不抛，否则代码规模一大不好控制。



良好实践经验 / 惯例写法：

- 每个项目最好都有统一的 .clang_format 文件，时常 format 下。有 clangd 配置文件 也好。

- [chengxumiaodaren/cpp-learning (github.com)](https://github.com/chengxumiaodaren/cpp-learning)。

- [你最喜欢的c++编程风格惯用法是什么?_51CTO博客_c++编程惯用法](https://blog.51cto.com/u_12205414/3251768)。其中的一些精华总结到下面。

  - 

- 基类/抽象类、派生类 的结构设计尽量按照实际情况，尽量分层次处理，基类/抽象类中列好公共 变量 和 接口/虚函数/纯虚函数 等。

- 创建和销毁资源务必成对去写。创建资源（类、结构体、数组等）用于承接的指针尽量使用 std::shared_ptr / std::unique_ptr 这种（尤其是 在异常等情况发生时，资源可以自动释放）。

- 类的析构，实例的删除等等的函数，尽量做到可重复多次调用（因为外部有可能重复调），可用 mIsInit 变量来记录这个类是否初始化成功，类的各个方法开头先判断一下这个。delete 前 先 判断指针 是否不为空，delete 后指针再置空（nullptr）。

- 推荐 多做/多用 RAII（利用对象生命周期管理资源）风格编码。

  如 使用 智能指针。

- 常用大括号控制生命周期，能提前结束的就可以提前结束。



- 一些表达式，使用 constexpr 替代 宏，且多用 编译期计算。宏有全局作用域，项目一大易混乱。
- 可以更多的使用模板元编程。



- 单例类只用 .h 文件里面 放一个 `extern class classType Global<name>Inst;` 这种方式（在 .cpp 里面去声明 `calss classType Global<name>Inst;`），之后全局调用 `Global<name>Inst` 即可。



细节写法：

- [编译优化 - OI Wiki (oi-wiki.org)](https://oi-wiki.org/lang/optimizations/)。
- 函数形参超过三个的，可考虑 使用 struct 打包（后续补充形参也可直接修改这个结构体，比较方便维护），传递参数尽量不用 std::array, std::pair, std::tuple 等这种破坏可动性的东西。
- 打印 log 的一些规范，有用的 log 优化常用方法：
  - 降频；比较前后数据，有变化时再打印；只打印 error 错误信息，以及关键 info 信息。
  - 比较稳定且不重要的模块尽可能精简，出了问题再加 log 也来的及。
  - log 描述尽量简化，单词用缩写，函数名不用打全。



TODO：参考 木须 的 编码规范的文档，补充到这里。



# 环境搭建 / 最佳实践

这里面也是对本文下面各种工具的整理。

TODO 引用 自己的 cmake模板工程仓库目录



# GDB / binutils / GCC options

## GDB / GDBServer

基本步骤 [Debugging With gdb Mini-Tutorial | hacking C++ (hackingcpp.com)](https://hackingcpp.com/cpp/tools/gdb_intro.html)。

更丰富各种资料 [ARM-Linux-Study/【1 GCC & GDB & GDBServer】 at main · Staok/ARM-Linux-Study (github.com)](https://github.com/Staok/ARM-Linux-Study/tree/main/%E3%80%901%20GCC%20%26%20GDB%20%26%20GDBServer%E3%80%91)。



对于 gdb 工具，若是单步调试等这种，一般有 VsCode、VS 这种界面工具，对于 GDBServer 则需要 一些单步调试命令。而对于 linux 产生的 coredump，更多是在使用 gdb 的各种信息查看命令。



GDB 常用命令总结：

`bt` 显示调用栈

`f <num>` 设置当前处于哪一层栈，再用 `info <xxx>` 的命令看看信息，常用的：`info locals`、`info args`、`info frame`，然后可以用 print 打印变量、结构体、指针等等

`thread apply all bt` 显示所有线程在干什么

`thread <thread-id>` 跳转到对应的线程号，再用 bt 查看调用栈，同上



gdb 查看 coredump `gdb {binary} {coredump_file}`。指定 sysroot 目录，在 gdb 后添加 `-ex "set sysroot $SYSROOT_PATH"`。

Linux 程序调试，产生 coredump 方法

[浅谈 Linux 中的 core dump 分析方法-CSDN博客](https://blog.csdn.net/qq_42417071/article/details/140147831)

[Linux内核调试方法总结之coredump - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/514516021)

需要编译程序 添加调试 -g，将符号表导出到 bin，可供 gdb 查询；可以开发阶段都是用这种编译，最后 release 的时候，可以稍微使用优化比如 -O2，然后去掉 -g 或者 使用 gcc 的 strip 工具给 bin 去掉 符号表。



程序编译时候 -g 会带上函数等符号，使用以上工具可以根据内存地址反查出函数名，若只有内存地址，可以用 gdb 工具

[c++ - How to use GDB to find what function a memory address corresponds to - Stack Overflow](https://stackoverflow.com/questions/7639309/how-to-use-gdb-to-find-what-function-a-memory-address-corresponds-to)——在 gdb 工具里面使用 info 系列命令来查看



## binutils 工具集

binutils 工具集介绍和使用 [GNU开发工具——GNU Binutils快速入门_51CTO博客_GNU Binutils](https://blog.51cto.com/quantfabric/2515980)。

包括 addr2line、ar、gprof、nm、objcopy、objdump、ranlib、size、strings、strip。



addr2line 使用详解

[在Linux中使用addr2line的参数有哪些 - 问答 - 亿速云 (yisu.com)](https://www.yisu.com/ask/96420422.html)

[addr2line使用详解_addr2line命令用法-CSDN博客](https://blog.csdn.net/zhangqi306891687/article/details/141498310)

[调试厉器addr2line-CSDN博客](https://blog.csdn.net/mingtiannihaoabc/article/details/131263823) 程序地址、库方法地址、内核模块的地址

一般用法 `addr2line -e <bin> -Cfp <addr(0xXXXX)>`



## GCC 实用选项



gcc 选项-finstrument-functions实现函数调用栈追踪

[gcc 选项-finstrument-functions实现函数调用栈追踪-CSDN博客](https://blog.csdn.net/m0_61549061/article/details/139065079)。



gcc 扩展关键字，可多了解和积累

`__attribute__`：

[__attribute__ 的详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/c8bea3807527)

[GNU C中不为人知的特色：__attribute__机制-CSDN博客](https://blog.csdn.net/juana1/article/details/6849120)

[__attribute__机制介绍-CSDN博客](https://blog.csdn.net/ithomer/article/details/6566739)

[__attribute__机制介绍_使用-finstrument-CSDN博客](https://blog.csdn.net/bytxl/article/details/7523472)



# 性能 / 内存相关工具

参考：会列出很多工具，选择自己趁手的即可。

- [一般Linux性能调优都用什么工具？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/448362493/answer/1770329163)。
- [C/C++ 编程有哪些值得推荐的工具？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/23357089/answer/1992218543)。
- [C++ 怎么检测内存泄露，怎么定位内存泄露？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/63946754/answer/1981098265)。
- [大型c++项目在linux下如何调试? - 知乎 (zhihu.com)](https://www.zhihu.com/question/26905808/answer/1971302757)。



## Linux 系统常用工具

> **网络I/O**：dstat、**tcpdump**（推荐）、sar
>
> **磁盘I/O**：**iostat**（推荐）、dstat、sar
>
> **文件系统空间**：**df**、du
>
> **内存容量**：free、**vmstat**（推荐）、sar
>
> **进程内存分布**：**pmap**
>
> **CPU负载**：uptime、**top**
>
> **CPU使用率**：**pidstat**（推荐）、vmstat、mpstat、top、sar、time
>
> **系统调用追踪**：**strace**（推荐）
>
> **网络吞吐量**：**iftop**、nethogs、sar
>
> **网络延迟**：**ping**
>
> **上下文切换**：**pidstat**（推荐）、vmstat、perf
>
> **软中断/硬中断**：**/proc/softirqs**、**/proc/interrupts**



各种工具用处可视化的各种图

[Linux Performance (brendangregg.com)](https://www.brendangregg.com/linuxperf.html)。



## 内存统计基本命令

[Linux 下查看内存使用情况方法总结 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/555018970)。

[linux进程VSZ（Virtual Memory Size 虚拟内存）RSS（Resident Set Size 驻留集大小，实际占用的物理内存）PSS、USS、ANON、RESVIRTDirty-CSDN博客](https://blog.csdn.net/Dontla/article/details/123131147)。



- procrank 查看各进程的 VSS RSS PSS USS 内存占用情况

  VSS RSS PSS USS 内存 介绍 [VSS/RSS/PSS/USS - 简书 (jianshu.com)](https://www.jianshu.com/p/995692aa0100)

  `procrank -u -R`

  `watch -n 1 procrank -u`（循环执行）

  ```bash
  watch -n 1 "procrank -u | grep <process_name>"
  ```

- `ps aux --sort -rss`

- `free -h`	对 /proc/meminfo 收集到的信息的一个概述

  进程的内存使用信息也可以通过 `/proc/<pid>/statm` 和 `/proc/<pid>/status` 来查看，但比较抽象，有具体的格式

- pmap 命令

  [如何在 Linux 上使用 pmap 命令_linux pmap使用-CSDN博客](https://blog.csdn.net/wlcs_6305/article/details/124434626)

  [Linux内存管理 -- smaps讲解-CSDN博客](https://blog.csdn.net/qq_34934140/article/details/121120348)

  [anon] 内存段 [系统调用mmap的内核实现分析-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1459253)

  - 该内存段就是操作系统为mmap系统调用新分配出来的区域。

  - frame buffer 算，其它的还有可能是 别的系统调用 通过 mmap 读写 驱动文件 产生的

  `pmap -p -x <pid>` 查看某一个进程的内存占用各个文件的信息，`-x` 以及 `-X` 和 `-XX` 选项增加显示信息

  `pmap -p -x <pid> > /tmp/xxx` 写入到文件，再取出到 pc 上，导入到 excel，排序查看，或者用别的方法排下序来看。

  循环监视：

  ```bash
  watch -n 1 "pmap -p -X $(pidof <procss_name>) | grep heap"
  ```



## 动态检查 *



几个主要工具对比

> | 工具       | 使用命令                                                     | 是否需要重新编译 | Profiling速度 | 是否支持多线程热点分析 | 是否支持链接库热点分析 |
> | ---------- | ------------------------------------------------------------ | ---------------- | ------------- | ---------------------- | ---------------------- |
> | gprof      | ./test; gprof ./test ./gmon.out                              | **是**           | 慢            | **否**                 | **否**                 |
> | valgrind   | Valgrind --tool=callgrind ./test                             | 否               | **非常慢**    | 是                     | 是                     |
> | gperftools | LD_PRELOAD=/usr/lib/libprofiler.so CPUPROFILE=./test.prof ./test | **否**           | 快            | 是                     | 是                     |



### valgrind

拖慢程序比较严重，不推荐使用了其实。后面的 prof 工具类 和 AddressSanitizer 推荐使用。

可参考：

[valgrind Introduction | hacking C++ (hackingcpp.com)](https://hackingcpp.com/cpp/tools/valgrind.html)。



一些使用和调试经验

可以查看程序的堆内存分配情况，包括哪些函数分配了大块内存。

https://www.cnblogs.com/jj-Must-be-sucessful/p/17005792.html    编译和添加环境变量

https://baijiahao.baidu.com/s?id=1652356863601374476&wfr=spider&for=pc    检测内存泄漏

https://blog.csdn.net/asitMJ/article/details/135371794 linux多线程互斥锁程序卡死排查



qt creator 中自带：（在Linux中）需要先安装 Valgrind 并添加环境变量，并测试能用，然后在 qt creator 中实用如下功能启用监控和生成结果（火焰图等）`Valgrind Memory Analyzer (External Application)` 和 `Valgrind Function Profiler (External Application)`。

[QT-Valgrind内存分析_我不是萧海哇的技术博客_51CTO博客](https://blog.51cto.com/xiaohaiwa/5380249)，qt（linux pc）中执行



### gperftools

> - gmc: gperf memory check, 内存检查（泄漏，错误等）内存泄漏检测工具
> - gmp: gperf memory profile, 内存性能分析（哪个函数内存分配多）内存占用分析。内存申请记录（定位到函数）。
> - gcp: gperf cpu profile, CPU性能分析（函数消耗CPU多）能够通过统计一定时间内各个功能单元（线程、函数等）的执行时间并给出其占用比例。cpu（函数调用 / 火焰图）。

> 相比与其他性能分析工具，**gperftools有Profiling速度快，灵活性较高的优点。**

但是配置起来需要安装一堆东西，需要专门用时间进行 学习、细细配置和使用起来。

> Gperftools 在 Windows 上提供了 tcmalloc_minimal 的支持，这是一个内存分配器，可以在 Windows 上使用。然而，一些依赖于 Linux 特有功能（如signal.h）的功能（如 ProfilerStart() 和 ProfilerStop() 函数）在 Windows 上不可用‌



基本使用：

1、以链接动态库的形式链接进程序。

2、也可以不重新编译程序，将库放到机器上，使用 LD_PRELOAD 环境变量指定加载库。

让程序启用，然后 pprof 打印内存申请情况。



使用上，建议不要自己编译 gperftools 生成库来给自己 程序 链接 和 编译，坑很多（大多数人生苦短，若你人生自由有时间，可以多研究多鼓捣），所以建议尽量使用编译好的lib 或者 现成的 package 来用（本文作者截止到 23.10（自己编译 gperftools 源码 然后链接成功，但是 bin 没有跑起来..） 还没有这么做过），推荐探索下（本文作者目前还没有这方面需求所以就没有花时间再深入研究，若日后正式再去用，则会记录成功的普适的步骤并补充到这里）。



参考：

[gperftools/gperftools: Main gperftools repository (github.com)](https://github.com/gperftools/gperftools)。

官方文档：

> ```
> TCMALLOC
> --------
> Just link in -ltcmalloc or -ltcmalloc_minimal to get the advantages of
> tcmalloc -- a replacement for malloc and new.  See below for some
> environment variables you can use with tcmalloc, as well.
> 
> tcmalloc functionality is available on all systems we've tested; see
> INSTALL for more details.  See README_windows.txt for instructions on
> using tcmalloc on Windows.
> 
> when compiling.  gcc makes some optimizations assuming it is using its
> own, built-in malloc; that assumption obviously isn't true with
> tcmalloc.  In practice, we haven't seen any problems with this, but
> the expected risk is highest for users who register their own malloc
> hooks with tcmalloc (using gperftools/malloc_hook.h).  The risk is
> lowest for folks who use tcmalloc_minimal (or, of course, who pass in
> the above flags :-) ).
> 
> 
> HEAP PROFILER
> -------------
> See docs/heapprofile.html for information about how to use tcmalloc's
> heap profiler and analyze its output.
> 
> As a quick-start, do the following after installing this package:
> 
> 1) Link your executable with -ltcmalloc
> 2) Run your executable with the HEAPPROFILE environment var set:
>      $ HEAPPROFILE=/tmp/heapprof <path/to/binary> [binary args]
> 3) Run pprof to analyze the heap usage
>      $ pprof <path/to/binary> /tmp/heapprof.0045.heap  # run 'ls' to see options
>      $ pprof --gv <path/to/binary> /tmp/heapprof.0045.heap
> 
> You can also use LD_PRELOAD to heap-profile an executable that you
> didn't compile.
> 
> There are other environment variables, besides HEAPPROFILE, you can
> set to adjust the heap-profiler behavior; c.f. "ENVIRONMENT VARIABLES"
> below.
> 
> The heap profiler is available on all unix-based systems we've tested;
> see INSTALL for more details.  It is not currently available on Windows.
> 
> 
> CPU PROFILER
> ------------
> See docs/cpuprofile.html for information about how to use the CPU
> profiler and analyze its output.
> 
> As a quick-start, do the following after installing this package:
> 
> 1) Link your executable with -lprofiler
> 2) Run your executable with the CPUPROFILE environment var set:
>      $ CPUPROFILE=/tmp/prof.out <path/to/binary> [binary args]
> 3) Run pprof to analyze the CPU usage
>      $ pprof <path/to/binary> /tmp/prof.out      # -pg-like text output
>      $ pprof --gv <path/to/binary> /tmp/prof.out # really cool graphical output
> 
> There are other environment variables, besides CPUPROFILE, you can set
> to adjust the cpu-profiler behavior; cf "ENVIRONMENT VARIABLES" below.
> 
> The CPU profiler is available on all unix-based systems we've tested;
> see INSTALL for more details.  It is not currently available on Windows.
> 
> NOTE: CPU profiling doesn't work after fork (unless you immediately
>       do an exec()-like call afterwards).  Furthermore, if you do
>       fork, and the child calls exit(), it may corrupt the profile
>       data.  You can use _exit() to work around this.  We hope to have
>       a fix for both problems in the next release of perftools
>       (hopefully perftools 1.2).
> 
> 
> EVERYTHING IN ONE
> -----------------
> If you want the CPU profiler, heap profiler, and heap leak-checker to
> all be available for your application, you can do:
>    gcc -o myapp ... -lprofiler -ltcmalloc
> 
> However, if you have a reason to use the static versions of the
> library, this two-library linking won't work:
>    gcc -o myapp ... /usr/lib/libprofiler.a /usr/lib/libtcmalloc.a  # errors!
> 
> Instead, use the special libtcmalloc_and_profiler library, which we
> make for just this purpose:
>    gcc -o myapp ... /usr/lib/libtcmalloc_and_profiler.a
> ```

可视化显示结果数据使用 pprof，[google/pprof: pprof is a tool for visualization and analysis of profiling data (github.com)](https://github.com/google/pprof)。

> pprof is a tool for visualization and analysis of profiling data



[GPERF 内存和性能分析 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/608605973)。

[你了解过Gperftools性能分析神器吗？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/678172638)。

[gperftools的安装使用说明_gperftools安装-CSDN博客](https://blog.csdn.net/fpcc/article/details/136573180)。



[使用heap profiler进行内存占用分析 - 溟漓 - 博客园 (cnblogs.com)](https://www.cnblogs.com/minglee/p/10124174.html) 安装和使用

[gperftools快速上手教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/623443812)。

[使用google perf工具来排查堆外内存占用 | KL's blog (qsli.github.io)](https://qsli.github.io/2017/12/02/google-perf-tools/) 具体使用

[性能测试工具Google perftools（简称gperftool)配置及使用_google perftools使用-CSDN博客](https://blog.csdn.net/m0_50179075/article/details/125141931) -lprofiler -lunwind

[gperftools安装与使用-CSDN博客](https://blog.csdn.net/qq_44407144/article/details/131313020) HEAPCHECK=模式



有许多使用上的选项，可以详细参考 官方文档，总之功能是相对丰富的。



### gprof / gcc -pg

> 一种用于分析程序性能的工具，它能够生成函数级别的性能分析报告，帮助开发人员找出程序中的瓶颈和性能问题。`gprof` 通常与 GNU 编译器集合中的 `gcc` 配合使用，它通过在程序中插入一些特殊的代码来收集运行时的函数调用信息，然后生成性能分析报告。

> gprof可以用来分析系统在运行时各函数调用的次数，耗时等情况，可以方便地帮助我们定位系统的瓶颈，同时也能让我们知道对程序的那个位置就行优化能够带来尽可能大的性能提升。gprof 优化尤其适用于CPU、内存密集性的应用模块。

> -p / -pg： gcc 中的一个编译选项，用于在生成的可执行文件中插入性能分析代码，以便进行性能分析和 profiling（性能剖析）。以帮助开发人员了解程序的运行时间分布、函数调用关系以及性能瓶颈，从而指导优化工作。需要注意的是，由于插入了额外的代码，使用 -pg 选项可能会稍微影响程序的执行速度，因此在进行性能分析时需要权衡是否使用该选项。

不适用于 多线程 程序 分析（默认只记录主线程，分析多线程需要一些方法来做到。个人觉得，与其这折腾这个，不如直接用 gperftools 等来做分析） 和 动态链接库 的 分析。

gprof 可以统计出各个函数的调用次数、时间、以及函数调用图。

在编译和链接程序的时候，使用 `-pg` 选项；执行程序；再 `gprof <app> <运行结束后生成的分析结果文件>`。

> 1. gcc -pg 编译程序
> 2. 运行程序，程序退出时生成 gmon.out
> 3. gprof ./prog gmon.out -b 查看输出

> 可通过`gprof -h`命令查看可用参数。



[性能优化之性能分析工具gprof - 懒人李冰 (lazybing.github.io)](http://lazybing.github.io/blog/2019/04/13/profiler-gprof/)。

> 生成的分析文件 analysis.txt 中有两种形式的分析数据。
>
> Flat Profile 和 Call Graph。都是用于表示 每个函数的 占用时间 和 调用次数等。



[程序性能分析工具—gprof-CSDN博客](https://blog.csdn.net/tongxin1101124/article/details/115248122)。

> 由于结果report.txt分析不太直观，可以借助gprof2dot.py与dot工具生成函数调用图



[gprof性能分析工具详解-CSDN博客](https://blog.csdn.net/mozun1/article/details/58011427)。

> 注意事项
>
> - 程序如果不是从main return或exit()退出，则可能不生成gmon.out。
> - 程序如果崩溃，可能不生成gmon.out。
> - 测试发现在虚拟机上运行，可能不生成gmon.out。
> - 一定不能捕获、忽略SIGPROF信号。man手册对SIGPROF的解释是：profiling timer expired. 如果忽略这个信号，gprof的输出则是：Each sample counts as 0.01 seconds. no time accumulated。
> - 如果程序运行时间非常短，则gprof可能无效。因为受到启动、初始化、退出等函数运行时间的影响。
> - 程序忽略SIGPROF信号！



### perf

命令行工具，有很多子功能，包含 函数调用 / 火焰图、内存申请记录（定位到函数）、内存泄漏检测 工具。

可以使用命令 生成 text、pdf（火焰图、函数调用关系图） 等形式的展示。



[系统性能分析工具--Perf - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/614212908) 基本使用，基本选项

[包罗万象-perf命令介绍 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/621893549) 各个命令介绍

生成的 perf.data 可以放到这个可视化网站上看 [speedscope](https://www.speedscope.app/)



perf 的一个可视化工具，也是一个 perf 的 UI 工具（推荐）：

KDAB 的 hotspot，linux（带图形界面的）平台运行 .appImage 文件，或者在如 ubuntu 平台安装 hotspot 软件即可用。具体参考官方文档。[KDAB/hotspot: The Linux perf GUI for performance analysis. (github.com)](https://github.com/KDAB/hotspot)。

> The main feature of Hotspot is the graphical visualization of a `perf.data` file.



### 自实现内存泄露检测工具原理

对 malloc / free 或 new / delete 做 插桩函数 或者 对其重载 来实现。

源自 [C++不用工具，如何检测内存泄漏？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/29859828/answer/1798470821)。



### ASAN / Address Sanitizer

[C++ ASAN (Address Sanitizer) Introduction | hacking C++ (hackingcpp.com)](https://hackingcpp.com/cpp/tools/asan.html)。

> - detects memory corruption bugs
>   - memory leaks
>   - access to already freed memory
>   - access to incorrect stack areas
>   - ...
> - instruments your code with additional instructions
>   - roughly 70% runtime increase
>   - roughly 3-fold increase in memory usage

[内存检测工具 AddressSanitizer - 简书 (jianshu.com)](https://www.jianshu.com/p/d80db380e295)。

> AddressSanitizer 是一个内存检测工具。支持GCC 4.8 及以上。在编译时添加`-fsanitize=address`选项，如果为了得到更全面的信息可以用`-fno-omit-frame-pointer`。

> 该工具为gcc自带，4.8以上版本都可以使用，支持Linux、OS、Android等多种平台，不止可以检测内存泄漏，它其实是一个内存错误检测工具，可以检测的问题有：
>
> - 内存泄漏
> - 堆栈和全局内存越界访问
> - free后继续使用
> - 局部内存被外层使用
> - Initialization order bugs

具体文档 [AddressSanitizer · google/sanitizers Wiki (github.com)](https://github.com/google/sanitizers/wiki/AddressSanitizer)。



更多详情：

- [内存错误检测工具-AddressSanitizer（ASAN）_asan安装-CSDN博客](https://blog.csdn.net/qq_15437629/article/details/114440930)。

  > Valgrind 其会极大的降低程序运行速度，大约降低10倍，而 AddressSanitizer 大约只降低2倍！

- [深入理解Asan：内存错误检测工具与实践-CSDN博客](https://blog.csdn.net/weixin_42136255/article/details/133815129)。

- [关于 ASAN - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/512578904)。

- [ASAN 问题总结-CSDN博客](https://blog.csdn.net/weixin_31260305/article/details/133288437)。

- [KASan介绍-CSDN博客](https://blog.csdn.net/weixin_42136255/article/details/133814026)。

- [C++(Qt)软件调试---GCC编译参数学习-程序检测（13）_gcc 编译-fsanitize=address-CSDN博客](https://blog.csdn.net/qq_43627907/article/details/132890999)。

  > AddressSanitizer（ASan）是一种用于检测和调试内存错误的工具。它是由Google开发的，并内置于GNU编译器套件（GCC）和LLVM编译器中。
  >
  > 释放后使用（野指针）
  >
  > 堆缓冲区溢出
  >
  > 栈缓冲区溢出
  >
  > 全局缓冲区溢出
  >
  > 返回局部堆区地址后使用（经过测试没检测出来）
  >
  > 作用域外使用栈内存
  >
  > 初始化顺序错误（经过测试未检测出来）
  >
  > 内存泄漏



使用：

首先说结论：对于 linux，则 gcc 和 clang 均可（注意版本）。对于 win，则 则 mingw-w64 没有带 ASAN 库，所以 win 上只能用 clang（而且还是特定的出包，比如 MSYS2 的 clang 包可以用 ASAN） 来使用 ASAN。



先碎碎念一波，各种查找信息和试验搞了半天，这里记录下：mingw 版本的 gcc 没有集成 ASAN 这个库，[c++ - MinGW-w64's gcc and Address Sanitizer - Stack Overflow](https://stackoverflow.com/questions/31144000/mingw-w64s-gcc-and-address-sanitizer)，并且 mingw 官网也说 win 上没有支持 ASAN [Contribute - MinGW-w64](https://www.mingw-w64.org/contribute/)。而 MSYS2 （使用其里面的 clang 工具链）是有的，如果你想使用 MSYS2 就可以配置环境直接用其工具链上手。要是非要用 mingw 环境，则要试着 自己编译 ASAN 库来使用，[自己动手编译asan库 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/71564723)，或者自己编 asan 源码 [AddressSanitizerHowToBuild · google/sanitizers Wiki (github.com)](https://github.com/google/sanitizers/wiki/AddressSanitizerHowToBuild)，自己编这个，这些我都暂没有在 win 上试成功，不推荐轻易尝试，MSYS2 和 Cygwin 等已经提供了比较好用的环境，自己编译的话用于研究和学习可以，但这个学习的路径比较陡峭所以不推荐轻易尝试，学习途径有很多（自己搭建开发环境，可以参考 TODO 放自己 cmake 模板工程 仓库），凡事讲究成本。

clang 在 win 上是支持 ASAN 的 [AddressSanitizerWindowsPort · google/sanitizers Wiki (github.com)](https://github.com/google/sanitizers/wiki/AddressSanitizerWindowsPort)。clang 官方也说 AddressSanitizer 支持 win 但是 支持不太好 [AddressSanitizer — Clang 20.0.0git documentation (llvm.org)](https://clang.llvm.org/docs/AddressSanitizer.html#more-information)。自己本地 win 上这种情况就可以换用 clang 编一编来跑一跑（编出来也是用于测试的，而非正式环境用），又发现，还需要依赖 compiler-rt 这个工具。这个 compiler-rt 可以用 MSYS2 安装。。折腾了一圈，还是拥抱 MSYS2 吧，用这个来管理所有编译相关工具链吧。。话又说回来，AddressSanitizer 在 win 上支持并不好，所以 win 上还是换用其它工具吧 比如 DrMemory（专用于 win 的），在 linux 下就可以愉快的使用 AddressSanitizer（gcc 和 clang 均可）。 

win 上使用 ASAN 路径：

- MSYS2 安装指引

  [MSYS2](https://www.msys2.org/)

  [MSYS2-Installation - MSYS2](https://www.msys2.org/wiki/MSYS2-installation/)

  更新最新库，使用命令 `pacman -Syuu`

- 在 MSYS2 里的 CLANG64 环境下，执行：来安装 clang 工具链，以及 compiler-rt 库。

  ```bash
  pacman -S mingw-w64-clang-x86_64-clang
  pacman -S mingw-w64-clang-x86_64-compiler-rt
  ```

  在 MSYS2 目录下 `.\clang64\bin` 目录下可以搜索 ASAN 找到相应的库（不容易啊终于找到个win上能用的）

  使用 clang/clang++ 就可以使用 ASAN 了（在mingw-w64 工具链的目录下就没有，是 MSYS2 也没有编译这个库）

- 把 MSYS2 目录下的 `.\clang64\bin` 目录添加到环境变量。



一个例子：使用 MSYS2 目录下的 `.\clang64\bin` 里面的 clang++ 来编译下面的程序例子，就有 ASAN 的检测和打印了。后续就可以方便的集成到 cmake 等工程里面，给自己工程定义个 DEBUG 模式，在该模式下使用选项 `-fsanitize=address -fsanitize=undefined -fno-omit-frame-pointer -g` 等。

```c++
#include <cstdint>
#include <iostream>

/*
    env: 对于 linux，则 gcc 和 clang 均可，gcc 的信息如下。对于 win，则 mingw-w64 没有带 ASAN 库，所以 win 上只能用 clang 来使用 ASAN
        gcc/g++ -v:
            Target: x86_64-linux-gnu
        gcc/g++ -- version:
            gxx (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
    compile:
        clang++/g++ -fsanitize=address -fsanitize=undefined -fno-omit-frame-pointer -g -O1 ./main.cpp -o main.exe
    run:
        ./main.exe
*/

int main(int argc, char* argv[])
{
    (void)argc;
    (void)argv;

    std::cout << " --- begin" << std::endl;

    int32_t* int_ptr;
    int_ptr = new int32_t(0);
    delete int_ptr;

    // int_ptr = nullptr;

    *int_ptr = 10;

    // int32_t num = *int_ptr;
    // std::cout << " --- *int_ptr: " << *int_ptr << std::endl;

    std::cout << " --- end" << std::endl;
}
```



**Undefined Behavior Sanitizer**

[C++ UBSAN (Undefined Behavior Sanitizer) Introduction | hacking C++ (hackingcpp.com)](https://hackingcpp.com/cpp/tools/ubsan.html)。

> - detects many types of undefined behavior at runtime
>
>   - dereferencing null pointers
>   - reading from misaligned pointers
>   - integer overflow
>   - division by zero
>   - ...
>
> - instruments your code with additional instructions:
>
>   runtime increase in debug build~25%

> `-fsanitize=undefined`：使用 UndefinedBehaviorSanitizer（UBSan）工具，它可以检测代码中的未定义行为，如空指针解引用、数组越界、变量溢出、除0 等等。





> `-fsanitize=thread`：使用 ThreadSanitizer（TSan）工具，它可以检测多线程程序中的数据竞争和其他线程相关的错误。数据争用是并发系统中最常见和最难调试的错误类型之一。当两个线程同时访问同一变量并且至少有一个访问是写入时，就会发生数据争用。



### 专用于 win 的工具

这里会罗列各种可能的方法，很多本文作者并没有试过。正如 unix 一个设计哲学——"提供机制，而不是提供策略"（实际采用的策略是因场景、需求选取使用一些机制来组合使用）。



一个综合贴：[[QT编程系列-43\]: Windows + QT软件内存泄露的检测方法_qt 内存泄露排查手段-CSDN博客](https://blog.csdn.net/HiWangWenBing/article/details/133519665)。

> 2.1 内存监测工具 -Valgrind
> 2.2.1 Valgrind for Linux
> 2.2.2 Valgrind for Windows
>
> 2.2 内存监测工具-Dr. Memory
>
> 2.3 内存监测工具-Visual Leak Detector
>
> 2.4 内存监测工具-WinDbg
>
> 2.5 Windows进程内存监控工具——任务管理器
>
> 2.6 Windowx线程内存 监控工具——Windows性能工具集（Windows Performance Toolkit）——xperf 命令行工具
>
> 2.7 API函数获取线程级内存使用情况——Windows API中的GetProcessMemoryInfo函数
>
> 2.8 Windows性能监控——性能监视器



补充：

- Windows Sysinternals Suite



#### DrMemory

[Home (drmemory.org)](https://drmemory.org/)。下载后，drmemory 的 bin 目录添加环境变量，即可 shell 中运行 `drmemory -version`。

参考：

- [Running Dr. Memory (drmemory.org)](https://drmemory.org/page_running.html)。
- [Dr. Memory 使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/183b0944a092)。



本地编译，使用 MinGW，用于 DrMemory

```bash
g++ .\main.cpp -g -static-libgcc -static-libstdc++ -ggdb -o main.exe
```

执行（但是没有一次正常过，试过各种选项）

```
drmemory.exe -- .\main.exe
```



#### Visual Leak Detector

内存泄漏检测（win 上）

[内存泄露检测工具VLD(Visual Leak Detector)使用说明-CSDN博客](https://blog.csdn.net/devillixin/article/details/126196206)

[Qt / MSVC 中使用内存泄露检测工具 VLD(Visual Leak Detector)_qt内存泄漏检测工具-CSDN博客](https://blog.csdn.net/weixin_41863029/article/details/128482295)



#### WinDbg



#### Application Verifier

配置太复杂了..若长期专门开发 win 程序可以用



#### Windows Performance Toolkit



#### Windows Sysinternals Suite

[Sysinternals Suite - Sysinternals | Microsoft Learn](https://learn.microsoft.com/zh-cn/sysinternals/downloads/sysinternals-suite)。

[微软工具包Windows Sysinternals Suite简介-CSDN博客](https://blog.csdn.net/nodeman/article/details/109615209)。

[Sysinternals Suite免费的Windows系统工具集（系统管理良兵利器） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/569262316)。



#### Windows API

Windows API 中的 GetProcessMemoryInfo 函数



## 静态检查 *

使用静态代码分析工具，来检测潜在的内存泄漏、不安全的内存操作，以及其它不合规范 等问题。这些工具可以帮助你发现代码中的潜在问题，提升程序健壮性，也可针对性减少内存占用。



### cppcheck

安装 bin 到系统并添加到环境变量后，VsCode 安装 `cpp-check-lint` 插件即可，可以对插件做进一步配置。



[Cppcheck - A tool for static C/C++ code analysis](http://cppcheck.net/)。

[vscode中嵌入cppcheck进行静态检查，包含插件使用方法_cppcheck集成到vscode-CSDN博客](https://blog.csdn.net/qq_35333978/article/details/122347687)。设置插件，也可以通过 VsCode 可视化操作而不必直接修改 setting 的 json 文件。这个因人习惯而异吧。



### clangd / clang-tidy

clangd

clangd 提供的 LSP 服务 给 VsCode 日常开发的 跳转、补全 等用，见 `cmake 模板工程` 仓库（暂没有上）的具体使用。



clang-tidy

> `clang-tidy`拥有多种内置检查器，可用于检测性能问题、代码规范、可能的程序错误、可移植性问题等。此外，它允许用户自定义规则，可以非常灵活地适应不同的编程规范和需求。

[Clang-Tidy — Extra Clang Tools documentation (llvm.org)](https://clang.llvm.org/extra/clang-tidy/index.html) 其中包含了 Clang Static Analyzer，以及更多检查项。

[clang-tidy - Clang-Tidy Checks — Extra Clang Tools 20.0.0git documentation (llvm.org)](https://clang.llvm.org/extra/clang-tidy/checks/list.html) 支持的检查类型。

> clang-tidy 大致分类：
> boost 检测boost库API使用问题
> cert 检测CERT的代码规范
> cpp-core-guidelines 检测是否违反cpp-core-guidelines
> google 检测是否违反google code style
> llvm 检测是否违反llvm code style
> readability 检测代码上相关问题，但又不明确属于任何代码规范的
> misc 其它一些零碎的check
> mpi 检测MPI API问题
> modernize 把C++03代码转换成C++11代码，使用C++11新特性
> performance 检测performance相关问题

clang-tidy 检查项各项更详细的说明：[使用 Clang-Tidy 进行静态代码分析：完整的配置与 CMake 集成实例_clang-tidy cmake-CSDN博客](https://blog.csdn.net/stallion5632/article/details/139545885)



[开源C++静态代码检测工具clang-tidy、cppcheck和oclint的比较_clang-tidy cppcheck-CSDN博客](https://blog.csdn.net/stallion5632/article/details/139569439)。



这是 clang-tidy 介绍 和 命令行的使用，一般更好的使用方法是与 IDE 结合，比如 VsCode。

[30.静态代码分析工具clang-tidy-CSDN博客](https://blog.csdn.net/lx_ros/article/details/139104753)。[c++静态代码扫描工具clang-tidy详细介绍-CSDN博客](https://blog.csdn.net/sexyluna/article/details/132001613)。



[vscode配置clang-tidy插件_vscode clang-tidy-CSDN博客](https://blog.csdn.net/weixin_45978181/article/details/128239547)。



实测发现，clang-tidy 有一些基础的问题查不出来，比如数组越界，等等（或许也是我配置有问题？）。这种意义上，cppcheck 还是 好用些。



关于 clangd、clang-tidy 的配置文件，可参考 TODO 放自己 cmake 模板工程 仓库。



scan-build

> `scan-build`是一个命令行工具，用于在编译时调用`Clang`静态分析器来分析C/C++代码。它的主要用途是识别程序中可能导致bug的构造。
>
> `scan-build`在编译过程中拦截编译器的调用，插入静态分析过程。它会生成一份包含潜在错误和警告的报告，并可以通过生成的HTML报告详细查看问题所在及上下文。
>
> `scan-build`通常在命令行环境中使用，可以轻松地与持续集成系统集成，作为项目构建过程的一部分自动运行。



### 编译时提示



综合 [C++ Diagnostic Basics: Warnings, Assertions, Testing | hacking C++ (hackingcpp.com)](https://hackingcpp.com/cpp/diagnostics.html)。

使用`-Wall`、`-Wextra`等标志打开所有警告。



## 大型静态检查软件



### SonarQube + sonar-cxx *

社区开源的。可以和 jenkins 结合。



[SonarQube C++ 社区插件安装与配置指南-CSDN博客](https://blog.csdn.net/gitblog_09137/article/details/142229356)。

[SonarQube 安装及使用 | Server 运维论坛 (learnku.com)](https://learnku.com/articles/59179)。



### Black Duck / Coverity

商业级静态扫描服务，收费的。

- [SAST - 静态代码分析工具 | Black Duck](https://www.blackduck.com/zh-cn/static-analysis-tools-sast.html)。[Coverity 静态分析软件 | Black Duck](https://www.blackduck.com/zh-cn/static-analysis-tools-sast/coverity.html)。
- [Black Duck 软件组件分析 (SCA) | Black Duck](https://www.blackduck.com/zh-cn/software-composition-analysis-tools/black-duck-sca.html)。帮助团队管理在应用和容器中使用开源和第三方代码所带来的安全、质量和许可证合规性风险。



[Coverity 代码静态安全扫描工具 ： 认识Coverity-CSDN博客](https://blog.csdn.net/baidu_31295661/article/details/122367838)。



# 内存占用优化相关



## 初步检查

如果对程序熟悉，针对性的对占内存的地方 进行优化。



使用 上述 内存统计命令和工具，检查。

看大头：

- 最小工程放到机器上看内存占用，和正式的进程进行比较

  一般 [heap]、[anon]、各种库、字体等 占了该进程的主要内存大头

- 程序中按各块功能逐个开启，看内存。

- UI界面，逐个页面加载看内存增长变化。

看细节：

比如 perf mem 等工具分析每个函数申请内存的情况，找出大头。



## 基本优化

这里以 qt 程序的内存占用优化为例。



### 库编译精简



编译器选项：使用适当的编译器选项，例如优化标志，以提高生成的代码的效率和内存使用。

调试相关的有 `-g -ggdb`，优化相关的有 `-O0 -O1 -O2 -Os`，工程上经验建议最高允许也常常开到 `-O2`。



比如 qt库 有一些精简编译的选项可以用。

在 buildroot 的 qt 选项里面 添加 Custom configuration options，看 package 里面 qt 文件夹 里面的 .in 和 .mk 文件可见，最终传递给 
`buildroot/output/<board>/build/qt5base-5.xx.x` 下面的 configure（通过 `./configure -help` 查看 所有配置选项）

添加选项 `-optimize-size -release -strip -reduce-exports`。

主要的核心库

- libQt5Core.so.5.12.2    4.89MB
- libQt5Gui.so.5.12.2    3.71MB
- libQt5Widgets.so.5.12.2    5.64MB
- libQt5Qml.so.5.12.2
- libQt5Quick.so.5.12.2    5.64MB
- libQt5Network.so.5.12.2    1.46MB
- libQt5VirtualKeyboard.so.5.12.2

qt 库 重编（这里是基于 buildroot 编译框架 来 编译 qt package）

```bash
make qt5base-dirclean && make qt5base-configure && make qt5base
```



### 针对项

- 程序的内存优化。

- UI 页面不缓存（但是 UI 理论上相对会变卡顿，具体看芯片性能）。精简 UI 页面。限制显示元素。

- 图片尽量不变形，图片变形会拷贝图片导致内存暴增（Qt）。批量显示图片的地方可以设置图片不缓存。

- 字体。

  这里是针对性缩减字体文件的，如果 flash 或者 ram 充裕 则不推荐这么做，为了未来的可能出现的各种文本的正常显示，留一定较广泛的兼容性较好。

  使用 fontcreator 挑出所用文字，缩小字体库，需要手动增减文字，对于后面增加文案来说不友好 https://blog.csdn.net/xiaohui_brook/article/details/51909612；一个提取给出文本中所有单独文字工具 https://gitee.com/Polarix/MinimumFontLib。



## chatGPT 给出 内存优化 基本经验

以下 chatGPT 给出。



Qt是一个流行的C++应用程序开发框架，可以用于创建跨平台的图形用户界面应用程序。要降低Qt应用程序的内存使用，可以考虑以下方法：

1.使用动态分配内存：避免在堆栈上创建大型对象，而是使用堆上的动态内存分配。使用new和delete或者更好的智能指针来管理对象的生命周期。
2.资源管理：确保及时释放不再需要的资源，如图像、字体、音频等。Qt提供了QResource类来管理应用程序的资源，确保在不需要时卸载它们。
3.使用精简的数据结构：选择最适合你的数据的数据结构。有时候，使用QVector比QList更高效，或者使用QHash而不是QMap，具体取决于你的需求。
4.避免不必要的复制：使用const引用来传递参数，以避免复制大型对象。使用move语义来移动对象，而不是复制它们。
5.使用局部变量：在可能的情况下，使用局部变量而不是全局变量或类成员变量。局部变量在超出其作用域后会自动释放内存。
6.定期清理内存：如果你的应用程序长时间运行，确保定期清理不再使用的内存。Qt的内存管理通常是自动的，但你可以显式地调用QCoreApplication::sendPostedEvents()来处理未处理的事件，这可以释放不再需要的内存。
7.使用Qt的容器类：Qt提供了一系列高效的容器类，如QList、QVector和QMap。使用这些容器类可以减少内存分配和释放的开销。
8.避免内存泄漏：定期检查应用程序以确保没有内存泄漏。你可以使用工具如Valgrind或Qt的内存分析工具来检测内存泄漏。
9.优化图形资源：如果你的应用程序涉及大量图形资源，确保这些资源被合理地加载和释放。使用Qt的图像和绘图类，如QImage和QPainter，来管理图形资源。
10.使用虚函数：如果你使用Qt中的继承体系，请合理使用虚函数。这可以减少对象的内存占用，并允许更高效的动态多态性。
11.精简Qt模块：如果你只需要Qt的特定功能，可以考虑只包含所需的模块，而不是整个Qt框架。这可以减小应用程序的二进制文件大小和内存占用。
12.使用Qt的资源系统：Qt的资源系统允许你将资源文件嵌入到二进制文件中，而不是在磁盘上存储它们，从而减少内存占用。

要降低Qt应用程序的内存使用，最重要的是了解你的应用程序的需求，以便选择合适的数据结构和内存管理策略，并进行适当的优化。

------



如果你的Qt程序已经开发完成，但你仍然想优化内存使用并减少不必要的模块占用内存，可以考虑以下方法：

1.静态分析工具：使用静态代码分析工具，如Clang Static Analyzer或Cppcheck，来检测潜在的内存泄漏、不安全的内存操作和其他潜在问题。这些工具可以帮助你发现代码中的潜在问题，从而减少内存占用。
2.动态分析工具：使用动态分析工具，如Valgrind（在Linux中）或Application Verifier（在Windows中），来检测运行时的内存错误和泄漏。这些工具可以帮助你找出程序中的内存问题，以便进行修复。
3.使用更轻量的替代品：如果你发现Qt模块占用了大量内存，考虑是否可以用更轻量的替代品替代它们。有时候，自定义的轻量级库可能比Qt更适合特定的任务，从而减少内存占用。
4.延迟加载模块：如果你的应用程序使用了多个Qt模块，但不是所有模块都在启动时立即需要，可以考虑延迟加载这些模块。这意味着只有在需要时才加载它们，而不是一开始就加载所有模块。
5.优化资源加载：如果你的应用程序使用大量图像、字体或其他资源，确保资源加载是延迟的，只在需要时加载，然后在不再需要时及时释放。
6.使用轻量级控件：如果你使用Qt的GUI模块，考虑使用轻量级的控件替代重型的控件。例如，可以使用QLabel替代QWebView来显示简单的HTML内容。
7.精简依赖项：如果你使用了第三方库或模块，确保只包括你实际需要的部分，避免引入不必要的依赖项。
8.内存池：实现自定义的内存池，以便更有效地分配和管理内存。这可以减少内存碎片和提高内存使用效率。
9.代码优化：审查代码并寻找可以优化的部分，例如减少不必要的对象复制、避免过度使用虚函数等。优化代码可能需要对性能和内存占用进行权衡。
10.使用Qt的资源系统：将应用程序中的资源文件合并到Qt的资源系统中，以减少磁盘上的文件访问，并降低内存占用。
11.动态链接：如果你的应用程序使用了大量的Qt模块，可以考虑将Qt库动态链接，以减小可执行文件的大小，因为它不会包含Qt库的副本。
12.编译器选项：使用适当的编译器选项，例如优化标志，以提高生成的代码的效率和内存使用。

在进行这些优化时，确保进行充分的测试，以确保你没有引入新的问题或破坏了应用程序的功能。内存优化通常需要权衡性能和内存使用，因此需要根据具体情况仔细评估每个优化步骤的效果。



# 程序中指针、抛异常地方检查





# 查看 bin 结构 / size 优化相关

## elf 解析

### 查看各段

```bash
# 使用 readelf -S <bin> 查看段
# 使用 readelf -h 来查看用法
readelf -S <bin>

# 也可以使用 objdump -x <bin>，注意要使用 bin 对应的编译器的 objdump
objdump -x <bin>

# 把段的原始二进制内容拷出来
objcopy --only-section=.rodata <bin> <output_file>

# 使用 strings 查看 <output_file> 里面的字符串成分
strings <output_file> > <output_strings_file>
```



[objdump命令的常见用法-CSDN博客](https://blog.csdn.net/u014100559/article/details/140620616)。

[基于GCC的工具objdump实现反汇编-CSDN博客](https://blog.csdn.net/qq_27071221/article/details/134297683)。



### 查看对象和函数

查看程序内各个对象和函数的大小并排序

```bash
readelf -s -W <bin> > symbols.txt
awk 'NR > 5 {print $3, $4, $8}' symbols.txt | sort -nr > temp1.txt

第一行的输出例子：

Symbol table '.dynsym' contains 1917 entries:
   Num:    Value  Size Type    Bind   Vis      Ndx Name
     0: 00000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 00000000     0 FUNC    GLOBAL DEFAULT  UND __aeabi_unwind_cpp_pr1@GCC_3.5 (3)
     2: 00000000     0 TLS     GLOBAL DEFAULT  UND _ZSt15__once_callable
     3: 00000000     0 OBJECT  GLOBAL DEFAULT  UND _ZTISt12system_error
     4: 00000000     0 NOTYPE  WEAK   DEFAULT  UND _ZTHN6BGuiFe13ThreadPoolE

把第一行的输出喂给 AI工具来生成，指引其对这段输出进行排序，生成上面第二段命令，执行则排序并输出到 temp1.txt 文件里面
```



## size 优化的点备忘

针对一些占 size 大头 的 东西

- 图片：使用优化工具，减 size；并且尽量使用 编码的数据，如直接存储文件，而不要存储图片数据数组（会膨胀很多，至少 5 倍以上）；可以的话还可以压缩处理。

  以及其它素材文件。

- 库：编译的时候可以去掉一些选项，不编译一些组件，缩减库。

- 依照上面 readelf 读出的程序内各个对象和函数的大小，再针对大的项，进行缩减。

- 加 根据不同产品区分的 功能宏，不编译 不必要的部分。

