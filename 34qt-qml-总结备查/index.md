# QT & QML 总结备查


# QT & QML 总结备查

首要注意，在桌面端开发QT可免费商用，而嵌入式端QT商用则收费。



各种 UI 库的总结和对比：

[Cpp-Learning/C-C++实用库备查.md at main · Staok/Cpp-Learning](https://github.com/Staok/Cpp-Learning/blob/main/C-C%2B%2B实用库备查.md#ui)。



文章所在 Github 仓库 [Staok/QT-QML-Learning: QT & QML 总结备查文章](https://github.com/Staok/QT-QML-Learning) 会保持最新，其它地方的不会跟进。



## 常看常新

QT 安装：网搜 Qt Creator 下载和安装即可。

编译器：对于 Win 上

- 可以选择 mingw 等。可以用 msys2 包管理器 下载 gcc 包 并使用。
- 也可配置使用 msvc 编译器 和 调试器 https://blog.csdn.net/qq_40010218/article/details/124988210。



### Qt \ QtQuick 的学习

- B站搜索即可
- 开源入门书籍，该仓库内积累了极其丰富的 Qt 开发经验
  - https://github.com/feiyangqingyun/qtkaifajingyan
  - https://gitee.com/feiyangqingyun/qtkaifajingyan
  - 上面链接里面有不少 书籍 pdf，其中推荐的书，选择感兴趣的章节看：
    - Qml 详解，好《Qt Quick核心编程》
    - Quick 和 C++ 一块讲，前后端都有个了解，但是讲的比较生硬《QT5 编程入门》
    - C++ 基础，Qt 下 C++ API 详解，好《C++  Qt设计模式》
    - 《从此乱码是路人》
- 入门系列 https://blog.csdn.net/qq_38880380/category_9592212.html
- Qt 提供的组件 https://www.qt.io/product/features
- Qt 测试相关 https://www.qt.io/product/quality-assurance，GUI 测试、代码覆盖率、静态检测等。
- Qt 对嵌入式的支持 https://doc.qt.io/embedded.html
  - MCU https://doc.qt.io/QtForMCUs-2.5/
  - 嵌入式 Linux，即 Qt for Device Creation https://doc.qt.io/Boot2Qt-5.15/
  - QtEmbedded，经查，这是 Qt 4.x 时代的东西，对于 Qt 5.x、6.x，目前已经被 Qt for Device Creation 取代，即在 配置 qt 库的时候指定交叉编译器 https://doc.qt.io/qt-5/configure-linux-device.html。




Qt Designer 教程：

- B站搜索即可



### 优秀开源参考

下面列出优秀开源仓库，分别列出 Github 和 Gitee 链接；
包含众多Qt组件使用案例可参考借鉴。

- Qt 中文文档
  	https://github.com/QtDocumentCN/QtDocumentCN

  ​	https://gitee.com/cryfeifei/QtDocumentCN

  

- Qml 丰富组件使用示例库：

  ​	https://github.com/zhengtianzuo/QtQuickExamples

  ​	https://gitee.com/zhengtianzuo/QtQuickExamples

  

- Qml 丰富使用例子

  ​	https://blog.51cto.com/u_12606971/category21.html

  ​	https://blog.51cto.com/u_12606971/category22.html

  

- QtQuick/Qml基础库和示例：

  ​	https://github.com/jaredtao/TaoQuick

  ​	https://gitee.com/jaredtao/TaoQuick

  

- Qml/C++小工具包

  ​	https://github.com/188080501/JQTools

  

- Qt Widget 优秀参考：

  开源的demo：

  ​	https://github.com/feiyangqingyun/QWidgetDemo

  ​	https://gitee.com/feiyangqingyun/QWidgetDemo

  控件集合

  ​	https://github.com/feiyangqingyun/qucsdk

  ​	https://gitee.com/feiyangqingyun/QUCSDK

  B站演示视频，众多例子开源可下载借用

  ​	https://space.bilibili.com/687803542/video

  开源嵌入式QT组件

  ​	https://gitee.com/coffeeLVeris/qt_open_icon

  编程语录

  ​	https://github.com/feiyangqingyun/bianchengyulu

  ​	https://gitee.com/feiyangqingyun/bianchengyulu

  丰富使用例子

  ​	https://blog.51cto.com/u_12606971/category11/p_4

  ​	https://blog.51cto.com/u_12606971/category18.html



### MISC

- Qt Widgets、QML、Qt Quick 的区别： https://waleon.blog.csdn.net/article/details/54141552

- QML 编码约定： https://waleon.blog.csdn.net/article/details/60964759
- Qt 资料大全：（内含编码风格、论坛） https://waleon.blog.csdn.net/article/details/51752029



在线源码查看 https://codebrowser.dev/qt5/



### QT 和 各个组件 开源协议



简述 各种版本的QT（专业版、商业版、社区版） 用于 PC软件、设备 等 的条件：

https://www.qt.io/licensing

有提到，社区版 用于 PC软件 或 设备 上，必须遵守 [(L)GPL](https://www.gnu.org/licenses/lgpl-3.0.en.html)。



https://doc.qt.io/qt-5/qtcore-index.html#licenses-and-attributions

> Qt Core 可根据商业许可获得[The Qt Company](http://www.qt.io/about-us/)。此外，它可以在自由软件许可下使用。从 Qt 5.4 开始，这些自由软件许可证是[GNU Lesser General Public License, version 3](http://www.gnu.org/licenses/lgpl-3.0.html)， 或者[GNU General Public License, version 2](http://www.gnu.org/licenses/gpl-2.0.html)。看[Qt Licensing](https://doc.qt.io/qt-5/licensing.html)了解更多详情。



各组件 的 使用许可 列表（只有 专业版 和 商业版 对于 PC软件 和 设备 上使用的说明）

https://www.qt.io/terms-conditions/qt-dev-framework/exhibit-1



qt 各组件 下的使用的三方库的开源协议

https://doc.qt.io/qt-5/licenses-used-in-qt.html



> GNU GPL（GNU通用公共许可证）和LGPL（Lesser GNU通用公共许可证）是一种常见的开源软件许可证。下面是对GPL2和LGPL3的简述以及它们之间的区别：
>
> GNU GPL（GPL2）： GPL2是GNU GPL的第二版，它是自由软件基金会（FSF）发布的一种开源软件许可证。主要特点包括：
>
> 1. 自由传播：GPL2要求任何以GPL2许可的软件必须能够自由传播。用户可以复制、分发和修改被许可的软件，并且任何以GPL2许可的衍生作品也必须在相同的许可下分发。
> 2. 源代码可用性：GPL2要求在分发和修改GPL2许可的软件时，必须提供相应的源代码，并允许接收者以GPL2的条件使用、修改和分发源代码。
> 3. 程序和库的一致性：如果你将一个GPL2许可的库嵌入你的应用程序中，你的应用程序也必须以GPL2许可进行分发。这被称为"传染性"的特性。
> 4. 版权声明：GPL2要求在软件中包含原始版权声明和GPL2许可文本。
>
> Lesser GNU GPL（LGPL3）： LGPL3是Lesser GNU通用公共许可证的第三版，也是由FSF发布的一种开源软件许可证。相对于GPL2，LGPL3更适用于库和框架的开源许可。其主要特点包括：
>
> 1. 动态链接：LGPL3允许将LGPL3许可的库与闭源应用程序进行动态链接，而不需要将应用程序的源代码公开。这使开发者能够使用LGPL3许可的库构建闭源商业产品。
> 2. 版权声明：LGPL3要求在库中包含版权声明和LGPL3许可文本。如果修改了库的源代码，则还需要提供修改后的源代码。
> 3. 衍生作品的许可：如果基于LGPL3许可的库创建了衍生作品，这些衍生作品也必须以LGPL3许可进行分发。
>
> 区别： 主要的区别在于GPL2对于软件的传染性要求，而LGPL3则更加灵活，特别适用于库和框架。具体来说，区别包括：
>
> 1. 传染性：GPL2具有传染性，要求整个衍生作品遵循GPL2许可，而LGPL3相对较灵活，允许闭源应用程序与LGPL3许可的库进行动态链接。
> 2. 动态链接：LGPL3允许将LGPL3许可的库动态链接到闭源应用程序中，而GPL2则将所有程序（包括应用程序和库）视为一个整体。
> 3. 库和框架的适用性：LGPL3更适合作为库和框架的许可证，而GPL2主要用于完整的应用程序。
>
> 需要特别注意的是，我提供的是简要概述，具体的许可证条款和法律解释可能更加详细和具体。如果您需要更具体的法律建议，请咨询专业的法律顾问或律师。



## 前置信息

### 最佳实践 / 性能优化 / 技巧

Qt 文档 `Qt Overviews`

> Qt Overviews 
>
> Qt features a wide range of different technologies. The following topics are key areas of functionality and can be used as a starting point for learning how to to get the most of Qt.
>
> - Development Tools
> - User Interfaces
> - Core Internals
> - Data Storage
> - Multimedia
> - Networking and Connectivity
> - Graphics
> - Integrating Web Content
> - Mobile APIs
> - QML Applications
>
> - Scripting
> - Internationalization with Qt
> - Testing and Debugging
> - Porting from Qt 4 
>
> Best Practices
>
> These pages give guidance on how to use Qt technologies best to create applications that excel in usability and software design.
>
> | Accessibility                                  | How to make your applications accessible to those with disabilities. |
> | ---------------------------------------------- | ------------------------------------------------------------ |
> | Accessibility for Qt Quick Applications        | How to make your applications accessible to those with disabilities. |
> | Best Practices for QML and Qt Quick            | Lists best practices for working with QML and Qt Quick       |
> | Books about GUI Design                         | Some recommended books about GUI design                      |
> | Calling Qt Functions From Unix Signal Handlers | You can't. But don't despair, there is a way...              |
> | Coordinate System                              | Information about the coordinate system used by the paint system |
> | Creating Custom Qt Types                       | How to create and register new types with Qt                 |
> | Creating Shared Libraries                      | How to create shared libraries.                              |
> | Creating and Using Components for Qt Designer  | How to create and use custom widget plugins                  |
> | Desktop Integration                            | Integrating with the user's desktop environment.             |
> | Exception Safety                               | A guide to exception safety in Qt.                           |
> | How to Create Qt Plugins                       | A guide to creating plugins to extend Qt's applications and functionalities. |
> | Implementing Atomic Operations                 | A guide to implementing atomic operations on new architectures. |
> | Qt Test Tutorial                               | A short introduction to testing with Qt Test                 |
> | Restoring a Window's Geometry                  | How to save  restore window geometry.                        |
> | Rich Text Processing                           | An overview of Qt's rich text processing, editing and display features |
> | Scalability                                    | How to develop applications that scale well on devices with different screen configurations and UI conventions. |
> | Session Management                             | How to do session management with Qt.                        |
> | Setting the Application Icon                   | How to set your application's icon.                          |
> | Standard Accelerator Keys                      | Recommended accelerator keys.                                |
> | Timers                                         | How to use Qt timers in your application                     |
> | Using Qt D-Bus Adaptors                        | How to create and use DBus adaptors in Qt                    |



QML 性能优化建议

- https://zhuanlan.zhihu.com/p/617646961
- https://zhuanlan.zhihu.com/p/617667595



一些 QtQuick 开发技巧

https://blog.csdn.net/qyvlik/article/details/51226005



how-to-write-clean-qml-code

https://scythe-studio.com/en/blog/how-to-write-clean-qml-code



有哪些机制，让 qml 更省内存

chatGPT

> 在 Qt QML 中，可以采取一些机制和最佳实践，以降低内存使用，从而使你的应用程序更加节省内存。以下是一些可用的方法：
>
> - 图像和资源管理：使用适当的图像格式和尺寸。确保图像不过大，可以通过工具进行压缩和优化。将大型图像切成小块以进行懒加载，只加载在需要的时候。
>
> - 
>   资源管理：使用 Image 控件的 cache 属性来管理图像的缓存，根据需要禁用缓存，以节省内存。使用 Loader 控件来异步加载和卸载组件，从而减少一次性加载大量内容带来的内存开销。
>
> - 
>   垃圾回收和销毁对象：在不再需要的时候，手动销毁 QML 对象以释放内存。例如，通过调用 JavaScript 函数 destroy()，以及在需要时解除信号连接。使用 JavaScript 引擎的垃圾回收来清理不再使用的对象。
>
> - 
>   对象池：对于那些需要频繁创建和销毁的对象，可以实现对象池来重复使用这些对象，而不是频繁地创建和销毁它们。
>
> - 
>   内存优化的 QML 设计：避免创建过多的不必要的对象。设计你的 QML 代码以便在可能的情况下重用对象，而不是不断地创建新的实例。避免在循环中创建大量的对象，因为这可能会导致内存泄漏。
>
> - 
>   使用位图字体：如果可能的话，使用位图字体代替矢量字体。矢量字体可以产生大量的内存开销，特别是在大型文本块的情况下。
>
> - 
>   合理使用 C++ 与 QML 混合编程：在某些情况下，使用 C++ 编写性能敏感的代码，以降低内存和 CPU 开销。C++ 可以更好地控制内存管理。
>
> - 
>   监测内存使用：使用 Qt 的内存分析工具来监测内存使用情况，以找出可能的内存泄漏和瓶颈。
>
> - 
>   减少不必要的渲染：使用 visible 属性来控制哪些元素在屏幕上可见，以减少不必要的渲染。
>
> - 
>   定时清理：使用定时器来定期清理不再需要的对象和资源。
>
>
> 总的来说，内存优化在 QML 中是一个综合性的工作，需要综合考虑你的应用程序的特定需求和限制。使用上述策略和实践来降低内存使用，可以提高应用程序的性能和稳定性。
>
> 
>
> 除了上述提到的机制和最佳实践，以下是更多方法，可帮助降低 Qt QML 应用程序的内存占用：
>
> - 使用 ListModel 代替 JavaScript 数组：在处理大量数据时，使用 ListModel 作为数据模型，而不是普通的 JavaScript 数组。ListModel 可以更有效地管理数据并降低内存使用。
> - 避免使用过多的不必要数据绑定：数据绑定是 QML 的强大特性，但滥用它可能导致内存占用增加。确保只在需要时进行数据绑定，避免不必要的信号和属性绑定。
> - 使用 Repeater 控件：Repeater 控件允许你重复创建相似的元素，而无需为每个元素创建单独的实例。这可以减少内存占用。
> - 使用 WorkerScript 进行异步计算：对于需要进行长时间计算的任务，可以将其放在 WorkerScript 中，以避免阻塞主线程并减少内存开销。
> - 减少 JavaScript 对象的复杂性：简化和规范你的 JavaScript 对象结构，避免过于复杂的嵌套对象，以降低内存使用。
> - 使用位运算或位图来管理状态：对于需要跟踪多个状态的场景，可以使用位运算或位图来更有效地管理状态信息，减少内存开销。
> - 优化界面布局：避免使用过多不必要的布局元素，合理设计布局以减少布局元素的数量，从而减少内存占用。
> - 使用虚拟滚动和分页加载：当处理大量数据时，实现虚拟滚动和分页加载，以便只加载和渲染当前可见区域的数据，而不是全部数据。
> - 适度使用缓存：尽管可以在 QML 控件中禁用缓存，但在某些情况下启用缓存可以提高性能。根据具体情况权衡是否启用控件的缓存。
> - 分析内存占用：使用 Qt Creator 或其他性能分析工具来分析内存占用，找出潜在的问题和内存泄漏，并对应用程序进行适当的优化。
>
> 记住，内存优化通常需要在应用程序的开发周期中进行多次迭代和测试。根据应用程序的特定需求和性能要求，采取不同的策略和组合来降低内存占用。



### 用法查找

1. 在组件上按 F1 弹出帮助。

2. 网搜具体控件的使用，CSDN、知乎等文章。

3. 参考上面 “Qt 中文文档” Github 仓库里内容。浏览 MarkDown 文档用 Typora（网搜有和谐版）。

4. Qt Creator 自带帮助，目录文档：

   All QML APIs by Module

   All QML Basic Types

   All QML Modules

   All QML Types

5. 下面给出“Qt Qml 控件总结”



### Qt Creator & QML tips



**Qt Creator**

- 编辑 QML 最好看着看实时效果来，用 QML Preview 一点点调就好。
- 在 “编辑” 界面进行主要工作，“设计” 界面可以对 .ui 或 .qml 编辑界面（对于qml/quick开发并不常用），“项目” 界面设置工具链。
- 在组件上按 F1 弹出帮助。
- ctrl + f：当前文件搜索，可使用高级搜索。
- ctrl + k：搜索文件。



**Qml**

- 每个页面文件中的文案，使用便利的数据结构（如 Qt 里的 ListModel）集中组织起来，并统一放到页面文件的最上方。

  单个页面具有重复性的元素的（以行或列排列）使用动态显示组件（比如 Qt 的 ListView）。

- qml 页面中的 自定义属性 可以都放到 QtObject（不可见控件，官方手册说很方便用于包裹一些杂物） 控件里面打包。

- 所有的 Qml Item 控件 最好都加上 Id 和 objectName 属性，二者同名即可，且最好是全局名字唯一，可以用 `属什么_是什么_做什么` 的规范来命名，比如 `page_rect_comp`，在 page（页面） 的 rect（矩形） 用来作为 comp（组件）。objectName 方便 C++ 端 寻找到该控件。

- 多使用 Item 对控件进行分组。当前控件或窗口捕获到 鼠标事件 或者 键盘事件 后，应该设置 相应的 mouse.accepted 为 true，再进行处理，防止事件（或者说信号）继续传播（给其它控件）。这个按需求来。

- 字数多的文本框，要加 width / maxWidth(ZText)，并且启用换行 wrap。

- 在 Text 或 Rectangle 等控件（不是所有控件）上 按下 ctrl + alt + space 则弹出快速设置这些 控件 的 弹窗。



### QML 辅助设计

但目前还是手写 Qml 居多，推荐用 QML Preview 看实时效果

- figma：https://www.figma.com/。

  ​    https://www.bilibili.com/video/av931445067/。

  ​    https://www.bilibili.com/video/BV15e4y1d7E5/。

  ​    https://edu.csdn.net/learn/30741/459042。

- 及时设计 + CODE.FUN插件 导出 js 代码。

  ​    https://www.bilibili.com/video/BV1KB4y1n7mX/。

  ​    https://js.design/tutorial/63b4ec9d2bd11c40c496212c。

- Qt Design Studio：可以图形化编辑 UI，也可以导入 figma 设计文件，然后导出 QML。

  ​    B站搜索相关教程：https://search.bilibili.com/all?keyword=Qt Design Studio。



### Qt 调试&性能优化

- QT debug and performance
  - QT log redirection，可以通过 `InstallMessageHandler(QtMessageHandler handler)` 重定向 log 输出。
  - QLoggingCategory，使用 QLoggingCategory 过滤所需 log。
  - QT QML Profiler，Qt Creator 的 Analyze->QML Profiler，可视化监控程序运行全程，各项参数，调用函数，函数调用火焰图，对耗时的地方针对性优化。
  - QT performance，QT 官方对于提升性能的指导和建议：https://doc.qt.io/qt-5/qtquick-performance.html#common-interface-elements。
- 根据 perf 抓取 qt 底层调用火焰图找出耗时API，热点函数，针对性优化，利用硬件进行加速。
- https://blog.csdn.net/qq_35865125/article/details/85867397。



### 测试 / 验证

官方质量保证工具：https://www.qt.io/zh-cn/product/testing-tools，https://www.qt.io/zh-cn/product/quality-assurance。

- Squish，GUI自动化测试
- Coco，代码覆盖率分析
- Test Center，测试结果管理和分析
- Axivion，静态代码分析与架构验证



- Qt Insight，https://www.qt.io/product/insight。



## Qt QML 常用控件总结备查 / 俯瞰

### QtQuick

- Item（x、y、z、width、height、visible、enabled、foucus、anchors、status、clip、opacity、forceActiveFocus() 等等）

  The Item type is the base type for all visual items in Qt Quick.

- Rectangle

- Text

- Column、Row、Grid、Flow；GridView

- MouseArea（MouseEvent，WheelEvent）

- Keys（KeyEvent），Drag（DragEvent）

- Image

- Loader

- TextInput；TextEdit

### QtQuick.Window

- Window（CloseEvent）

### QtQml

（QtQuick.Controls 包含 QtQml）

- Component
- Binding、Connections
- Timer

### QtQuick.Layouts

- GridLayout
- ColumnLayout、RowLayout
- StackLayout



### QtQuick.Controls

（包含 QtQml）（有 1系列版本 和 2系列版本，其内的控件有差别）：

- ApplicationWindow
- Label
- Button、RadioButton、RoundButton、Switch
- CheckBox、GroupBox、SpinBox
- TextField；TextArea
- BusyIndicator、Dial、ProgressBar
- Slider、RangeSlider
- ScrollBar、ScrollView
- ListView
- Menu、MenuBar
- ComboBox
- TabView（QtQuick.Controls 1.4）、TableView
- Calendar、Tumbler
- StackView、Page、Dialog、Popup

### QtQuick.Dialogs

- ColorDialog	Dialog component for choosing a color
- Dialog		A generic QtQuick dialog wrapper with standard buttons
- FileDialog		Dialog component for choosing files from a local filesystem
- FontDialog	Dialog component for choosing a font
- MessageDialog	Dialog component for displaying popup messages

### Other

- QtCharts
- QtQuick.VirtualKeyboard（QtQuick.VirtualKeyboard.Settings）
- QtTest		This module provides QML types to unit test your QML application
- QtAudioEngine	音频相关
- QtMultimedia	视频播放、摄像头等支持
- QtSensors	读传感器相关
- QtWayland.Compositor	Provides QML types for writing custom Wayland display servers
- QtWebEngine	Provides QML types for rendering web content within a QML application
- QtWebView	显示本地网页
- QtWebSockets	Provides QML types for WebSocket-based communication
- QtWinExtras	Enables the use of Windows features with QML



## 实用三方组件收集

https://blog.csdn.net/m0_60259116/article/details/134247505。

> - 一、自定义控件
> - 二、图表控件
> - 三、网络
> - 四、 音视频
> - 五、多线程
> - 六、数据库



这些已经加到我的 github star 里面了 [Your list / QT](https://github.com/stars/Staok/lists/qt)。



## 常用基础 & 经验

- 控件的 属性 properties 和 方法 methods 使用。
- 调用组件、设置属性，自定义组件、页面，属性暴露，属性参数传递。信号和槽。
- 会看和会使用 Qt 自带帮助。



### C++ 端 显示 Qml 文件

- QQmlApplicationEngine 搭配 qml 文档 根控件 Window 或 ApplicationWindow（看手册有哪些属性，前面 相比于 后面 那种，对于窗口的控制权更多）。

  ```c++
  #include <QGuiApplication>
  #include <QQmlApplicationEngine>
  
  int main(int argc, char *argv[])
  {
      QGuiApplication 或 QApplication app(argc, argv);
      QQmlApplicationEngine engine;
      engine.load(QUrl(QLatin1String("qrc:/main.qml")));
      return app.exec();
  }
  
  //main.qml
  Window 或 ApplicationWindow {
      id: main_window
      objectName: "main_window_objName"
      visible: true
      width: 480
      height: 320
      minimumWidth: 480
      minimumHeight: 320
      title: qsTr("Ts File Translation Tool")
          ...
  }
  ```

- QQuickView 搭配 qml 文档 根控件 Item（适合嵌入式）。

  ```c++
  #include <QGuiApplication>
  #include <QQuickView>
  
  int main(int argc, char *argv[]) {
      QGuiApplication 或 QApplication app(argc, argv);
      QQuickView viewe;
      viewe.setSource (QUrl("qrc:/main.gml"));
      viewe.show();
      return app.exec();
  }
  ```

  

### QML 基础语法

- https://www.cnblogs.com/linuxandmcu/p/11594541.html            语法，变量，原始类型，类型转换（内置函数），函数

- https://www.ngui.cc/el/2490436.html?action=onClick                     QML 中常用的 JS 函数整理

- https://blog.51cto.com/u_15333750/5867537                                  基本组件调用，自定义信号、发射信号和槽函数，事件

- https://blog.csdn.net/wenxingchen/article/details/128515623     自定义信号、发射信号和槽函数

- https://blog.csdn.net/gmcnoah/article/details/129816489            QML中的函数和方法

- https://blog.csdn.net/douzhq/article/details/80959516                 QML JS 循环语句。其它判断语句等同理

- Qt中connect中`[]() and [&]()`有什么区别？

  https://blog.csdn.net/caridle/article/details/129767443

  https://blog.csdn.net/qq_45675910/article/details/107183512



### QML 较全面的基础 API 介绍

https://blog.csdn.net/m0_60259116/article/details/129249920

> - ECMAScript
> - Qt 对象系统
> - Qt Quick 标准库



QML 字符串、数组、MATH

https://blog.csdn.net/m0_60259116/article/details/129250132

indexOf、search、match、length、concat、slice、substring、replace、arg()、RegExp



https://blog.csdn.net/m0_60259116/article/details/129250261

Date、Objec、其它更多实用方法



### QML 中几种信号和槽

- 控件的属性 或 自定的属性 的值 发送变化： `on<Property>Changed : { ... }`。

- qml 控件提供的信号：`on<Signal>: { ... }`，qml 控件提供了哪些 信号 可以看其手册。

- 附加属性的信号，需要写全 `<控件>.on<Signal>`：`Component.onCompleted: { ... }`，`Keys.onReturnPressed: { ... }`，更多：

  ```js
  Keys.enabled: true;
  Keys.onPressed: {
      switch (event.key){
          case Qt.Key_Left:
          	x == 10;
          	break;
          case Qt.Key_Right:
          	x += 10;
          	break;
          case Qt.Key_Down:
          	y += 10;
          	break;
          case Qt.Key_Up:
          	y -= 10;
          	break;
          default:
          	return;
      }
      event.accepted = true;
  }
  ```




官方信号与槽介绍，与三方库交互

https://doc.qt.io/qt-5/signalsandslots.html#using-qt-with-3rd-party-signals-and-slots



多个槽函数连接一个信号，信号发出后，槽函数按照连接的顺序执行。

槽函数里面也可以得到信号发送者。

https://blog.csdn.net/m0_73443478/article/details/128332487



### C++ 实现 Qt 的信号槽机制

https://blog.csdn.net/weixin_41098116/article/details/130281834

https://blog.csdn.net/canon20070904/article/details/122728859



另外有 C++ 的 信号槽库如 libsigc++、KDBindings 等 可以直接用~

参考 [Cpp-Learning/C-C++实用库备查.md at main · Staok/Cpp-Learning](https://github.com/Staok/Cpp-Learning/blob/main/C-C%2B%2B实用库备查.md#sig-slot)。



### QML 控件 ID 作用域

https://blog.csdn.net/ykun089/article/details/120745716

https://blog.csdn.net/qq_31375721/article/details/125173953

- 子控件内部 可以访问到 自己的 ID，子控件也可以访问 同级别 其它控件的 ID。
- 子控件可以访问到 上级们的控件的 ID，子控件也可以访问到 上级们的 同级别的 控件的 ID。
- 但是 子控件 存在无法访问到 同级别控件的 子控件的 ID 的问题，这时应该将 后者 ID 通过 property alias 放到 本 qml 文件的 最前面的 根控件 下，作为本 qml 文件的全局变量，就可以访问到。其它情况同理。



### QML 属性绑定和解绑

https://cloud.tencent.com/developer/article/1463416

https://blog.csdn.net/CLinuxF/article/details/90713508

函数绑定 https://cloud.tencent.com/developer/article/1625079

总结：

- property : xxx，后面再使用 `=` 赋值 则解除旧绑定而使用新绑定。

- 使用 `Binding`控件对已经解除绑定的属性重新绑定。

- 在 js 函数内绑定 `rect.height = Qt.binding(function() { return this.width * 2 })`。

- Connections。可以在 Item 里面用（其它的像 `on<Singal>`不能写在 Item 里），用于连接信号和槽，比较好用。

  https://blog.csdn.net/douzhq/article/details/81007504



### QML 与 C++ 相互调用



#### 	QML 调用 C++ 类

​	https://blog.csdn.net/byxdaz/article/details/89304074

​	https://blog.csdn.net/Y03977211367Y/article/details/111434962

​    自己定义类，公共继承自 `QObject`，且添加 `Q_OBJECT` 宏（则 Qml 里面 可 使用该类里面的 属性、方法（函数），以及信号和槽），若不使用 信号和槽，可用更轻量的宏 `Q_GADGET`。

​    坑！若这个类要给另一个工程（.pro）用 要在 class 右边添加 `Q_DECL_EXPORT` 修饰符，并且引用头文件 `#include <QtCore/qglobal.h>`。

​    类里面 使用 `Q_PROPERTY` 修饰 要给 qml 访问的各个属性 / 变量，使用 `Q_INVOKABLE` 修饰 要给 qml 访问的各个函数 / 方法。典型实现看 `tsFile_translation_tool`。

​    写函数时，尤其是定义 属性 property 的读写 函数，形参可以写成引用，返回值不能写成引用（除非返回的是静态变量）而是拷贝，要形成这个习惯，因为如果函数里面有申请堆内存，比如 c++ stl 容器 等，返回引用的话那么这块内存就不会释放了，如果频繁调用该函数，很容易内存泄漏。



1 用 `setContextProperty()`（要在 load qml 之前），即在 c++ 里面先例化类，再注册，qml 里面就可以直接用。

```c++
QDataMgr data_mgr; // 先例化类
engine.rootContext()->setContextProperty("DATAMGR", &data_mgr); 
// 注册后则可以在 qml 里面 通过 DATAMGR 使用该类里面的 属性、方法（函数），以及信号和槽
```



2 用 `qmlRegisterSingletonType()`，注册单例控件（要在 load qml 之前），这是 带回调的注册函数 https://blog.csdn.net/weixin_42208702/article/details/132001997

好的例子：

```c++
qmlRegisterSingletonType<FileManagerQt>("FileManagerQt", 1, 0, "FileManager",
										[](QQmlEngine*, QJSEngine*) -> QObject* {
	QQmlEngine::setObjectOwnership(&FileManagerQt::inst(), QQmlEngine::CppOwnership);
	return &FileManagerQt::inst();
});

// 类的 ::inst() 定义，例子：
class FileManagerQt
    : public QObject, public FileManager
{
    Q_OBJECT
	...
public:
	static FileManagerQt & inst();
	...
signals:
    ...
public slots:
    ...
private:
    ...
}

FileManagerQt & FileManagerQt::inst()
{
    static FileManagerQt FileManagerQt_;
    return FileManagerQt_;
}
```



3 qmlRegisterType()，常规注册方式

```c++
qmlRegisterType<FileSimple（类名）>("FileSimple（库名，一般与类名一致）", 1, 0, "FileSimpleItem（控件名）");
                                                                          // 注意 控件名 首字母要大写

// qml 里面：
import FileSimple 1.0
    ...
    FileSimpleItem {
        id: fileSimpleItem
        objectName: "fileSimpleItem_objName"
        Component.onCompleted: { }
    }
// 便可以用 fileSimpleItem 来使用 FileSimple 类 里面的东西
```

​	

4 qmlRegisterUncreatableType() https://blog.csdn.net/cleverhorse/article/details/86494983

​	即 qml 里面不可创建（类的）对象 的控件，只用其对应的 类 里面的东西，对于类里面提供很多 枚举值 很适用这种注册方法。

​	使用 `Q_ENUM` 修饰 类里面的 枚举类型。



#### C++ 调用 QML

​	https://blog.csdn.net/m0_73443478/article/details/129844458

​	https://blog.csdn.net/baidu_33850454/article/details/81941675

​	读 qml 内属性，典型程序见 `加埋点` 和 `具体控件` 一节的 `EventFilter`，就是从 rootObject 通过 objectName 或者 id 寻找 子 obj，再可以读写 qml 里面 控件 的 属性等等。 

​	调用 qml 里的 js 函数不常用，也不推荐，因为前端尽量只做展示，业务放在 c++ 后端。



### 多语言 & 字体

​	https://blog.csdn.net/zhengtianzuo06/article/details/78550695

​	https://blog.csdn.net/qq_45477402/article/details/124443527

1. qml 和 c++ 中要多语言支持的文案分别使用 `qsTr("<str>") 或 qsTrId` 和 `QObject::tr("<str>") 或 ` 或 `QT_TR_NOOP`。

2. 在工程文件 .pro 中加入`TRANSLATIONS = zh_CN.ts en_US.ts ...`。

3. 用 Qt 自带的 lupdate 生成 .ts 文件：`工具 -> 外部 ->  Qt预言家 -> 更新翻译(lupdate)`。

4. 然后ts文件可以通过各种软件翻译，QT官方使用的是 Qt Linguist，也可以使用 localazy 或者其他工具。

   用 linguist Qt 语言家工具翻译：用该软件打开 .ts 文件 并逐条翻译 后保存，在 Qt 里面：`工具 -> 外部 ->  Qt预言家 -> 发布翻译(lrelease)`，则生成 .qm 文件，不行的话就 用 linguist 工具翻译并发布为 .qm 文件。

5. C++ 里面使用 QTranslator 相关函数 加载 .qm 文件并执行，界面即切换成对应语言。



全局字体设置：

​	https://blog.csdn.net/qq_24890953/article/details/107557023



### 控件位置和排列设置

常用的方式是：

界面左上角第一个组件用x、y 定好位置（或其它方式，或设置可随窗口变化），然后其它组件用 anchors 定与之的相对位置（或随窗口变化），长宽可固定设置或随窗口变化。

如果是有规律的列表显示，多个组件的重复排列，可用 ListView 或 Repeater，推荐前者。

Qml 里面不用 Row/Column 相对位置组件（实测用了之后很多 UIBase 库中的组件容易出问题，估计实现上有冲突）。
多用 Item / Rectangle 和 anchors 来 框住同框的组件 和 组件内的相对位置设置。

使用了 定位器 或 布局管理器 的控件，其 x、y、anchor 等定位属性就无效了，不要再用了。

> 定位器包括Row(行定位器)、Column(列定位器)、Grid(表格定位器)、Flow(流式定位器)。
> 布局管理器包括行布局(RowLayout)、列布局(ColumnLayout)、表格布局(GridLayout)。
>
> QtQuick中的布局管理器与QtWidgets中的相似，它与定位器的不同之处在于：布局管理器会自动调整子Item的尺寸来适应界面大小的变化。
>
> GridLayout所管理的Item，可以使用下列附加属性(这正是布局管理理器和定位器之关键不同点)：
>
> - Layout.row
> - Layout.column
> - Layout.rowSpan
> - Layout.columnSpan
> - Layout.fill Width
> - Layout.fill Height
> - Layout.alignment



横竖排列，网格排列：

QML GridLayout 和 Grid

https://blog.csdn.net/mengfz_cn/article/details/120094644

Column 里面的 Item 不要再用 anchor，因为column已经在帮你管理item的位置了。你设置了anchor如果和column冲突，是无效的。

https://ask.csdn.net/questions/10917



## 问题解决



#### 工程文件 .pro 解析

https://zhuanlan.zhihu.com/p/616842442。



#### 更新 qml 再运行

qml 文件代码更改后直接构建运行还是上次的结果解决：https://tieba.baidu.com/p/4206771409。

或者，在 Qt 工程里项目文件夹上面右击选择 “执行qmake” 一下再 Run。



#### Qt 非阻塞处理机制（Qt 的 单线程循环 QEventLoop 和 多线程 QThread 编程）

看这篇 https://zhuanlan.zhihu.com/p/614426792，分为 

- 非阻塞（主线程）同步。即 QEventLoop，同步等待，但是不阻塞 GUI 主线程。
- 非阻塞（主线程）异步，即 多线程，线程内处理后用 回调函数 或者 信号槽机制 异步的返回结果再处理。



非阻塞同步：

- QEventLoop。https://blog.csdn.net/QtCompany/article/details/129282296，用事件循环方式 QEventLoop 同步等待。

  在本文里面直接搜 QEventLoop，有一些例子。



非阻塞异步：

- 线程法。QThread，写个类继承 QThread，写个设置运行函数的 方法成员，用 std::function 接，填入函数可以用 lambda 并捕获必要的上下文数据。

  https://blog.csdn.net/qq_37529913/article/details/110521759

  或者 std::thread 如：

  ```c++
  // add format_sdcard_exec() to a thread to exec
  std::thread t(format_sdcard_exec); t.detach();
  
  std::thread t( [] (...) {...}); t.detach();
  ```

  这种临时任务另启一个线程可以，但是遇事不决就随意新开线程不推荐，增加线程切换负担。

- QtConcurrent。本质是使用线程池

  https://blog.csdn.net/danxibaoxxx/article/details/121381000

  https://blog.csdn.net/HighproX/article/details/127074258



#### 子页面向父页面传参

StackView 子页面向父页面传参

https://blog.csdn.net/weixin_44820280/article/details/123253576

即 子页面添加一个绑定 父页面 obj 的属性，只能用 obj 去绑定本属性！因为绑定具体属性的话，子页面里面修改属性就解除绑定了，而绑定 obj，这个不改变因此不会解绑。



如果是使用 loader 等切页，那么 还是将所用到的数据均在 c++ 后端写数据结构进行抽象和存储吧，这是规范的。



#### QML 圆角矩形 radius clip 对子组件无效

https://blog.csdn.net/likianta/article/details/110703819

https://blog.csdn.net/gongjianbo1992/article/details/114465501



https://stackoverflow.com/questions/6090740/image-rounded-corners-in-qml

```js
    Image {
        id: img
        property bool rounded: true
        property bool adapt: true

        width: 200
        height: 200

        anchors.centerIn: parent
        source: "file:///xxx/images/bug.png"

        layer.enabled: rounded
        layer.effect: OpacityMask {
            maskSource: Item {
                width: img.width
                height: img.height
                Rectangle {
                    anchors.centerIn: parent
                    width: img.adapt ? img.width : Math.min(img.width, img.height)
                    height: img.adapt ? img.height : width
                    radius: Math.min(width, height)
                }
            }
        }
    }
```



#### 显示图片

Qt Image 控件 显示图片，根据图片文件后缀名加载，若图片本身编码和后缀名不一致会导致显示失败，解决办法

https://blog.csdn.net/qiangzi4646/article/details/80764262

```c++ 
/*  if img file(imgFilePathIn) suffix is not match the img file encode, then correct the suffix(named imgFilePathOut)
    then rename the "imgFilePathIn" file to right one "imgFilePathOut"
    please write some COMMENTs, for the others
*/
QString correctImgFileSuffix(QString& imgFilePathIn, QString& imgFilePathOut, \
        bool isOnlyReturnSuffix, bool& isCorrectSuffix)
{
    imgFilePathOut = imgFilePathIn;

    QFileInfo _fileInInfo(imgFilePathIn);
    const QString _suffix = _fileInInfo.suffix();

    QFile _filein(imgFilePathIn);
    _filein.open(QIODevice::ReadOnly);
    QDataStream file_in(&_filein);
    quint32 magic;
    file_in >> magic;

    /* refer https://blog.csdn.net/qiangzi4646/article/details/80764262
        img file head info
        .jpg    ffd8ff      JPEG (jpg)
        .jpeg   ffd8ff      JPEG (jpg)
        .jpe    ffd8ff      JPEG (jpg)
        .png    89504e47     PNG (png)
        .gif    47494638    GIF (gif)
        .tif    49492a00    TIFF (tif)
        .bmp    424d        16bit(bmp)
    */
    QString correctSuffix = "png";
    switch (magic) {
        case 0x89504e47 : correctSuffix = "png"; break;
        case 0xffd8ff :   correctSuffix = "jpg"; break;
        case 0xffd8ffe0 : correctSuffix = "jpg"; break; // jfif
        case 0x424d :     correctSuffix = "bmp"; break;
        case 0x47494638 : correctSuffix = "gif"; break;
        default: {
            qDebug() << "correctImgFileName(): Unsupported image format";
            return _suffix; // return origin file name : imgFilePathOut = imgFilePathIn;
        }
    }

    if (_suffix == correctSuffix) {
        isCorrectSuffix = true;
        return _suffix; // the correct img file suffix, do not need to change
    }

    isCorrectSuffix = false;
    
    if (isOnlyReturnSuffix) {
        return _suffix;
    }

    // replace suffix to the right
    imgFilePathOut = imgFilePathIn.replace("." + _suffix, "." + correctSuffix);

    qDebug() << "correctImgFileName(): imgFilePathOut" << imgFilePathOut;

    _filein.rename(imgFilePathOut);
    _filein.close();

    return correctSuffix;
}

// 用例：
        QString file2;
        bool isCorrectSuffix;
        QString suffix_temp = correctImgFileSuffix(file1, file2, true, isCorrectSuffix);

        if(!isCorrectSuffix) qDebug() << "uncorrcet img suffix:" << file1;
```



qml Image 控件显示图片的三种方式：https://blog.csdn.net/gongjianbo1992/article/details/128439262

> 1. 从 Qt 资源系统加载：qrc://图片路径
> 2. 文件加载：file://图片路径
> 3. 由 ImageProvider 提供数据：image://provider路径

1. `qrc://` 方式 需要 图片添加到 qt 工程的 qrc 里面，如果是固定的素材则要这么做。

2. `file://` 方式 是可以显示任意路径的图片（不必非要加在 qt 工程 的 qrc 文件里），但是是根据后缀名（suffix）来识别编码而不是识别文件内容，因此如果遇到 png 编码的图片 但 文件名后缀是 .jpg 就会不识别。写程序改后缀名的话不优雅。

3. **好用！**`image://<provider>/` 的方式 是 c++ 后端 写个 provider，内存方式 给 Image 控件 显示，这个不受 图片 后缀名 限制，可以正确显示图片。provider 很好用，可以写个通用的，供 qml 里面 Image 显示图片，QImageReader 提供了不少丰富功能，包括根据图片内容识别图片格式（这就可以直接解决上面说的 问题），还有 Scale 设置、裁剪 等等等。

   ```c++
   if (file.open(QFile::ReadOnly)) 
   {
       QImageReader reader(&file, nullptr);
       reader.setDecideFormatFromContent(true); // add this to let QImageReader Decide Format From Content
       reader.setScaledSize(scaledSize(reader.size()));
       auto image = reader.read();
       if (image.isNull())
           errorString_ = file.fileName() + ": " + reader.errorString();
       else
           image_ = image;
       ...
   ```
   


然后很坑很重要：https://blog.csdn.net/weixin_39628268/article/details/111979647

- win 下，Image：`source: "file:///" + "C:/Desert.jpg"`，必须要三个斜杠后面加地址。
- linux 和 安卓 下：这两个系统是一样的路径：`“file://" + <path>`。
- 这些路径变换，用下面的 转换函数即可！



函数做转换

```c
// remove "file:///" to let QFile handle
QString file1 = QUrl(posterUrl_).toLocalFile();

qDebug() << "———————— 1 posterUrl_ " << posterUrl_;
qDebug() << "———————— 2 file1 " << file1;

// add "file:///" to the front to let Image show this pic
posterUrl_ = QUrl::fromLocalFile(file2).toString();

qDebug() << "———————— 3 posterUrl_ " << posterUrl_;

/* 打印结果：
———————— 1 posterUrl_  "file:///data/Auxiliaries/Model...Panda_01.jpg"
———————— 2 file1  "/data/Auxiliaries/Model...Panda_01.jpg"
———————— 3 posterUrl_  "file:///data/Auxiliaries/Model...Panda_01_1692158487.png"
*/
```



#### QT 事件传播链 / 加事件过滤

参考 https://subingwen.cn/qt/event_handler/

> 1. 当事件产生之后，Qt使用用应用程序对象调用notify()函数将事件发送到指定的窗口
>
>    QApplication::notify
>
> 2. 事件在发送过程中可以通过事件过滤器进行过滤，默认不对任何产生的事件进行过滤
>
>    QObject::eventFilter
>
> 3. 当事件发送到指定窗口之后，窗口的事件分发器会对收到的事件进行分类
>
>    QWidget::event
>
> 4. 事件分发器会将分类之后的事件（鼠标事件、键盘事件、绘图事件。。。）分发给对应的事件处理器函数进行处理，每个事件处理器函数都有默认的处理动作（我们也可以重写这些事件处理器函数），比如：鼠标事件
>
>    QWidget::mousePressEvent
>
>    QWidget::mouseReleaseEvent
>
>    QWidget::mouseMoveEvent



实现事件处理函数的几种方法，中间拦截事件，添加自己的处理逻辑

https://www.51cto.com/article/272256.html

以下，从下到上，也是 Qt 处理 事件的传播链顺序

> 1. 重新实现事件函数。 比如： mousePressEvent(), keyPressEvent(),  paintEvent() 
> 2. 重新实现 QObject::event()
> 3. 安装事件过滤器。即给 相应的 QObject 添加 EventFilter
> 4. 在 QApplication 上安装事件过滤器
> 5. 重新实现QApplication 的 notify()方法



qt 事件传播链大致为

1. QApplication::notify()
2. QApplication::eventFilter()，虚函数，可重写，添加自己的处理逻辑
3. 某个具体控件的 QObject::eventFilter()，虚函数，可重写，添加自己的处理逻辑
4. 某个具体控件自己的 QObject::event()
5. 某个具体控件的 某个事件相应函数，比如鼠标事件官方实现有细分  mousePressEvent()、mouseReleaseEvent() 等。



添加 EventFilter

直接看 Qt 手册的 QObject 下的 eventFilter 函数的例子。

即给控件的事件添加回调函数 `eventFilter()`，事件发生（点击、快捷键、语言切换、调出虚拟键盘等等）先进入一个统一的回调函数。



具体方法：

- 新版本的 qt 有 qml EventFilter 控件，可加到 qml 页面中。但是在 c++ 后端 写会更灵活。

- 后端 c++ 自写。具体原理就是，捕获具体某个控件的所有事件，就是这个控件发生了事件了，调用一个回调函数，里面 检查&处理，返回 false 表示事件可以继续传播，返回 true 则 该 事件 不继续传播了。

  - 给 QApplication 或 QGuiApplication  添加 eventFilter()。拦截该 qt 界面中所有的事件。在 eventFilter() 给需要添加处理逻辑的控件加，或需要控件有全局唯一的 id 或 objectName。

    参考 https://www.cnblogs.com/ourran/p/6816986.html 在 QApplication 上安装事件过滤器，拦截所有 GUI 上发生的事件~

  - 通过 qml 或者 页面的 根对象 rootObject，搜索其全部子对象，再逐一添加 eventFilter()。添加时就可以有选择性的。

    参考 https://forum.qt.io/topic/110350/how-to-make-an-eventfilter
    
    页面通过 loader 加载其它页面，可以用这个方法 也找到其它页面 的 根对象，首先找 loader 控件（通过 id 或者 objectName），然后找其 item 属性 得到 load 的 qml 对象的 rootObject。
    
    https://stackoverflow.com/questions/36418941/accessing-qml-objects-from-loaded-qml-using-cpp-code
    
    但是这个还有个问题，通过 stackView 加载的页面怎么获取。



存在问题 & 问题解决：

- 使用 QApplication::eventFilter()，那么全局的事件都会从这里过，会增加系统负担；另外，qml 或 widget 这种 UI 界面上 传播的是 信号 signal，不同于 后端的 event，event 是更原始的，signal 是处理后的 比如 单击 click 信号 是 按下 和 抬起 的 两个或多个事件的组合发生 的触发。

  经过 嵌入式linux soc(A7) 上面测试，快速操作屏幕情况下，没有明显增加卡顿，cpu 占用也没有明显增加，最高均在 35% 左右。

  所以要拦截事件（比如做埋点），更推荐使用下面的方法：

  只使用某些具体控件自己的 QObject::event()，通过根对象寻找符合条件的（比如 id 或 objectName 属性（保持当前页面唯一） 包含 `track` 字符的则处理，否则直接返回）子对象 installEventFilter。对要埋点的控件必加 当前页面唯一的 id 或 objectName 属性。

  对于在 listView 中的 按键，则要加 `listview` 标识符，程序中做特殊处理才能找打 ListView 中的具体哪一个按键被按下，比如 id 设置为 `<widgetType>_listviewBtn_<page>_<name>_track`。

  加个 识别符 `track`，在 eventFilter() 里面可以 只识别带有该 标识符 的 控件的事件。

- 需要单独处理的。统一在 eventFilter() 添加逻辑，界面文件中控件要进行相应修改，而涉及功能逻辑部分不用动

  - 某些控件暂，还需要想办法优化代码实现。无法取到 ListView 的 delegate 的 Component 以及其下控件的 objectName。

    对于 ListView 的 delegate 里的按键控件，要单独添加处理，处理方法：

    delegate 中的 按键控件，id 中加一个特殊标识符 比如 `listviewBtn`，比如导航列表中的 ListView 下的 按键 的 id 合起来就是比如 `zbutton_listviewBtn_nav_track`，然后在 eventFilter() 中识别这个 标识符，然后用 `objParenContext->contextProperty("index").toString();` 找到 其上下文中的 `index` 属性。

  - 该方法，进入 eventFilter() 时传入的 QObject 是信号的发出者，比如按键，若该按键控件见是被层层封装的，或者多个其它控件都封装了该按键控件，那么单看 eventFilter() 传入的 QObject 无法区分（该功用的按键控件在 eventFilter() 可以设置忽略掉），可通过找其 patent() 来区分，这就要求 其 patent 必须有 全局唯一的 id 或 objectName 属性。

    有的共用按键封装了一层，比如 XButton（其 TapHandler 上一层 id 可设 `tapArea_track`），那么向上找一层 patent() 即可，有的共用按键封装了两层，那么需要向上找两层 patent()。

    封装了两层的：XSwitchButton，XCheckBox。对于 XCheckBox，其 MouseArea 上一层 id 可设 `mouseArea_track`，其他同理。而 风扇控制的 XSwitchButton 又是在 ListView 里面，用如上同样的方法区分。

    功用的按键等控件，设置有意义的 id，在 eventFilter() 里面识别 该控件需要网上找一层还是两层。

- 重要注意，程序中会大量读取 QObject* 和 QQmlContext* 等信息，需要判断是否为空，不能对空指针操作，否则界面立即崩掉。

例子：

```c++
// eventMonitor.h
#ifndef EVENTMONITOR_H
#define EVENTMONITOR_H

#include <QObject>
#include <QtQml>
#include <QEvent>
#include <QElapsedTimer>

#include <QGuiApplication>

/* 3 ways of usage
   1 through "rootObject" of a qml file in main.cpp search its all eligible children QObject and add them eventFilter() one by one
        but other aml file loaded by "Loader" is very complex to found:
            https://stackoverflow.com/questions/36418941/accessing-qml-objects-from-loaded-qml-using-cpp-code
        usage:
            QObject* rootObjects = view.rootObject();
            eventMonitor eventMonitor0(rootObjects, true);

    2 add QApplication a eventFilter()
        All events in the QT pass through here, posing a risk of performance congestion and security
        add special process code to widget in eventFilter(), and the tracked widget need global unique "id"
        usage: in main.cpp
            eventMonitor eM;
            eM.eM_installEventFilter(&app);

            or (recommend)
                #if isUITrack_eM
                    eventMonitor::inst().eM_installEventFilter(&app);
                #endif

    3 QGuiApplication::notify() level event filter
        All events in the QT pass through here, posing a risk of performance congestion and security
        before use, in "eventMonitor::eventMonitor(QObject* parent)", add "QGuiApplication::instance()->installEventFilter(this);"
        usage
            use "eM_QGuiApplication app(argc, argv);" insted of "QGuiApplication app(argc, argv);" in main.cpp
*/

#define isUITrack_eM 1

class eventMonitor : public QObject
{
    Q_OBJECT
public:

    static eventMonitor& inst();
    explicit eventMonitor(QObject *parent = nullptr);

    explicit eventMonitor(QObject* rootObject, bool isEnable, bool isPrintMsg = true, bool isGiveObjName_ = false, QObject *parent = nullptr);
    ~eventMonitor() override;

    bool eM_installEventFilter(QObject* installEventFilter_obj);  // "eM" is for "eventMonitor"

    void setEnableEventFilter(bool isEnable);
    void setPrintMsg(bool isPrintMsg);
    void setPrintPos(bool isPrintPos);

    bool eventFilter(QObject *obj, QEvent *event) override;

signals:

public slots:
    void sendTrackMsg(const int mainPageIndex, const int subPageIndex, const QString& objectID, const QString& arg);

protected:
private:
    QObject* installEventFilter_obj_ = nullptr;
    QObject* rootObject_ = nullptr;
    bool isEnable_ = true;
    bool isPrintMsg_ = false;
    bool isPrintPos_ = false;

    QElapsedTimer elapsedTimer;

    // store page now at
    int mainPageIndex = 0; // 0~4 indicate main page index
    int mainPageSubPageIndex[5] = {0, 0, 1, 0, 0}; // mainPageSubPageIndex[mainPageIndex] indicate sub page index

    // variables below that inside eventFilter()
    QEvent::Type eM_eventType;

    QObject* eM_object;
    QQmlContext* eM_context;
    QString eM_objectId;
//    QString eM_objectName;

    QObject* eM_objParent;
    QQmlContext* eM_objParenContext;
    QString eM_objParentId;

    QObject* eM_objPp;
    QQmlContext* eM_objPpContext;
    QString eM_objPpId;
};

class eM_QGuiApplication : public QGuiApplication
{
public:
    eM_QGuiApplication(int argc, char *argv[]);
    ~eM_QGuiApplication() override;

    bool notify(QObject *obj, QEvent *event) override;

signals:
public slots:
protected:
private:
};

//#define DEBUG_eventMonitor
//#define DEBUG_PrintMsg

#endif // EVENTMONITOR_H



// eventMonitor.cpp
#include "eventMonitor.h"
#include <QDebug>
#include <iostream>
#include <string>

#include <QCursor>
#include <QPoint>

eventMonitor& eventMonitor::inst()
{
    static eventMonitor eM;
    return eM;
}

eventMonitor::eventMonitor(QObject* parent)
  : QObject(parent)
{
#ifdef DEBUG_PrintMsg
    isPrintMsg_ = true;
#endif
//    qDebug() << " --- eM: eventMonitor class constructor";
//    QGuiApplication::instance()->installEventFilter(this);
}

eventMonitor::eventMonitor(QObject* rootObject, bool isEnable, bool isPrintMsg, bool isGiveObjName_, QObject *parent)
  : QObject(parent),
    rootObject_(rootObject),
    isEnable_(isEnable),
    isPrintMsg_(isPrintMsg)
{
    if(!rootObject_) { qDebug() << " --- eM: null rootObject"; return ;}

    QObject* object = nullptr;
    QQmlContext* context = nullptr;
    QString objectId = "";
    QString objectName = "";

    QList<QObject*> rootChildren = rootObject_->findChildren<QObject*>();

    for(int i = 0; i < rootChildren.length(); i++)
    {
        object = rootChildren[i];
            if(!object) { continue ;}

        // get id
        context = QtQml::qmlContext(object);
            if(!context) { continue; }
        objectId = context->nameForObject(object);
            if("" == objectId) { continue; }

        // qDebug() auto add '\n', so use std::cout here
        if(isPrintMsg_) std::cout << " --- eM: find Id: " << objectId.toStdString() << ",";

        objectName = object->objectName();

        if ("" != objectName) {
            if(isPrintMsg_) std::cout << " - find N: " << objectName.toStdString() << std::endl; // "N" is for "Name"
        } else {
            if (isGiveObjName_) {
                objectName = objectId + "_objName";
                object->setObjectName(objectName);
                if(isPrintMsg_) std::cout << " - set N: " << objectName.toStdString() << std::endl;
            } else {
                if(isPrintMsg_) std::cout << " - no N " << std::endl;
            }
        }

        object->installEventFilter(this);
    }
}

void eventMonitor::setEnableEventFilter(bool isEnable)
{
    isEnable_ = isEnable;
    if(!installEventFilter_obj_) return ;
    if(isEnable_)
    {
        installEventFilter_obj_->installEventFilter(this);
    } else {
        installEventFilter_obj_->removeEventFilter(this);
    }
}
void eventMonitor::setPrintMsg(bool isPrintMsg)
{
    isPrintMsg_ = isPrintMsg;
}
void eventMonitor::setPrintPos(bool isPrintPos)
{
    isPrintPos_ = isPrintPos;
}

bool eventMonitor::eM_installEventFilter(QObject *installEventFilter_obj)
{
    if(!installEventFilter_obj) {
        return false;
    } else {
        installEventFilter_obj_  = installEventFilter_obj;
        installEventFilter_obj_->installEventFilter(this);
        return true;
    }
}

eventMonitor::~eventMonitor()
{
    installEventFilter_obj_->removeEventFilter(this);
    elapsedTimer.invalidate();
}

/* track and ID definition shall be clear in a doc somewhere
    Measure the average runtime of this function to be 0.35ms, not much CPU usage
*/
bool eventMonitor::eventFilter(QObject *obj, QEvent *event)
{
    if(!isEnable_) return false;
    if(!obj) return false;
    if(!event) return false;

    eM_eventType = event->type();
//    int eventType_int = static_cast<int>(eM_eventType); not used

//    if(QEvent::KeyPress == eM_eventType) /* key, 6 */
//    { if(isPrintMsg_) qDebug() << " --- eM: key"; return false;}

    if(QEvent::LanguageChange == eM_eventType) /* LanguageChange, 89 */
    {
        if(isPrintMsg_) qDebug() << " --- eM: languageChange" << "- lang" << QString(XXX.language());
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "LanguageChange", \
                     QString(XXX.language()));
        return false;
    }

#ifdef Q_OS_WIN
    if(    (QEvent::MouseButtonPress == eM_eventType) /* MouseButtonPress, 2 */
//        || (QEvent::FocusIn == eM_eventType)        /* input software keyboard, 8, not stable, not used */
      )
#endif

#ifdef Q_OS_LINUX
        if(    (QEvent::TouchBegin == eM_eventType)     /* TouchBegin, 194 */
            || (QEvent::HoverEnter == eM_eventType)     /* HoverEnter, 127, response "TapHandler" in qml, its occur this event*/
            || (QEvent::HoverMove  == eM_eventType)     /* HoverEnter, 129, response "TapHandler" in qml */
          )
#endif
    {

    eM_object = obj;

    // get id
    eM_context = QtQml::qmlContext(eM_object);
        if(!eM_context) return false;
    eM_objectId = eM_context->nameForObject(eM_object);
    // get objectName
//    eM_objectName = eM_object->objectName(); not used

    int index;

#ifndef DEBUG_eventMonitor
    // the event sender`s ID must contains "track"!
    // such as "id: mouseArea_track" in XCheckBox.qml and XSwitchButton.qml
    if(!eM_objectId.contains("track")) {return false;}

    // choise, need "onjectName" property, be same as ID
    if(eM_objectId.contains("choise_tapArea_track"))
    {
        // test cannot read its ID, use "onjectName" insted
        QString choise_id = eM_context->contextProperty("choise_objName").toString();
            if(!choise_id.contains("track")) {return false;}
        // get its "index" to know which item is choiced
        index = eM_context->contextProperty("index").toInt();
        if(isPrintMsg_) qDebug() << " --- eM: choise Id" << choise_id << "- index" << index;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], choise_id, QString::number(index));
        return false;
    }
#endif

    // find its parent
    eM_objParent = eM_object->parent();
        if(!eM_objParent) { /*qDebug() << " --- eM: !objParent";*/ return false;}

    eM_objParenContext = QtQml::qmlContext(eM_objParent);
        if(!eM_objParenContext) { /*qDebug() << " --- eM: !objParenContext";*/ return false; }

    eM_objParentId = eM_objParenContext->nameForObject(eM_objParent);

#ifdef DEBUG_eventMonitor
    // for debug
    qDebug() << " --------------- eM: Id" << eM_objectId << "- pID" << eM_objParentId << "- eT" << eM_eventType;
    return false;
#endif

    if(!eM_objParentId.contains("track")) {return false;}

    // get page
    // find btn in ListView of "Navigator" or "BasePage"
    if(eM_objParentId.contains("xb_listviewZb_nav_track")) // in Navigator.qml
    {
        // read its "index" property to locate which btn in a ListView
        mainPageIndex = eM_objParenContext->contextProperty("index").toInt();
        if(isPrintMsg_)
            mainPageIndex ? (qDebug() << " --- eM: page switch" << mainPageIndex << mainPageSubPageIndex[mainPageIndex]) \
                : (qDebug() << " --- eM: page switch" << mainPageIndex) ;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "pageSwitch", "");
        return false;
    } else if(eM_objParentId.contains("xb_listviewZb_subTab_track")) // in BasePage.qml
    {
        mainPageSubPageIndex[mainPageIndex] = eM_objParenContext->contextProperty("index").toInt();
        if(isPrintMsg_)
            mainPageIndex ? (qDebug() << " --- eM: page switch" << mainPageIndex << mainPageSubPageIndex[mainPageIndex]) \
                : (qDebug() << " --- eM: page switch" << mainPageIndex) ;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "pageSwitch", "");
        return false;
    }

    // process specific type qml widget

    // its parent`s parent is the tracked id
    // XCheckBox.qml and XSwitchButton.qml
    // get "checked" to know its state
    if(    eM_objParentId.contains("xcheckBox_mouseArea_track")
        || eM_objParentId.contains("xswitchButton_mouseArea_track")
      )
    {
        eM_objPp = eM_objParent->parent();
            if(!eM_objPp) return false;
        eM_objPpContext = QtQml::qmlContext(eM_objPp);
            if(!eM_objPpContext) return false;
        eM_objPpId = eM_objPpContext->nameForObject(eM_objPp);

        if(eM_objPpId.contains("track"))
        {
            // get "checked" to know it state
            static bool last_checked = true;
            bool checked = eM_context->contextProperty("checked").toBool();
            if(checked != last_checked)
            {
                if(eM_objPpId.contains("listview"))
                {
                    index = eM_objPpContext->contextProperty("index").toInt();
                    eM_objPpId.append("_" + QString::number(index));
                }
                if(isPrintMsg_) qDebug() << " --- eM: ppId" << eM_objPpId << "- checked" << last_checked;
                sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objPpId, last_checked ? "1" : "0");
            }
            last_checked = checked;
        }
        return false;
    }

    // its parent`s parent is the tracked id
    // SimplePaging.qml, downBtn
    if(eM_objParentId.contains("xb_pagerDown_track"))
    {
        eM_objPp = eM_objParent->parent();
            if(!eM_objPp) return false;
        eM_objPpContext = QtQml::qmlContext(eM_objPp);
            if(!eM_objPpContext) return false;
        eM_objPpId = eM_objPpContext->nameForObject(eM_objPp);
        if(eM_objPpId.contains("track"))
        {
            if(isPrintMsg_) qDebug() << " --- eM: pager downBtn ppId" << eM_objPpId;
            sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objPpId, "");
        }
        return false;
    }

    // Dialog.qml
    // read its "index" get which btn(no need for now)
    // read its "modelData.name"(not work, actually use "name") get "buttons.name" to know btn type
    // read its "dialog_errorMsg" or "dialog_text" property get dialog msg, to distinguish unique dialog
    // "dialog_errorMsg" and "dialog_text" choose one not null to send
    if(eM_objParentId.contains("xb_listview_dialog_track"))
    {
//        index = eM_objParenContext->contextProperty("index").toInt(); no need
//        eM_objParentId.append("_" + QString::number(index));
        QString dialog_btn_name =   eM_objParenContext->contextProperty("name").toString();
        QString dialog_xxxFinishTitle    =   eM_objParenContext->contextProperty("dialog_xxxFinishTitle").toString();
        QString dialog_errorMsg =   eM_objParenContext->contextProperty("dialog_errorMsg").toString();
        QString dialog_text     =   eM_objParenContext->contextProperty("dialog_text").toString();
        if(isPrintMsg_) qDebug() << " --- eM: dialog - pId" << eM_objParentId \
                                 << "- btn" << dialog_btn_name << "- title" << dialog_xxxFinishTitle << ". - dialog_errorMsg" << dialog_errorMsg << "- dialog_text" << dialog_text;
        if(dialog_errorMsg != "") {
            sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "dialog_track", \
                         dialog_btn_name + "," + dialog_xxxFinishTitle + "." + dialog_errorMsg);
            return false;
        }
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "dialog_track", dialog_btn_name + "," + dialog_xxxFinishTitle + "." + dialog_text);
        return false;
    }

    // XButton, its parent is the tracked id
    // XButton.qml use "TapHandler", but its parent emit event, if its parent named with "xb_" and "track"(above checked)
    if(eM_objParentId.contains("xb_"))
    {
        if(eM_objParentId.contains("listview"))
        {
            // get "index" propertys to know which one
            index = eM_objParenContext->contextProperty("index").toInt();
            eM_objParentId.append("_" + QString::number(index));
            if(isPrintMsg_) qDebug() << " --- eM: xbutton in listview - pId" << eM_objParentId;
            sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objParentId, "");
            return false;
        }
        if(isPrintMsg_) qDebug() << " --- eM: xbutton - pId" << eM_objParentId;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objParentId, "");
        return false;
    }

    // XButton, its parent is the tracked id
    // XButton.qml use "TapHandler", but its parent emit event
    // XButton, but it defined MouseArea(), such as "xb_P00_goto_track"
    if(("xbutton_tapArea_track" == eM_objectId))
    {
        if(isPrintMsg_) qDebug() << " --- eM: xbutton pId" << eM_objParentId;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objParentId, "");
        return false;
    }

    // choise, itself is the tracked id
    // choise process above in "if(eM_objectId.contains("choise_tapArea_track"))"
//    if(eM_objectId.contains("ch_") && eM_objectId.contains("track")) // Choise id
//    {
//        // get its "currentIndex" to know which item is choiced
//        index = eM_context->contextProperty("currentIndex").toInt();
//        if(isPrintMsg_) qDebug() << " --- eM: choise Id" << eM_objectId << "- index" << index;
//        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], eM_objParentId, QString::number(index));
//        return false;
//    }

    // for debug
//    if(isPrintMsg_) qDebug() << " --- eM: other Id" << eM_objectId << "- pID" << eM_objParentId;

    if(isPrintPos_) { if(isPrintMsg_) qDebug() << " --- eM: pos" << QCursor::pos().x() << QCursor::pos().y(); }

    }

    // continue the event propagation
    return false;
}

eM_QGuiApplication::eM_QGuiApplication(int argc, char *argv[])
    : QGuiApplication(argc, argv)
{
}

eM_QGuiApplication::~eM_QGuiApplication()
{
}

bool eM_QGuiApplication::notify(QObject *obj, QEvent *event)
{
    eventMonitor::inst().eventFilter(obj, event);
    return QGuiApplication::notify(obj, event);
}

/* track and ID definition shall be clear in a doc somewhere
    sendTrackMsg() will send json msg to "xxx/log/xxxtracker/xxxtrack_log.xx"
    the process "xxxtracker" in AP will periodically(such as 8h) send its to cloud to visualization data
*/
void eventMonitor::sendTrackMsg(const int pageIndex, const QString& objectID, const QString& arg)
{
    if(elapsedTimer.restart() < 100) return ;
    qDebug() << " --- eM: sendTrackMsg() - page" << pageIndex << "- ID" << objectID << "- arg" << arg;
    QVariantMap trackMsgContent = {
        {"State", xxx->state()},
        {"pageIndex", pageIndex},
        {"objectID", objectID},
        {"arg", arg}
    };
    XXX.sendTrackerMsg("XXX_Track", trackMsgContent);
}

```



#### QML 附加属性

c++ 端添加附加属性，就是 qml 里面任何控件里面直接访问一个类（作为附加属性）的方法和读写其变量

https://stackoverflow.com/questions/14537193/attached-properties-in-qml

​	这个里面也提到，可以 `viewer->rootContext()->setContextProperty("MyPropClass", &myProp);` 来让 qml 全局可以访问 MyPropClass。

https://www.jianshu.com/p/36ea29750398

https://blog.csdn.net/gongjianbo1992/article/details/102029750

```c++
// eM_qmlAttachedProperties.h
#ifndef Track_H
#define Track_H

#include <QObject>
#include <QtQml>
#include <QElapsedTimer>

#include <QQmlEngine>

/* refer    https://stackoverflow.com/questions/14537193/attached-properties-in-qml
            https://www.jianshu.com/p/36ea29750398
            https://blog.csdn.net/gongjianbo1992/article/details/102029750
 * usage:
    in main() and before load qml
            qmlRegisterUncreatableType<Track>("Track", 1, 0, "Tk", \
                " --- eM_qAP: This is an abstract type that is only available as an attached property.");
        or
            #if isUITrack_eM_qAP
                Track::inst().Track_init("Track", "Tk");
            #endif

    in qml, for example: see "Track::processCaptureThings()" for detail
        in "Tk.c", must have "id" key and its string value must have "track"

        import Track 1.0

        xButton {
            id: xb_P00_XXXCtrl_track
            objectName: "xb_P00_XXXCtrl_track" // keep it as same as id
            ...
            onClicked: {
                Tk.c = {"id": objectName}
                or
                Tk.c = {"id": "xb_P00_XXXCtrl_track", "info": ""}
                or
                var str = string("key:%1, key2:%2").arg().arg()
                Tk.c = {"id": "xb_P00_XXXCtrl_track", "info": str}
            }
        }

        Choise {
            id: XXXLevelCh
            ...
            onCurrentIndexChanged: {
                Tk.c = {"id": "XXXLevelCh", "currentIndex": currentIndex}
            }
        }

        ZCheckBox {
            id: xcb_P13_XX_track
            ...
            onToggled: {
                Tk.c = {"id": "xcb_P13_XX_track", "checked": checked}
            }
        }

    for widget in listview: msuh have "id" and "index"
        XButton {
            id: xb_listview_P10_XXX_track
            ...
            onClicked: {
                Tk.c = {"id": "xb_listview_P10_XXX_track", "index": index}
            }

        XSwitchButton {
            id: xsw_listview_P10_XXX_track
            ...
            onToggled: {
                Tk.c = {
                    "id": "xsw_listview_P10_XXX_track",
                    "index": index,
                    "checked": checked }
            }
        }
*/

#define isUITrack_eM_qAP 1

class Track : public QObject
{
    Q_OBJECT
public:
    Q_PROPERTY(QVariantMap c READ captureThings WRITE setSaptureThings)
    Q_INVOKABLE void setTrackisEnable(bool isEnable);

    explicit Track(QObject *parent = nullptr);
    ~Track() override;
    static Track& inst();
    static Track* qmlAttachedProperties(QObject *object); // this class as Attached Properties

    void Track_init(QString libName, QString itemName);

    void setEnableQAP(bool isEnable);
    void setPrintMsg(bool isPrintMsg);

    QVariantMap& captureThings();
    void setSaptureThings(const QVariantMap& things);
    void processCaptureThings();

signals:
public slots:
    Q_INVOKABLE void sendTrackMsg(const int mainPageIndex, const int subPageIndex, const QString& objectID, const QVariantMap& arg);

private:
    QVariantMap captureThings_;
    bool isEnable_ = true;
    bool isPrintMsg_ = false;
    QElapsedTimer elapsedTimer;

    QObject* captureObject; // from "object" of qmlAttachedProperties(QObject *object)
//    QQmlContext* captureContext;
    QString captureObjectId;

    // json key deinfe
    const QString key_id            = "id";
    const QString key_info          = "info";
    const QString key_index         = "index";
    const QString key_checked       = "checked";
    const QString key_currentIndex  = "currentIndex";
    const QString key_argExtra      = "argExtra";

    const QString key_dialog_btn    = "dialog_btn";
    const QString key_dialog_text   = "dialog_text";
    const QString key_hms_btn       = "hms_btn";
    const QString key_hms_text      = "hms_text";

    const QString key_lang          = "lang";
};

// Makes the type Track known to QMetaType (for using with QVariant)
QML_DECLARE_TYPE(Track)
// declares that the Track supports attached properties.
QML_DECLARE_TYPEINFO(Track, QML_HAS_ATTACHED_PROPERTIES)

#endif // Track_H


// eM_qmlAttachedProperties.cpp
#include "Track.h"

#include <QDebug>

Track::Track(QObject *parent) : QObject(parent)
{
//    qDebug() << " --- eM_qAP: Track class constructor";
}

Track::~Track()
{
//    qDebug() << " --- eM_qAP: ~Track class destructor ";
    elapsedTimer.invalidate();
    isEnable_ = false;
    captureThings_.clear();
}

Track& Track::inst()
{
    static Track eM_qAP;
    return eM_qAP;
}

// run once when exec "Tk.c = {...}" in a different item in qml
Track* Track::qmlAttachedProperties(QObject *object)
{
    if(inst().isPrintMsg_) qDebug() << " --- eM_qAP: qmlAttachedProperties()" << object;
    inst().captureObject = object;
    return &(inst());
}

void Track::Track_init(QString libName, QString itemName)
{
    qmlRegisterUncreatableType<Track>(libName.toStdString().c_str(), 1, 0, itemName.toStdString().c_str(), \
        " --- eM_qAP: This is an abstract type that is only available as an attached property.");
}

void Track::setEnableQAP(bool isEnable)
{
    isEnable_ = isEnable;
}
void Track::setPrintMsg(bool isPrintMsg)
{
    isPrintMsg_ = isPrintMsg;
}

void Track::setTrackisEnable(bool isEnable)
{
    isEnable_ = isEnable;
}

QVariantMap& Track::captureThings()
{
    return captureThings_;
}

// run every time when exec "EM_qAPItem.captureThings = {...}" in qml
void Track::setSaptureThings(const QVariantMap& things)
{
    captureThings_ = things;
    processCaptureThings();
}

void Track::processCaptureThings()
{
    if(!isEnable_) return ;
    if(!captureObject) return ;

    // must have "id"
    if(!captureThings_.contains(key_id)) return ;

    captureObjectId = captureThings_[key_id].toString();
    // string value of key "id" must have "track"
    if(!captureObjectId.contains("track")) return ;

    // store page now at
    static int mainPageIndex = 0; // 0~4 indicate main page index
    static int mainPageSubPageIndex[5] = {0, 0, 1, 0, 0}; // mainPageSubPageIndex[mainPageIndex] indicate sub page index

    // get page
    if(captureObjectId.contains("xb_listview_xxx_track"))
    {
        // read its "index" property to locate which btn in a ListView
        mainPageIndex = captureThings_[key_index].toInt();
        if(isPrintMsg_)
            mainPageIndex ? (qDebug() << " --- eM_qAP: page switch" << mainPageIndex << mainPageSubPageIndex[mainPageIndex]) \
                : (qDebug() << " --- eM_qAP: page switch" << mainPageIndex) ;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "pageSwitch", {});
        return ;
    } else if(captureObjectId.contains("xb_listview_xxx_track")) // in BaseTabPage.qml
    {
        mainPageSubPageIndex[mainPageIndex] = captureThings_[key_index].toInt();
        if(isPrintMsg_)
            mainPageIndex ? (qDebug() << " --- eM_qAP: page switch" << mainPageIndex << mainPageSubPageIndex[mainPageIndex]) \
                : (qDebug() << " --- eM_qAP: page switch" << mainPageIndex) ;
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "pageSwitch", {});
        return ;
    }

    // language change
    if(captureObjectId.contains("LanguageChange_track"))
    {
        if(isPrintMsg_) qDebug() << " --- eM_qAP: languageChange" << "- lang" << captureThings_[key_lang].toString();
        captureThings_.remove(key_id);
        sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], "LanguageChange", captureThings_);
        return ;
    }

    if(captureObjectId.contains("listview") && captureThings_.contains(key_index))
    {
        captureObjectId = captureObjectId.append("_" + captureThings_[key_index].toString());
    }

    // get id, not used because for choise it come out others id, use "captureThings_.value("info").toString()" instead
//    captureContext = QtQml::qmlContext(captureObject);
//        if(!captureContext) return ;
//    captureObjectId = captureContext->nameForObject(captureObject);
//    if(captureObjectId.contains("listview")) { captureObjectId.append("_" + captureThings_["index"].toString()); }

    if(isPrintMsg_) qDebug() << " --- eM_qAP: obj id" << captureObjectId << \
                             "- info:" << captureThings_.value(key_info).toString()
                             << ", index:" << captureThings_.value(key_index).toString()                // for widget in listview
                             << ", checked:" << captureThings_.value(key_checked).toString()            // for switch or checkBox
                             << ", currentIndex:" << captureThings_.value(key_currentIndex).toString()  // for choose
                             << ", argExtra:" << captureThings_.value(key_argExtra).toString()
                             << ", dialog_btn:" << captureThings_.value(key_dialog_btn).toString()
                             << ", dialog_text:" << captureThings_.value(key_dialog_text).toString()
                             << ", lang:" << captureThings_.value(key_lang).toString();

    captureThings_.remove(key_id);
    sendTrackMsg(mainPageIndex, mainPageSubPageIndex[mainPageIndex], captureObjectId, captureThings_);
}

/* track and ID definition shall be clear in a doc somewhere
    sendTrackMsg() will send json msg to "userdata/log/tracker/track_log.xx"
    the process "tracker" in AP will periodically(6h) send its to cloud to visualization data
    immediately trigger "tracker" to send its to cloud cmd: touch /tmp/tracker_debug
*/
void Track::sendTrackMsg(const int pageIndex, const QString& objectID, const QVariantMap& arg)
{
    if(elapsedTimer.restart() < 100) return ;
    if(isPrintMsg_) qDebug() << " --- eM: sendTrackMsg() - page" << pageIndex << "- ID" << objectID << "- arg" << arg;
    QVariantMap trackMsgContent = {
        {"State", XXX->state()},
        {"PageIndex", pageIndex},
        {"objectID", objectID},
        {"args", arg}
    };
    XXX.sendTrackerMsg("XXX_Track", trackMsgContent);
}
```



qt 新版本 5.15 以上的方法，用到两个类 https://blog.csdn.net/baidu_41388533/article/details/117091443，这个挺好~

​	一个类 info 存储信息，一个类 person 对外提供调用（实现 `qmlAttachedProperties()` 里面 返回 new info 类，用 `QML_ATTACHED(Info)` 让 person 类 可以访问 info 类成员），main.c 在 load qml 之前 注册 `qmlRegisterUncreatableType<Person>()`，qml 里面 运行到 该附加属性的时候，先调 `qmlAttachedProperties()`，即 new info 类，即 qml 里面 每一个控件 对应一个 info 类，用 Person 附加属性 调 info 的成员 进行读写，如 `Person.name: ...` 或 `Person.name = ...`。



#### UI 埋点

加埋点，用户行为统计。下面是笼统的概念介绍

- https://blog.csdn.net/weixin_39614276/article/details/111437770

- https://www.xiaohongshu.com/explore/63bbe67c000000002203688c

  > 认识B端｜前端需求埋点
  >
  > 👉埋点流程👈
  >
  > 01选择埋点类型
  >
  > 一般分为页面埋点、模块埋点、组件埋点、其他类型埋点
  >
  > 02编辑埋点信息
  >
  > 填写需求名称、prd链接、需求描述、预计上线版本等信息
  >
  > 03需求提审
  >
  > 埋点需求制作完成后，点击提交审核，生成审批工单给数仓审核
  >
  > 04需求开发
  >
  > 需求审核通过后，可以分享需求链接给开发同学进行开发
  >
  > 05需求验证
  >
  > 对埋点需求进行验证，验证埋点需求的正确性
  >
  > 06需求上线
  >
  > 需求开发完成并且验证没有问题后，点击需求上线，就可以开始分析数据了
  >
  > 🚗前端埋点类型:
  >
  > 1.页面埋点:发生在页面上，在页面加载完成后触发或在页面退出时触发的埋点事件。
  >
  > 2.模块埋点:发生在单个页面的某个模块上点击和曝光的埋点事件，例如:按钮、图片、弹窗、浮层等。
  >
  > 3.组件埋点:发生在某个模块上且该模块被多个系统页面重复使用，营销大转盘。
  >
  > 4.其他埋点:发生在更多其他类型事件模版，例如:视频播放结束事件、扫码事件、蓝牙事件等。
  >
  > 🚕变量命名规范
  >
  > 1)统一遵循小驼峰的命名规范:除第一 个单词之外，其他单词首字母大写;
  >
  > 2)统一格式为{业务}_ {组件|页面}_ {具体元素}， 比如finance_ .qualityHomePage_ repay;
  >
  > 🚙触发时机说明
  >
  > 1)浏览/pageview:采集用户浏览页面相关的数据，用户打开该页面即会被记录一次;
  >
  > 2)点击/click: 采集用户的点击行为相关的数据，用户点击页面上某个按钮会被记录一次;
  >
  > 3)曝光/expose:采集某个页面/模块被看到的数据，用户有效浏览页面/模块会被记录一次;

- 3种前端埋点方式 https://blog.csdn.net/LuckyWinty/article/details/130939489

  > 最直接有效的方式就是了解用户的行为，了解用户在网站中做了什么，呆了多久。
  >
  > `所谓'埋点'是数据采集领域（尤其是用户行为数据采集领域）的术语，指的是针对特定用户行为或事件进行捕获、处理和发送的相关技术及其实施过程。. 比如用户某个icon点击次数、观看某个视频的时长等等`。
  >
  > 基于此我们可以知道埋点是实际上是对特定事件或者行为的数据监控和上报。

- 前端数据打点（埋点） https://blog.csdn.net/m0_70190404/article/details/128477172

- 前端埋点实现方案 https://huaweicloud.csdn.net/639fe937dacf622b8df8faa8.html

  > 埋点就是在应用中特定的流程收集一些信息，用来跟踪应用使用的状况，后续用来进一步优化产品或是提供运营的数据支撑，包括访问数（Visits），访客数（Visitor），停留时长（Time On Site），页面浏览数（Page Views）和跳出率（Bounce Rate）。这样的信息收集可以大致分为两种：页面统计（track this virtual page view），统计操作行为（track this button by an event）。
  > 
  >
  > 两方面上报: 1.事件上报(目前只有点击事件埋点)，2.停留时间上报
  >
  > - **事件上报**：通过给元素绑定自定义指令的方式实现(减少对原有代码的侵入)🍜，将信息[存储](https://activity.huaweicloud.com/free_test/index.html?utm_source=hwc-csdn&utm_medium=share-op&utm_campaign=&utm_content=&utm_term=&utm_adplace=AdPlace070851)在缓存池中定时上报，上报之后清空之前的上报信息🥠。
  > - **停留时间上报**：需要重新封装路由，创建路由拦截在跳转之前记录来源,以及上一个页面的停留时间，当拦截器捕获成功之后🌯，如果发现停留时间大于xx秒进行上报🥙。




原始 背景 和 需求：

1. 用户行为统计，收集用户习惯，比如点击顺序或者点击热点。
2. 目前设计比较复杂，找出用户不常用的，看是不是设计有问题。
2. 打埋点的地方，同时也输出到调试日志。



下面是细化：

埋点类型，可以用 event 区分下面这些 类型事件 的发生：

- 页面切换（当前页面的字符串变量发生变化时记录，确保跟UI显示的一致）。
  - 记录当前所在页面，记录切换到了哪个页面。

- 点击按键（点击时记录）。
- 点击选择框 和 开关（点击后记录点击后控件的开关状态）。
- 选择下拉框（点击下拉框 + 选择的项，点击后记录）。
- 合并按键，一个区域的所有按键任何一个点击当作同一个。
  - 给这些在一个区域的控件再添加新的 subName 都保持一样，这样能筛选出来。

- 弹窗中的按键（比如点击格式化后的弹窗）。
  - 记录当前点击的弹窗中的按键或其它类型控件。
  - 每个弹窗有个 独一无二 的 id，当作区分弹窗。

- 操作链（10秒间隔 或 50次操作间隔），前两种，量大了会看出趋势。
- 具体的一些关键操作统计，包含一些列特定的操作，或者完整的打开和关闭了某一个设置页面（包括停留时间），编程需要根据一些列特定事件才算计数加一。
- 语言切换（切换事件时记录）。
- 页面停留时间。
  - 一级页面 和 二级页面 切换之间的停留时间。
  - 各种弹出子页面，即特定的按键和返回按键（两个按键 id 做成一对，方便识别），两个点击事件之间的时间，可由处理埋点信息端计算。
- 开机事件。
- 开始升级，结束升级。
- qml 控件中其它信息，可以任指定。



需要上报的信息：

在 C++ 端写统一调用的函数，并设计一个是否埋的开关。打埋点的地方，同时也输出到调试日志。

埋点的控件，发生点击等事件后，上报的信息：

json 例子：

```json
{ "evt":"jMachine_UITrack",
    "content":{
        "event":<"pageBtn","btn","checkBox","switchBtn","choise","dialogBtn","operationChain">,
        // 一级页切换按键、按键、选择框 / 开关、下拉框、弹窗中的按键、操作链上报事件
        
        "id":"...",
        
        "choiseIndex":x,      // 对于 event 为 choise 时候才有，选择了第几项
        "checked":true/false, // 对于 event 为 checkBox 或 switchBtn 时候才有，开了还是关了
        
        "dialogType":"xxx"，  // 对于 event 为 dialogBtn 时候才有，这个弹窗的类型，错误、警告、提示 等
        "dialogId":"xxx",     // 对于 event 为 dialogBtn 时候才有，这个弹窗的唯一 id，文案唯一对应的 编号 或缩减字符串
        
        "extraInfo":{...},    //自定
         
        "pageName":"xxx",     // 发生事件时候所在页面
        "State":x,       // 机器单当前所在阶段，状态机所在状态 空闲、工作中、暂停等。
 
        "lang":"en/zh-cn/de/...",
        "sn":xxx,             // 机器唯一序列号
        "time":xxx,
    }
}

// 还有记录一整个状态变化之中，所发生事件的计数
// 比如：开始工作 → 成功完成工作：start (state 从 1 到 2) → complete (state 从 2 到 1)
"control":"wholeEvent","beginStage:1,"endStage":2,"id":"skipBtn","times":0,...
```



要埋点的控件 id 命名规范：

- id 命名 有一定的 可辨识的含义。
- 没有特别限制，保证在一个 UI 页面里面的所有控件 id 不重复即可。
- 类型 控件，推荐尽量在 id 加个类型尾缀，比如有 xxxRect，xxxBtn，xxxImage，xxxText，xxxListView，xxxModel，xxxDeleComp 等。



方案：

**第一种：eventMonitor。为了便于埋点，减少侵入 qml 代码，给特定的控件添加埋点功能，按照 一定的 控件 id 命名规范，区分开控件即可**

参考 `QT 事件传播链 / 加事件过滤` 

但是存在的问题分析，见里面。

https://www.xjishu.com/zhuanli/55/202110265850.html

https://cprs.patentstar.com.cn/Search/Detail?ANE=9FHF1ABA8CEA9HHG4DAA8FDA7AFA9BCA9HCFEGHA9AFB9HFD

**第二种：qmlAttachedProperties。在 qml 文件头 引用库 “import Track 1.0” 之后在要埋点的控件的 响应槽函数里面添加 “Tk.c = {"id": xxx} ” 即表示上报 这个控件的 xxx 属性**

UI 工程的 界面控件一般都是使用 自己封装 qml 原生控件 的 定制基础控件，在定制基础控件里面埋点，再向上找所有 parent 来找界面控件的 id 和所在页面，合成 id，也可以不合成，上报信息的时候信息全一些就行。

附加属性机制对于有定制基础控件的 qt 工程方便实施，但有个缺陷，就是qml中按键执行 onclicked() 和 后端 执行收集信息 可能是并发进行的，若采集信息里面包含 onclicked() 里面设置的变量，那么前后行为不确定，这个可以通过在 里面 onclicked() 合适的位置 直接给附加属性赋值来解决，这又变成挨个加，分散到业务代码里；而 eventFilter 不会有这样问题，一个事件会先进入 eventFilter() 函数再 执行 按键的 onclicked()，前后行为确定。



其它方法，但不实际用。

- 法3：（挨个添加）官方工具 Qt Insight 等，可以轻松实现埋点和跟踪，首先需要钱，其次上传的云端也是 qt 指定的平台 https://insight.qt.io。

  https://www.qt.io/product/insight/onboarding-instructions

  Qt Insight 的使用 需要 Qt 企业账户（若 app 商用也许会被检测到）。

  Qt 官方规定使用 Qt Insight 上传用户数据，需要在 app 界面上 加一个关闭开关。https://www.qt.io/terms-conditions/terms-of-use-qt-insight-tracker-library

  Qt Insight 作为库使用：

  > ##### **Availability**
  >
  > **Qt 6.5-beta3 (available now)**
  >
  > Qt Insight Tracker library can be installed with [Qt Installer](https://account.qt.io/s/downloads) by selecting Custom Installation -> Qt -> Qt 6.5.0-beta3 -> Additional Libraries -> Qt Insight Tracker
  >
  > **Qt 6.2.8 (coming in March 2023)**
  >
  > **Qt 5.15.14 (coming in May 2023)**

  Qt Insight 在 Qt Design Studio 里面可以直接 作为组件 用起来。

  在 qt creater 里面，在 c++ 类 或 qml 来使用 qt insight ，需要单独给每个 按键 / 鼠标区域 添加 `InsightTracker.sendClickEvent()`，仍然不是统一加的方法。



#### Qt显示中文问题

根上讲编码 https://blog.csdn.net/m0_46577050/article/details/133804929

直接的方法 https://blog.csdn.net/yiyiyayade_niu/article/details/129393525

```c++
// 1 std::string 转 QString

std::string s = "乱码";
QString qs=QString::fromLocal8Bit(s.data());

// 2 QString 转 std::string

QString s = "乱码";
std::string str = std::string(s.toLocal8Bit());
```



## 具体控件积累

*p.s 下面会贴一些关键代码。*

*p.ss 所遇问题日常添加在此，且顺序无关，按需去看即可*



### QT 实用类 集合

#### QFlags

对 enmu 例化一个变量，用 setFlag()、testFlag() 等 增减 enmu 项，还有其它 操作符重载，是一个安全、好用的工具。

```c++
enum Flag {
    A = 1,
    B = 1 << 1,
    C = 1 << 2,
    ...
};

Q_DECLARE_FLAGS(Flags, Flag)
Q_FLAG(Flags) // for Qt Script or edited in Qt Designer

Flags flag_ = nullptr;

flag_.testFlag(A);
flag_.setFlag(B, true / false);

```



#### QElapsedTimer

好用，比如 `if(elapsedTimer.restart() < 50) return ; // max 20hz operate`。



#### qAsConst

要处理某个信息时候，防止篡改



#### QSharedPointer



#### QCache



### qDebug() 重定向

https://cloud.tencent.com/developer/article/1930475

通过 qInstallMessageHandler() 设置重定向数据的去向



### 获取自身 内存占用 和 CPU 使用率

https://www.5axxw.com/questions/simple/tfvpez

```c++
// 内存占用获取
// 这个写的并不优雅， 直接用 pmap 命令的返回信息（如下） 比较大 而且是 RSS，需要的是 PSS 或者 USS。
#include <QProcess>
qint64 processId = QCoreApplication::applicationPid(); //获取当前进程的PID
QStringList arguments;
arguments << QString::number(processId);
//执行命令"pmap -x <processId>"，获取当前进程的内存映射
QProcess p;
p.start("pmap", arguments);
p.waitForFinished(); //等待命令结束
QString result = QString(p.readAllStandardOutput());
QStringList lines = result.split('\n');
qint64 memoryUsage = 0;
for (QString line : lines) {
    QStringList tokens = line.split(' ', Qt::SkipEmptyParts);
    if (tokens.length() >= 3) {
        qint64 size = tokens.at(1).toLongLong(nullptr, 16);
        memoryUsage += size;
    }
}
qDebug() << "Memory usage:" << memoryUsage / 1024 << "KB";

// CPU 使用率
#include <QThread>
int cpuUsage = qBound(0, qRound(QThread::currentThread()->cpuUsage() * 100), 100);
qDebug() << "CPU usage:" << cpuUsage << "%";
```



### 添加 icon 图标

给可执行文件 添加 icon 图标

​	https://www.cnblogs.com/maijin/p/17264089.html



### MouseArea / TapHandler

MouseArea

​	https://waleon.blog.csdn.net/article/details/129252688

​	https://blog.csdn.net/kingzhou_/article/details/128193953 QML事件处理之鼠标事件（MouseEvent）和滚轮事件（WheelEvent）



TapHandler

https://blog.csdn.net/u011942101/article/details/122433972

> TapHandler有效敲击手势的检测取决于gesturePolicy。默认值为DraggThreshold,它要求按下和释放键在空间和时间上都紧密靠近。



### 动态 创建 / 加载组件

QML 中如何动态创建组件：**ViewList**，**Loader**，createObject / createQmlObject
	https://blog.csdn.net/m0_73443478/article/details/129844157

> 当Loader的source或sourceComponent属性发生变化时，它之前加载的Component会自动销毁，新对象会被加载。
>
> Loader的item属性指向它加载的组件的顶层Item。对于Loader加载的Item，它暴露出来的接口，如属性、信号等，都可以通过Loader的item属性来访问。

Loader 有一个 Loaded 信号，可以用。

Component 一般用于新定义一个组件，单个文件的（需要id与文件名一致，且文件名首字母大写）或者定义在一个文件里面，其下就一个 id 属性 和 item{ ... }。

> 如果Loader加载的Item想处理按键事件，那么必须将Loader对象的focus属性设置为true（注，不是必须，根据自己工程情况多调试试试）。又因为Loader本身也是一个焦点敏感的对象，所以如果它加载的Item处理了按键事件，则应当将事件的accepted属性设置为true，以免已经被吃掉的事件再传递给Loader。



### ListModel & ListView

​	https://blog.csdn.net/u011942101/article/details/115050458



若 ListView 数据来自 c++ 后端，则在 其 delegate 的 Component 里面引用 Model 数据应该用 `modelData.xxx`。



在 delegate 里面 可以使用 附加属性的一些信息 `delegate的component的item.ListView.view` 等等，看手册即可



Qml ListView 的 组件里面包含 下拉框 ComboBox，将下拉框内的文本也放入 ListModel 里面
	https://qa.1r1g.com/sf/ask/3160982681/



Qml ListView 动画
	https://gongjianbo1992.blog.csdn.net/article/details/109713124
	https://blog.csdn.net/m0_60259116/article/details/129336808



Repeater
	https://blog.csdn.net/qq_26611129/article/details/113933202
	https://blog.csdn.net/aoiyoru/article/details/128202698
	https://www.python100.com/html/89698.html
	使用Repeater时的注意事项：总的评价：不如 ListView
	Repeater在第一次创建时会创建其所有委托项。如果存在大量的委托项，并且不是所有的项都需要同时可见，那么这么做效率可能会很低。如果是这种情况，请考虑使用其他视图类型，如ListView（它仅在将委托项滚动到视图中时创建委托项），或者根据需要使用动态对象创建方法来创建委托项。



### 信息打印

QML 打印信息：

​	https://blog.csdn.net/kenfan1647/article/details/122013713



c/c++ 端 定义，QML 端调用：

不用多色，就 [info]、[warn]..

```c++
void XXX::log_msg(QString id, QString msg)
{
    qDebug() << "msg" << id << ":" << msg;
}

// 多色打印可以参考 https://zhuanlan.zhihu.com/p/331847712
// 但是 不是所有 cmd 都支持显示彩色 log 的，如果不支持从而显示原生字符则会显得很乱
void XXX::log_info(QString id, QString msg)
{
    qInfo() << "\033[0;" "34" ";m" "- info" << id << ":" << msg << "\033[0m";
}

void XXX::log_warn(QString id, QString msg)
{
    qInfo() << "\033[0;" "33" ";m" "- info" << id << ":" << msg << "\033[0m";
}

void XXX::log_crit(QString id, QString msg)
{
    qWarning() << "\033[0;" "1" ";" "31" ";m" "- info" << id << ":" << msg << "\033[0m";

}

/*
    qml usage：
    property var lm: XXX.log_msg
    property var li: XXX.log_info
    property var lw: XXX.log_warn
    property var lc: XXX.log_crit

    // fill "c++ function or qml object id"(when use in c file) and msg
    lm("<c++ function or qml object id>", "msg...")
    li("fun 1", "msg...")
    lw("qml obj", "msg...")
    lc("id 3", "msg...")
*/
```



### 模拟点击 / 随即点击

问 chatGPT 给的

```c++
#include <QCoreApplication>
#include <QMouseEvent>
#include <QApplication>
#include <QWidget>
#include <QRandomGenerator>
#include <QTimer>

void simulateClick(QWidget* widget, const QPoint& pos)
{
    QMouseEvent pressEvent(QEvent::MouseButtonPress, pos, Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::postEvent(widget, &pressEvent);

    QMouseEvent releaseEvent(QEvent::MouseButtonRelease, pos, Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::postEvent(widget, &releaseEvent);
}

void performMonkeyTest(QWidget* widget)
{
    QTimer* timer = new QTimer(widget);
    QObject::connect(timer, &QTimer::timeout, [widget]() {
        int x = QRandomGenerator::global()->bounded(widget->width());
        int y = QRandomGenerator::global()->bounded(widget->height());
        simulateClick(widget, QPoint(x, y));
    });

    // 设置定时器间隔，单位是毫秒
    timer->start(1000); // 每秒模拟一次点击
}

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    // 创建一个窗口
    QWidget widget;
    widget.setGeometry(100, 100, 300, 200);
    widget.show();

    // 执行 Monkey 测试
    performMonkeyTest(&widget);

    return a.exec();
}

```



### 多页面切换

https://blog.csdn.net/weixin_34290631/article/details/86364900

就推荐用两种：

1. Component 组件的 `object createObject(QtObject parent, object properties)` 方法。
2. Loader，设置 `.source = xxx.qml` 或者 `.sourceComponent  = xxx` 创建，设置 `.source = “”` 销毁。



其它：StackView、SwipeView，是特定场景用：

- StackView 可以用于 进入多个 一连串的 子页面（push()），而且还要逐一返回（pop()），可以进入一个临时的设置或展示用的子页面，然后按键返回退出（才能释放）

- SwipeView 相当于 一系列 引导页面，逐个过，这种场合。




### QT 多线程

> QThread有两种用法：
>
> 1、（推荐）写一个QObject子类A，实例化之，再实例化一个 Qthread 类 的 示例 AQthread，A.moveToThread(&AQthread)，然后运行线程，AQthread.start()，调用 类A 里的函数即在 Qthread 线程里运行。
>
> 2、子类化一个QThread，然后实现run()虚函数
>
> 然后使用 thread->start(); 来启动 线程

https://blog.csdn.net/zz_6_3/article/details/109399098

https://blog.csdn.net/qq_40041064/article/details/114921026



QThread 相关 API

https://betheme.net/dashuju/23242.html?action=onClick



法1 的例子，可以看 正点原子的 QT 教程 手册，第十章 多线程。

法2 的例子：

```c++
// simpleQThread.h

#ifndef WORKERQTHREAD_H
#define WORKERQTHREAD_H

#include <QObject>
#include <QThread>
#include <QDebug>

class simpleQThread : public QThread
{
    Q_OBJECT
public:
    simpleQThread();
    simpleQThread(std::function<void ()> &action);
//    ~workerQThread();

    void run() override;
    void postRunFn(std::function<void ()> &action);

signals:

public slots:

private:
    std::function<void ()>* action_;
};

#endif // WORKERQTHREAD_H


// simpleQThread.cpp

#include "simpleqthread.h"

simpleQThread::simpleQThread()
    : action_(nullptr)
{
}

simpleQThread::simpleQThread(std::function<void ()> &action)
    : action_(&action)
{
}

void simpleQThread::postRunFn(std::function<void ()> &action)
{
    action_ = &action;
}

void simpleQThread::run()
{
    (*action_)();
}


// 使用例子：

std::function<void ()> abc(
    []() -> void {
        while(1)
        {
            QThread::sleep(1);
            qDebug() << "---------------------------";
        }
    });

simpleQThread* abcQThread = new simpleQThread(abc);
abcQThread->start();
```



### 延时

（纯 C++）

这些会阻塞当前线程，如果只有一个线程，那么其它地方将不响应。

​	https://blog.csdn.net/qq_36659059/article/details/118521190

- 多线程 程序使用`QThread::sleep()`， `QThread::msleep(1000)`。

- 使用 `QEventLoop`。

  ```c++
  void Widget::Sleep(int msec)
  {
  	QTime dieTime = QTime::currentTime().addMSecs(msec);
  	while( QTime::currentTime() < dieTime ){}
  	QCoreApplication::processEvents(QEventLoop::AllEvents, 100);
  }
  ```

- 用 QEventLoop + QTimer::singleShot https://it.cha138.com/nginx/show-3077466.html

  ```c++
  QEventLoop eventloop;
  QTimer::singleShot(100, &eventloop, SLOT(quit()));
  eventloop.exec();
  ```



### 文件读写

（纯 C++）：QFile 类

​	https://blog.csdn.net/QtCompany/article/details/130691341 （API 介绍）

​	https://blog.csdn.net/weixin_44618297/article/details/123538302（API 介绍）

​	https://blog.csdn.net/QtCompany/article/details/131013800 （C++写成类库，qmlRegisterSingletonType，qml调用）

​	https://blog.csdn.net/wangpailiulanqi8/article/details/125926116（C++写成类库，qmlRegisterSingletonType，qml导入再调用）



### 文件浏览

c++ 和 qml

https://blog.csdn.net/u011942101/article/details/124220963

https://www.cnblogs.com/listensong/p/4202039.html



这个用到的数据结构比较多

https://blog.csdn.net/qq_26611129/article/details/116997082



纯 c++，使用 QTreeView

https://www.cnblogs.com/wanghongyang/p/15017253.html



### 网络

http requst（纯 C++）



用信号、槽方式异步等待，建议需要搭配多线程使用

https://download.csdn.net/download/one_l_star/10472150

```c++
#include <QNetworkAccessManager>
#include <QNetworkRequest>
#include <QNetworkReply>
#include <QUrl>

#include <QEventLoop>

manager = new QNetworkAccessManager(this);

QObject::connect(manager, SIGNAL(finished(QNetworkReply*)), \
				this, SLOT(onQNetworkReplyFinished(QNetworkReply*)));
// 要把 onQNetworkReplyFinished() 函数放入 public slots

QNetworkReply *reply = manager->get(QNetworkRequest(QUrl(url)));

void Translator_baidu::onQNetworkReplyFinished(QNetworkReply* reply)
{
    QString response_json = reply->readAll(); // json format
    qDebug() << "response_json: " + response_json;
}
```



用事件循环方式 QEventLoop 同步等待，推荐

https://blog.csdn.net/QtCompany/article/details/129282296

```c++
manager = new QNetworkAccessManager(this);

QEventLoop eventLoop;

QNetworkReply *reply = manager->get(QNetworkRequest(QUrl(url)));

// 网络 http get 方法，同步方式
connect(reply, SIGNAL(finished()), &eventLoop, SLOT(quit()));
eventLoop.exec();       // block until finish

// 错误处理
if (reply->error() != QNetworkReply::NoError)
{
    qDebug() << "err request protobufHttp";
    dst = ""; return dst;
}

// 接收
QByteArray response_json = reply->readAll(); // json format
qDebug() << "response_json: " + response_json;
```



用 while() 死等方式同步等待，不推荐

https://blog.csdn.net/m0_73443478/article/details/130305415



### Json 构造、解析

（纯 C++，后面有 qml 的）

​	https://blog.csdn.net/weixin_46068274/article/details/127808897（例子）

```c++
#include <QJsonDocument>
#include <QJsonParseError>
#include <QJsonObject>
#include <QJsonValue>
#include <QJsonArray>

/*
    输出举例
    正确回复：
    {
        "from": "en",
        "to": "zh",
        "trans_result": [
            {
                "src": "apple",
                "dst": "苹果"
            }
        ]
    }
    异常回复：
    {
        "error_code": "54001",
        "error_msg": "Invalid Sign"
    }
*/

// 处理 json，提取 翻译结果
QJsonParseError jsonError;
QJsonDocument doc = QJsonDocument::fromJson(response_json, &jsonError);

if (jsonError.error != QJsonParseError::NoError && !doc.isNull())
{
    qDebug() << "err Json Parse " << jsonError.error;
    dst = ""; return dst;
}

QJsonObject rootobj = doc.object();
if(rootobj.contains("error_code"))
{
    qDebug() << "err trans, error_msg: " << rootobj.value("error_msg").toString();
    dst = rootobj.value("error_msg").toString(); return dst;
}
QJsonArray  trans_result = rootobj.value("trans_result").toArray();
QJsonValue dst_ = trans_result.at(0).toObject().value("dst");

dst = dst_.toString();
```

​	https://blog.csdn.net/weixin_43729127/article/details/127522889（API 罗列）

​	https://blog.csdn.net/qq_44632658/article/details/127539003（API 罗列）

​	https://blog.csdn.net/My_class2233/article/details/125674115（API 罗列）



qt 里面，构造 json 可以用更方便的 QVariantMap

```c++
#include <QVariantMap>
#include <QJsonDocument>
#include <QJsonObject>

QVariantMap params = {
	{"content", 123},
    {"id", "abc"},
    ...
};

QJsonObject json = QVariant(params).toJsonObject();
QByteArray json_str = QJsonDocument(json).toJson(QJsonDocument::Compact);
```



qml 里面解析 json

使用 JSON 对象，它包含两个函数，parse() 和 stringify()。



### 颜色表示法

QML 颜色表示法

​	https://waleon.blog.csdn.net/article/details/129230582



### qt 定时器



继承自 QObjec 的类，QObject 还带有 timerEvent() 虚函数可以用，子类中实现该函数，再可以在构造函数里面 startTimer(xxx) 即可。

https://www.ngui.cc/el/3202953.html?action=onClick



qml 定时器

https://waleon.blog.csdn.net/article/details/129340128



### qt 测量时间

提供了很多种方法 QTime、struct timeval & gettimeofday()、clock() 等等。

https://blog.csdn.net/hebbely/article/details/78953318



QElapsedTimer

https://blog.csdn.net/lengyuezuixue/article/details/79996209




### 单击显示坐标

在 qml 的 root 控件 的 最后添加，且 其中设置 `mouse.accepted = false` 表示当前控件不接收 这个 事件，让其继续传递给其它控件，这样不会影响其它控件 相应 鼠标事件！`preventStealing: true` 和 `propagateComposedEvents: true` 同理。

```js
    MouseArea {
        id: findCurrentObj
        objectName: "MouseArea_findCurrentObj"
        anchors.fill: parent
        preventStealing: true
        propagateComposedEvents: true
        onPressed: {
            findPointObj(mouseX, mouseY)
            mouse.accepted = false
        }
        onReleased: { mouse.accepted = false }
        onClicked:  { mouse.accepted = false }
    }

    property var obj: screen

    function findPointObj(mouseX, mouseY) {
        console.log(" —————————— pressed at:   " + mouseX + "   " + mouseY)
        var obj = screen.childAt(mouseX , mouseY)
        if(obj)
            console.log(" —————————— " + obj.objectName)

//        console.log(point_.x, point_.y)
//        console.log(childAt(point_.x, point_.y))
    }
```



### 多点触摸控件

qml MultiPointTouchArea 控件

https://blog.csdn.net/u014491932/article/details/124969522



c++ 中可以用 QTouchEvent，转换 event 为 QTouchEvent，再获取多点



### encodeURI()

```js
var uri = "http://www.baidu.com/s?wd=KatieMelua";
var encodedUri = encodeURI (uri);
var encodedComponent = encodeURIComponent(uri)
console.log (encodedUri);
console.log(encodedComponent);

var decodedUri = decodeURI (encodedUri);
var decodedComponent = decodeURIComponent(encodedComponent)
console.log (decodedUri);
console.log(decodedComponent);

/*
    encodeURI()方法用于处理完整的URI(例如http://www.pingwvest.com/abc def.html),而
    encodeURIComponent()用于处理URI的一个片段(如 abc def.html)。两者的主要区别是,
    encodeURI()方法不对URI中的特殊字符进行编码,如冒号、前斜杠、问号等;而
    encodeURIComponent()则对它发现的所有非标准字符进行编码。通常我们使用encodeURI()
    处理完整的URI,使用encodeURIComponent()处理附加在已有UR1末尾的字符串
*/
```



### 控件对应 C++ 原型

打印 qml 里面控件的 id，会打印该控件对应的 C++ 的类的名字，在 qt 源码中可以找到 该控件的 C++ 实现，里面有对应的 属性、信号 等的定义~。若含有 QMLTYPE 字样，则该控件是 qml 中定义的控件。

```js
Component.on Completed:{
    console.log("QML Text\'s C++ type - ", text1)
    console.log("QML Button\'s C++ type - ",buttonl);
    console.log("QML Image\'s C++ type - ", imagel)
}
```



### 键盘事件

QML 键盘事件

​	https://waleon.blog.csdn.net/article/details/129309600



### 快捷键

QML 快捷键（Shortcut、Keys）
	https://blog.csdn.net/gongjianbo1992/article/details/116954979



### 输入组件 / 文本块显示

> 行编辑 Textlnput 与 TextField
>
> 文本块 TextEdit 与 TextArea

TextEdit 是 Textlnput 的升级，TextArea 是 TextField的升级。TextEdit 与 TextArea 具有 指定文本格式、内容的语法高亮、如何折行、提供 API 编辑其内容，背景可以更改 等等。

> TextEdit可定制cursor，与TextInput类似，TextEdit也有cursorDelegate属性，TextArea 没有。
> TextArea支持文本滚动，这是TextArea的大招啊，你什么都不用做，它就可以支持上下方向键(非只读模式)、翻页键以及鼠标中键的滚动，因为它继承自ScrollView。



QML 基本文本输入组件TextInput、TextField、TextEdit、TextArea
	https://blog.csdn.net/gongjianbo1992/article/details/101156110



Qml 输入框 的 validator 属性
	https://www.rstk.cn/news/722557.html?action=onClick
	其中 RegExpValidator 字符串验证用 JavaScript 正则表达式写： https://www.runoob.com/jsref/jsref-obj-regexp.html
	QML设置IP输入验证 https://blog.csdn.net/joyopirate/article/details/110167359



### 虚拟键盘

​	https://www.cnblogs.com/linuxAndMcu/p/13667894.html



### 读 Excel 表格

（纯 C++，使用 QAxObject 类）

​	https://blog.csdn.net/didi_ya/article/details/120208099（基础 API 介绍）



### 调用 SQLite

QML 保存用户配置，调用 SQLite
	https://waleon.blog.csdn.net/article/details/132073943



### 动画

Qml 动画

​	https://blog.csdn.net/Mr_robot_strange/article/details/126522600
​	https://zhuanlan.zhihu.com/p/564072781
​	https://blog.csdn.net/wenxingchen/article/details/128522558



点击后移动效果，比如输入框点击之后 动画移动 x,y 到屏幕中上方（也可以再加个背景框和文字标题），以避免弹出虚拟键盘后遮挡原来位置的输入框。

```js
        onPressed: {
            isInputting = true; z = 3
            // 点击后输入框飞到屏幕中上，键盘不会遮挡
            if(!isTextFieldAnimationMove) {
                x = 280
                y = 70
            }else {
                animation_x_go_textField_Domain_name.running = true
                animation_y_go_textField_Domain_name.running = true
            }
        }

        onEditingFinished: {
            isInputting = false; z = 1
            ca_certiInputModel.set(0, {text: textField_Domain_name.text.toString()});
            // 输入完成后回到原位
            if(!isTextFieldAnimationMove) {
                x = 629
                y = 172
            }else {
                animation_x_back_textField_Domain_name.running = true
                animation_y_back_textField_Domain_name.running = true
            }
        }

        PropertyAnimation on x { easing.type: Easing.OutQuad
            id: animation_x_go_textField_Domain_name; to: 280
            duration: 300; running: false }
        PropertyAnimation on y { easing.type: Easing.OutQuad
            id: animation_y_go_textField_Domain_name; to: 70
            duration: 300; running: false }

        PropertyAnimation on x { easing.type: Easing.OutQuad
            id: animation_x_back_textField_Domain_name; to: 629
            duration: 300; running: false }
        PropertyAnimation on y { easing.type: Easing.OutQuad
            id: animation_y_back_textField_Domain_name; to: 172
            duration: 300; running: false }
```



### 绘图

绘图 Shapes Canvas 

​	https://blog.csdn.net/qq_21438461/article/details/130464717

​	Shapes：https://blog.csdn.net/xiaoyu21520/article/details/130890829

​	Canvas：https://waleon.blog.csdn.net/article/details/131254637



### 显示网页

Qml 显示网页

​	WebEngineView

​		说明：QtWebEngine  使用了使用 LGPLv2.1 协议的 的三方组件，且只能用 MSVC 编译

​		https://zhuanlan.zhihu.com/p/623440635	看这个就可以跑起来了

​		https://zhuanlan.zhihu.com/p/616392695

​		https://www.cnblogs.com/judes/p/15641582.html

​		http://www.xn.bslzg.com/userblog/onenews.aspx?blog_news_nodeuuid=16483762468210000003000

​		https://blog.csdn.net/u013352076/article/details/121016093

​	WebView

​		https://www.elecfans.com/d/2088103.html

​		https://doc.qt.io/qt-5/qml-qtwebview-webview.html#details



### 程序打包

Qt release 程序打包（注意，使用 `windeployqt` 对 qml 工程打包，应该再加上 `--qmldir <qml源码地址>`）

​	https://blog.csdn.net/zlpng/article/details/130773437

​	https://blog.csdn.net/weixin_68016945/article/details/130493586

​	程序 放到另一个电脑上出问题： https://blog.csdn.net/childbor/article/details/125283893

​	程序文件夹瘦身：

​		https://www.ycpai.cn/python/Mwbdzv3Q.html

​		https://blog.csdn.net/weixin_42126427/article/details/113250855
