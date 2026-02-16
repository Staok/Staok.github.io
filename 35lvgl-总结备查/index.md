# LVGL 总结备查


# LVGL 总结备查



各种 UI 库的总结和对比：

[Cpp-Learning/C-C++实用库备查.md at main · Staok/Cpp-Learning](https://github.com/Staok/Cpp-Learning/blob/main/C-C%2B%2B实用库备查.md#ui)。



文章所在 Github 仓库 [Staok/LVGL-Study-Record: LVGL 总结备查文章](https://github.com/Staok/LVGL-Study-Record) 会保持最新，其它地方的不会跟进。



## Start / 各家资源

**官方**



主要特性 [Introduction - LVGL documentation](https://docs.lvgl.io/master/introduction/index.html#key-features)。

- Powerful building blocks such as [buttons, charts, lists, sliders, images](https://docs.lvgl.io/master/widgets/index.html#widgets), etc.
- Advanced graphics with animations, anti-aliasing, opacity, smooth scrolling
- Various input devices such as touchpad, mouse, keyboard, encoder, etc.
- Multi-language support with UTF-8 encoding
- Multi-display support, even with mixed color formats
- Fully customizable graphic elements with CSS-like styles
- Hardware independent: use with any microcontroller or display
- Scalable: able to operate with little memory (64 kB Flash, 16 kB RAM)
- [OS](https://docs.lvgl.io/master/integration/overview.html#threading), external memory and [GPU](https://docs.lvgl.io/master/main-modules/draw/index.html#draw) are supported but not required
- Single frame buffer operation even with advanced graphic effects
- Written in C for maximal compatibility (C++ compatible)
- [Simulator](https://docs.lvgl.io/master/integration/pc/index.html#simulator) to start embedded GUI design on a PC without embedded hardware
- User code developed under simulator can be shared with firmware to make UI development more efficient.
- Binding to [MicroPython](https://docs.lvgl.io/master/integration/bindings/micropython.html#micropython)
- Tutorials, examples, themes for rapid GUI design
- Documentation is available online
- Free and open-source under MIT license
- Free for commercial projects



支持的显示 [FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html#is-my-display-supported)。

LVGL needs just one simple driver function to copy an array of pixels into a given area of the display. If you can do this with your display then you can use it with LVGL.

Some examples of the supported display types:

- TFTs with 16 or 24 bit color depth
- Monitors with an HDMI port
- Small monochrome displays
- Gray-scale displays
- even LED matrices
- or any other display where you can control the color/state of the pixels

See the [Display (lv_display)](https://docs.lvgl.io/master/main-modules/display/index.html#display) section to learn more.



硬件要求

Basically, every modern controller which is able to drive a display is suitable to run LVGL. The minimal requirements are:

- 16, 32 or 64 bit microcontroller or processor
- \> 16 MHz clock speed is recommended
- Flash/ROM: > 64 kB for the very essential components (> 180 kB is recommended)
- RAM:
  - Static RAM usage: ~2 kB depending on the used features and object types
  - Stack: > 2kB (> 8 kB is recommended)
  - Dynamic data (heap): > 4 KB (> 48 kB is recommended if using several objects).   Set by *LV_MEM_SIZE* in *lv_conf.h*.
  - Display buffer:  > *"Horizontal resolution"* pixels (> 10 × *"Horizontal resolution"* is recommended)
  - One frame buffer in the MCU or in an external display controller
- C99 or newer compiler
- Basic C (or C++) knowledge: [pointers](https://www.tutorialspoint.com/cprogramming/c_pointers.htm), [structs](https://www.tutorialspoint.com/cprogramming/c_structures.htm), [callbacks](https://www.geeksforgeeks.org/callbacks-in-c/).



Is my MCU/hardware supported? [FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html#is-my-mcu-hardware-supported)。

Every MCU which is capable of driving a display via parallel port, SPI, RGB interface or anything else and fulfills the [Requirements](https://docs.lvgl.io/master/introduction/requirements.html#requirements) is supported by LVGL.

This includes:

- "Common" MCUs like STM32F, STM32H, NXP Kinetis, LPC, iMX, dsPIC33, PIC32, SWM341 etc.
- Bluetooth, GSM, Wi-Fi modules like Nordic NRF, Espressif ESP32 and Raspberry Pi Pico W
- Linux with frame buffer device such as /dev/fb0. This includes Single-board computers like the Raspberry Pi
- Anything else with a strong enough MCU and a peripheral to drive a display



开源协议

The LVGL project (including all repositories) is licensed under **MIT  license**. This means you can use it even in commercial projects.

It's not mandatory, but we highly appreciate it if you write a few words  about your project in the My projects category of the forum or a private message to [lvgl.io](https://lvgl.io/#contact).

Although you can get LVGL for free there is a massive amount of work behind it.  It's created by a group of volunteers who made it available for you  in their free time.

To make the LVGL project sustainable, please  consider contributing to the project. You can choose from many different ways of contributing such as simply writing a tweet about you using  LVGL, fixing bugs, translating the documentation, or even becoming a  maintainer.



- 开始：[Getting started - LVGL documentation](https://docs.lvgl.io/master/getting_started/index.html)。

- 官方例子：https://lvgl.io/demos

- **主要文档**：[LVGL documentation](https://docs.lvgl.io/master/index.html)。

  - 介绍 Introduction

  - 开始使用 Get started（概览、平台、操作系统等）

  - 入门例子 Examples（用 C 写的）

  - **移植 Integration or Porting**

  - Modules 和 Widgets

    - Objects；
    - Positions, sizes, and layouts；Styles
    - Scroll；Layers；Events
    - Input devices；Displays
    - Colors；Fonts；Images
    - File system
    - Animations；Timers；Drawing；Profiler
    - Renderers and GPUS；New widget

  - 以及**各个控件 Widgets、布局 Layouts** 等等的介绍。要都熟悉。

    总结在下面 `基础控件`、`样式系统` 等章节。



- Github仓库：https://github.com/lvgl

- 入门小例子 Examples 源码：https://github.com/lvgl/lvgl/tree/master/examples

  基本是一些创建 label、btn，给 btn 加回调函数，更改 btn、label 等的样式（很长的设置代码，很繁琐）。

  这些大部分前端都在 比如 SquareLine Studio 等的可视化组件拖拽 UI 编辑器 里面做就可以了~然后导出 lvgl 的 UI 源码然后进一步编写业务逻辑。

- 官方 Demo 源码：https://github.com/lvgl/lvgl/tree/master/demos



- 移植相关，具体要看源码 [Integration - LVGL documentation](https://docs.lvgl.io/master/integration/index.html)。
- 官方 lvgl drivers 底层驱动源码：[lvgl/src/drivers at master · lvgl/lvgl](https://github.com/lvgl/lvgl/tree/master/src/drivers)。
- Building LVGL with CMake：[CMake - LVGL documentation](https://docs.lvgl.io/master/integration/building/cmake.html)。



官方论坛 https://forum.lvgl.io/，有问题就去找和问。



*p.s 这里不涉及 MicroPython 版本的 LVGL（还是 C 源码 的 功能是最全的，最通用，性能有保障的）。*

*p.s 注意，有很多 LVGL 视频教程，但是大都搞得时长那么长，个人觉得不如直接看官方文档和源码，这个库设计比较优雅，LVGL 的 设备输入输出、控件 和 style 和各个模块 都过一遍不难的。*



一个自己开源的 LVGL 模板工程 [Staok/lvgl_port_win-linux_vscode](https://github.com/Staok/lvgl_port_win-linux_vscode)。



**百问网**



B站教程：

- 【lvgl项目开发】IMX6ULL Linux LVGL GUI演示，开源并且有lvgl教程 lvgl开发 lvgl项目 littleVGL https://www.bilibili.com/video/BV1cU4y1b7dY。

- 基于100ASK_IMX6ULL开发板的LVGL(v8.2)学习+开发教程，面向零基础+简易上手+项目导向 https://www.bilibili.com/video/BV1Xa41197uh。




手册，有的版本有翻译 https://lvgl.100ask.net/master/。



官方论坛 https://forums.100ask.net/c/13-category/13。



开发实用工具 https://lvgl.100ask.net/8.2/tools/index.html，在里面可以选择其它 LVGL 版本。

！注意！一些功能，可能后来 LVGL 官方支持了，所以要及时跟进 LVGL 官方；或者其他地方有更好的实现，所以多调研调查。

包括：

- 显示中文
- 等宽字体
- 自定义SYMBOL(图标)字体
- 让 lvgl 支持中文输入
- lv_lib_100ask https://github.com/100askTeam/lv_lib_100ask 不少实用功能
  - Iv_100ask_2048
  - Iv_100ask_calc
  - lv_100ask_file_explorer
  - Iv_100ask_memory_game
  - Iv_100ask_nes
  - Iv_100ask_page_manager
  - Iv_100ask_pinyin_ime
  - Iv_100ask_screenshot 保存为 bmp、png、jpg 格式。
  - Iv_100ask_sketchpad
- 文件浏览（基础组件）https://forums.100ask.net/t/topic/926，LVGL V9 官方已经支持了。
- 组件库（作为三方库）https://forums.100ask.net/t/topic/193。




**正点原子**

【正点原子】手把手教你学LVGL图形界面编程 https://www.bilibili.com/video/BV1CG4y157Px。

在正点原子资料下载站，大部分开发板配套资料里面带有 LVGL 教程手册 http://www.openedv.com/docs/index.html，如：`LVGL开发指南_V1.x.pdf`，还有配套视频的源码和ppt可下载。

也有 [2023年新版手把手教你学LVGL — 正点原子资料下载中心 1.0.0 文档](http://www.openedv.com/docs/book-videos/zdyzshipin/4free/newlvgl.html)。



## 移植相关 & 建立工程

### 移植相关参考手册和例子

这里是一些官方移植教程和网上例子罗列。

看官网也有了 工程创建器了 [LVGL — Download Project Creator](https://lvgl.io/tools/project-creator)。

不过还行希望处于深入学习原理的目的，手动创建工程：VsCode + CMake (+ clangd .etc)。



移植 Porting 官方参考文档 [Overview - LVGL documentation](https://docs.lvgl.io/master/integration/overview.html)。

具体例子见源码 exmaples 文件夹 里面这些文件：

```bash
lv_port_disp_template.c
lv_port_disp_template.h
lv_port_fs_template.c
lv_port_fs_template.h
lv_port_indev_template.c
lv_port_indev_template.h
```



win 端 和 linux 端移植参考：

- https://gitee.com/staok/lvgl_port_win_vscode



linux 端移植参考：

- 官方 lv_port_linux_frame_buffer：

  - https://github.com/lvgl/lv_port_linux_frame_buffer 这个 FB 机制显示， lv tick inc 用 custom_tick_get() 得到系统时间。
  - https://blog.lvgl.io/2018-01-03/linux_fb。

- 快速支持参考文章

  https://blog.csdn.net/weixin_45861321/article/details/115772632。

  https://blog.csdn.net/Donald_Shallwing/article/details/130671241 这个是使用 DRM 机制 代替 FB。

- IMX6ULL Linux LVGL GUI V2.0

  源码 https://gitee.com/weidongshan/lv_100ask_linux_desktop。

  视频 https://www.bilibili.com/video/BV1nT4y1R7rz。



有条理建立 LVGL 工程。

参考本人做的 win 和 linux 均兼容的移植好的工程 https://gitee.com/staok/lvgl_port_win-linux_vscode，实现了通过 cmakelist 控制，可在 win（ VsCode（with sdl lib 或 win_drv）） 和 嵌入式 linux 均能跑的工程，方便调试和运行。



### 多线程应用注意

LVGL 的 API 不是线程安全的，多线程应用中，官方建议：

**调用 LVGL的 API `lv_xx()`，保证两点：1、按照程序里面的执行顺序执行，2、互斥 或者 都在一个线程里面执行（使用单线程的线程池的提交 或者 单线程执行的函数的队列）**，即可基本保证 LVGL 的稳定运行。



## 可视化 UI 设计工具

UI 可视化操作 有 SquareLine Studio (以及网页版的 SquareLine Vision) 和 EEZ Studio 等可视化设计器，可以拖拽生成C代码。前者有组件 component 功能，后者有事件流功能。前者比较重，且收费，后者较轻量且免费开源。组件是更需要的，需要看看后者是否支持了，如果支持了就选用后者。

- eez studio（开源免费）推荐。
- squareLine（收费）。
- [anyui](https://anyui.tech/)。
- [LVGL Visual Architect Specification](https://lvgl.btvi.com.br/)。web 在线 LVGL UI 制作，功能较简单。
- 等等。



- LVGL 官方 的 XML 编辑 UI [LVGL Pro](https://pro.lvgl.io/)（收费）。



- 将 C UI 代码转换为 HTML 文件：https://github.com/lvgl/lv_web_emscripten。LVGL ported to Emscripten to be converted to JavaScript。
- 这是一个用 Qt 写的 可视化布局 LVGL 前端界面的 工具 https://github.com/CURTLab/LVGLBuilder。玩具，看看就好。



因为自己之前工作原因 用了很久 SquareLine Studio，因此下面有很多对这个软件的记录。




### SquareLine Studio

> SquareLine Studio 是一款易于使用的 LVGL 拖放式 UI 编辑器工具，甚至设计人员也可以在其中创建功能齐全的 UI。
>
> 立即实现功能性 UI 立即设计和创建工作 UI，而不是重新实现原型。
>
> 与供应商无关的导出平台独立代码，可以为任何供应商的 MCU、MPU 或显示器构建。

SquareLine Studio [SquareLine Studio - Design and build UIs with ease](https://squareline.io/)。收费。

官方参考手册 [SquareLine Studio Documentation | SquareLine Studio](https://docs.squareline.io/docs/squareline)。

官方论坛 https://forum.squareline.io/，有问题就去找和问，有意见就提，下一版可能会更新上。



注意，下面的 `基础控件`、`样式系统` 等章节，是 C 编程 方式 繁琐的搞出前端界面。

**推荐尽量全用 SquareLine Studio 来搞前端的视觉样式（添加控件、布局、样式、动画全搞定）**。

使用 SquareLine Studio 生成的文件，除了  event 回调函数里面 和 component 自定义组件 hook 等，不要手动修改，保持生成的原样，使用 SquareLine Studio 生成更新覆盖。

**SquareLine Studio 日常使用遇到的问题和注意点见 `优化相关` 章节。**



#### 基本信息

- 教程：LVGL设计器SquareLine Studio零基础入门1：style、font、event使用介绍 https://www.bilibili.com/video/BV1Bu411p7cM。



- Simulator on PC [Windows - LVGL documentation](https://docs.lvgl.io/master/integration/pc/windows.html#)。
- win & linux 端，使用 VsCode，自己移植的模板，Github 仓库在 https://github.com/Staok/lvgl_port_win-linux_vscode。



- win 上 使用 CodeBlocks: https://github.com/lvgl/lv_port_win_codeblocks。

  CodeBlocks 编译器很难用，推荐使用  VsCode（with sdl2 lib），就是上面的。

  下载 CodeBlocks 带 mingw 的 安装版本，不要下便携版的：https://www.codeblocks.org/downloads/。

  教程 https://blog.csdn.net/hmc_123/article/details/128016552。

  CodeBlocks 报错解决：修改 编辑器 为 CodeBlocks 自带的，再点 Rebuild。

  - https://blog.csdn.net/weixin_46023406/article/details/132041014。
  - https://blog.csdn.net/slimmm/article/details/130064209。
  - https://ask.csdn.net/questions/7625851。



#### 关键教程

- 所有自带控件介绍 https://docs.squareline.io/docs/widgets/
- 所有可调节的 style https://docs.squareline.io/docs/styles
- 添加自己的字体（就是需要填入需要的文字，或者索引范围（这个比较方便）） https://docs.squareline.io/docs/dev_env/fontmanager
- screen，每个页面都建一个 screen 比较好，然后 switch screen 即可 https://docs.squareline.io/docs/dev_env/screens
- 提供的所有 event https://docs.squareline.io/docs/events
- 提供的所有 Layout、Flags、States 等 https://docs.squareline.io/docs/dev_env/inspector
- 自定义 Components，可重复利用 https://docs.squareline.io/docs/components
- 自定义 board 模板，直接导出自己用的完整工程 https://docs.squareline.io/docs/obp



### EEZ Studio

同样可图形化的 LVGL 编辑器，并可图形化编辑事件。开源免费。

[eez-open/studio: Cross-platform low-code GUI and automation](https://github.com/eez-open/studio)。



[gxdung/eez_studio_cn: EEZ Studio 中文版](https://github.com/gxdung/eez_studio_cn)。



使用之前，需要全面评估下是否支持足够全面的功能。



### LVGL Pro

LVGL 本家做的 UI 编辑器，XML 描述 UI。有免费版和收费版。

[LVGL Pro](https://pro.lvgl.io/)。



## 控件 / 样式 / 布局

可见一个不错的教程 https://www.iotword.com/13599.html。



注意本文主要成型于 LVGL V8 时期，有些 API 和最新版有出入，参考 源码 [lvgl/src at master · lvgl/lvgl](https://github.com/lvgl/lvgl/tree/master/src) 中的 `lv_api_map_vX.X.h` 文件里面的定义查看新旧版本的 API。



### 前置信息

- **参考 API，重要**：

  - 每个控件的 API 可见 lvgl 源码 `\src\widgets\` 目录下的对应控件的 `.h` 文件，源码注释很丰富。
  - 尤其需要熟悉配置文件 `lv_conf.h`。
  - 重要官方参考文档
    -  [All Widgets - LVGL documentation](https://docs.lvgl.io/master/widgets/index.html)。
    - [Main Modules - LVGL documentation](https://docs.lvgl.io/master/main-modules/index.html)
    - [Common Widget Features - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/index.html)。
    - [3rd-Party Libraries - LVGL documentation](https://docs.lvgl.io/master/libs/index.html)。

- **Events**：[Events - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/events.html)。

  > Events are used to inform the user that something has happened with an object. You can assign one or more callbacks to an object which will be called if the object is clicked, released, dragged, being deleted, etc.
  >
  > ```c
  > lv_obj_add_event(btn, btn_event_cb, LV_EVENT_CLICKED, user_data); /*Assign a callback to the button*/
  > 
  > ...
  > 
  > void btn_event_cb(lv_event_t * e)
  > {
  >        // The current event code can be retrieved with:
  >     lv_event_code_t code = lv_event_get_code(e);
  > 
  >     // The object that triggered the event can be retrieved with:
  >     lv_obj_t * obj = lv_event_get_target(e);
  > 
  >     printf("Clicked\n");
  > }
  > ```

- **States**：[Parts and States - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/parts_and_states.html)。

  > LVGL objects can be in a combination of the following states:
  >
  > - `LV_STATE_DEFAULT`: Normal, released state 默认状态
  > - `LV_STATE_CHECKED`: Toggled or checked state 切换或选中状态
  > - `LV_STATE_FOCUSED`: Focused via keypad or encoder or clicked via touchpad/mouse 通过键盘、编码器聚焦或通过触摸板、鼠标单击
  > - `LV_STATE_FOCUS_KEY`: Focused via keypad or encoder but not via touchpad/mouse 通过键盘、编码器聚焦
  > - `LV_STATE_EDITED`: Edit by an encoder 由编码器编辑
  > - `LV_STATE_HOVERED`: Hovered by mouse (not supported now) 鼠标悬停（现在不支持）
  > - `LV_STATE_PRESSED`: Being pressed 已按下
  > - `LV_STATE_SCROLLED`: Being scrolled 正在滚动的状态
  > - `LV_STATE_DISABLED`: Disabled 禁用状态
  >
  > For example, if you press an object it will automatically go to the `LV_STATE_FOCUSED` and `LV_STATE_PRESSED` states and when you release it the `LV_STATE_PRESSED` state will be removed while focus remains active.
  >
  > To check if an object is in a given state use `lv_obj_has_state(obj, LV_STATE_...)`. It will return `true` if the object is currently in that state.

  **Parts**：通过 `_style_` 相关 API 给 控件 的 PART 相关部分 给予设定的样式。

  > Widgets might be built from one or more parts. For example, a button has only one part called `LV_PART_MAIN`. However, a Slider (lv_slider) has `LV_PART_MAIN`, `LV_PART_INDICATOR` and `LV_PART_KNOB`.

- **Styles**：[Styles - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/styles/index.html)。

  样式系统，巨多样式属性（半径、不透明度、渐变、边框、轮廓、阴影等）可在任何状态下自定义各种控件的各个细节部分。

  Size、Position、Background、Outline、Border、Shadow、Others
  
  > A style instance contains properties such as background color, border width, font, etc. that describe the appearance of objects.
  >
  > properties can be added to configure the style. For example:
  >
  > ```c
  > static lv_style_t style1;
  > lv_style_init(&style1);
  > lv_style_set_bg_color(&style1, lv_color_hex(0xa03080))
  > lv_style_set_border_width(&style1, 2))
  > ```
  >
  > **给控件 不同 part 设置在 不同 state 下的 Styles**。**Styles** are assigned using the OR combination of an object's **part** and **state**.For example to use this style on the slider's indicator when the slider is pressed:
  >
  > ```c
  > lv_obj_add_style(slider1, &style1, LV_PART_INDICATOR | LV_STATE_PRESSED);
  > ```
  >
  > **父对象设置 样式，其所有子对象均顺延继承**。Some properties (typically the text-related ones) can be inherited. This means if a property is not set in an object it will be searched for in its parents too. For example, you can set the font once in the screen's style and all text on that screen will inherit it by default.
  >
  > **本地样式属性**。Local style properties also can be added to objects. This creates a style which resides inside the object and is used only by the object: 推荐使用这种方式
  >
  > ```c
  > lv_obj_set_style_bg_color(slider1, lv_color_hex(0x2080bb), LV_PART_INDICATOR | LV_STATE_PRESSED);
  > ```



- **Layouts**： [Layouts - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/layouts/index.html)。

布局引擎，类似 CSS 的 Flexbox 和 Grid 布局引擎能够以响应方式自动调整小部件的大小和位置。

Flexbox 类似 Qt 的 anchors，Grid 是 二维网格布局。



- **Flags**：[Flags - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/flags.html)。

控制控件的一些杂类特性。



### 基础控件

*p.s 随着 LVGL 版本更新，会增加基础控件，请跟进官方文档和源码。*

重要官方参考文档

-  [All Widgets - LVGL documentation](https://docs.lvgl.io/master/widgets/index.html)。
- [Main Modules - LVGL documentation](https://docs.lvgl.io/master/main-modules/index.html)
- [Common Widget Features - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/index.html)。
- [3rd-Party Libraries - LVGL documentation](https://docs.lvgl.io/master/libs/index.html)。



**提示类**

- 标签（lv_label）
- 进度条（lv_bar）
- 加载器 / 加载 / 转圈 提示动画（lv_spinner）
- LED / 圆形-亮灭、亮度 指示（lv_led）



**交互大类**

- 按钮（lv_btn）
  - 矩阵按键（lv_btnmatrix），一次创建矩阵排列的多个按键
  - 图片按钮（lv_imgbtn），可在按钮里面添加图片
- 开关（lv_switch）
- 复选框（lv_checkbox）
- 列表 / 列表方式显示控件（lv_list）
- 下拉框（lv_dropdown）
- 菜单（lv_menu）
- 滚轮 / 滚动设置（lv_roller），上下滑动切换显示 / 设置
- 微调器（lv_spinbox），数字文本框带 上下 或 左右 箭头按键可进行调节
- 滑块 / 滑动设置（lv_slider）
- 圆弧滑块 / 圆弧进度显示（lv_arc）
- 色环 / 颜色选择器（lv_colorwheel）
- 日历 / 日期选择（lv_calendar）



**文本输入框**

- 文本区域（lv_textarea）

  基本 API 有：给输入框内添加文本、调出键盘部件（关联之）、设置光标位置、删除文本、设置单行模式 / 密码显示模式（密码显示时间）、限制可接受字符 / 字符串长度、设置输入框内默认显示（placeholder）、获取输入框当前的文本。

- 富文本显示（lv_span）

  A spangroup is the object that is used to display rich text. Different from the label object, `spangroup` can render text styled with different fonts, colors, and sizes into the spangroup object.



**图形 / 图像 / 序列图动画**

- 图形：

  - 画板（lv_canvas）

    A Canvas inherits from Image where the user can draw anything. Rectangles, texts, images, lines, arcs can be drawn here using lvgl's drawing engine. Additionally "effects" can be applied, such as rotation, zoom and blur.

  - 线条（lv_line）

- 图像：

  - 图片显示（lv_img）

- 多个图片按序列显示 / 切换 （lv_animimg）



**窗口 / 多页面 / 菜单 / 消息框**

- 窗口（lv_win），创建一个新页面。
- 选项卡（lv_tabview）
- 平铺视图（lv_tileview），多个页面平铺拼接，上下左右滑屏即切换显示页面。
- 菜单（lv_menu），列表形式显示菜单，点击后有子菜单。
- 消息框（lv_msgbox）



**表盘 / 表格 / 图表**

- 仪表 / 表盘（lv_meter）
- 表格（lv_table），设置行列数，单元格添加内容
- 图表（lv_chart），显示 柱状图、折线图、点图，可动态滚动、更新、放大缩小。



### 虚拟键盘

lv_keyboard，官方手册 [Keyboard (lv_keyboard) - LVGL documentation](https://docs.lvgl.io/master/widgets/keyboard.html)。

虚拟键盘的使用建议：在 squareLine 里面用到键盘的页面 添加上，并设置 hide，当 textarea 输入文本框 focused 的时候 显示键盘并设置键盘的输入目标为这个输入文本框，输入文本框 defocused 的时候 直接隐藏键盘即可。



**基本**

参考 https://www.iotword.com/13599.html

> 1：创建键盘部件
>
> ```c
> lv_obj_t  *kb = lv_keyboard_create(parent);
> ```
>
> 2：关联文本框
>
> ```c
> lv_obj_t *ta = lv_textarea_create(lv_scr_act());		/* 创建文本区域部件 */
> lv_keyboard_set_textarea(kb, ta);						/* 关联键盘和文本区域部件 */
> ```
>
> 3：设置按键弹窗
>
> ```c
> lv_keyboard_set_popovers(kb, true);						/* 允许按键弹窗提示 */
> ```
>
> 4：设置键盘模式
>
> ```c
> lv_keyboard_set_mode(kb, LV_KEYBOARD_MODE_NUMBER);		/* 数字键盘模式 */
> ```



键盘分为全键盘和数字键盘，可以自定义键盘中的按键字符、排列，键盘外观，键盘的多个页面等。



**中文输入**

参考 上面 `Start / 各家资源` 一节中 `百问网` 一段的内容。

- 【LVGL中文输入(拼音输入法)】lv_100ask_pinyin_ime：支持中文输入(拼音输入法)的LVGL键盘部件增强插件

  https://www.bilibili.com/video/BV1DY41147xX

  文档地址(有中文)：https://docs.lvgl.io/master/others/ime_pinyin.html
  
  源码地址：https://github.com/lvgl/lvgl/tree/master/src/extra/others/ime

  使用示例：https://docs.lvgl.io/master/others/ime_pinyin.html#example
  
  这个，需要自己添加中文拼音对应的文字字库。



### 三方库支持 / 更多功能

具体见 [3rd-Party Libraries - LVGL documentation](https://docs.lvgl.io/master/libs/index.html)。

- 文件系统接口。
- 图片 BMP / JPG / PNG / GIF 等支持。
- 二维码、条形码显示 QR code，Barcode。
- 字体支持 FreeType。Tiny TTF font engine。
- FFmpeg support，lvgl 调用 ffmpeg 的 API 显示任意格式图片和播放视频。
- 等。



在下面对这些的使用做记录。




### 多字体 & 字库支持

文字特征：UTF-8 支持；抗锯齿；（lv_label）自动换行和自动文本滚动；双向文本支持（混合 RTL 和 LTR）；阿拉伯语和波斯语支持；自定义字体引擎的接口；FreeType 集成；等。



#### 使用 LVGL 自带字体

仅支持 ASIC 字符。

官方手册 [Fonts (lv_font) - LVGL documentation](https://docs.lvgl.io/master/main-modules/fonts/index.html)。



#### 自带 Tiny TTF 字体解码库

官方文档 [Tiny TTF Font Engine - LVGL documentation](https://docs.lvgl.io/master/libs/font_support/tiny_ttf.html)。

lvgl 自带 Tiny TTF 库，可以通过 字体文件 或者 内存数组（占 RAM） 创建字体 lv_font_t，可以设置其 size，然后 通过 lv_style_set_text_font() 给一个 style，再把这个 style 给一个 label。 

```c
static lv_font_t* temp_font = lv_tiny_ttf_create_file_ex(
    "X:xxx/Sans.ttf",     42,
    20 * 1024 * 1024 );

if(!temp_font) {
    BGUIFE_LOGE("err lv_tiny_ttf_create_file()");
    return -ENOENT;
}

lv_obj_set_style_text_font(
    ui_xxxStr,
    temp_font,
    LV_PART_MAIN | LV_STATE_DEFAULT );

// lv_tiny_ttf_set_size(temp_font, 27);
```

使用字体文件，每次刷新 ui 是 现读 字体文件，很慢，不推荐；而导出字体文件为数组，那么 更换字体、加字符 等 又是增加麻烦的步骤，占用 Flash 和 RAM。

所以不推荐这个方法。



#### freeType 字体解码库支持（推）

使用字体文件相比于转换字体为数组的方式，不明显增加 编译后 bin 大小，且可以灵活增加多种字体大小，且一招解决各种特殊字符乱码问题。

官方文档 [FreeType Font Engine - LVGL documentation](https://docs.lvgl.io/master/libs/font_support/freetype.html)。

需要预安装 freetype 库：

- 从官网下载库包 https://freetype.org/download.html，并 解压

- win 上可直接用 cmake-gui 来生成 build，选择好 build 目录 和 `CMAKE_INSTALL_PREFIX` 目录，点 config 和 gen 即可；然后在 build 目录下 执行 `make` 和 `make install`。把 install 目录下的 include 和 lib 文件夹直接复制到编译器目录下比如 `mingw64/x86_64-w64-mingw32`。然后 自己 cmake 工程里面，直接：

  ```cmake
  find_package(Freetype REQUIRED)
  target_include_directories(lvgl PRIVATE ${FREETYPE_INCLUDE_DIRS})
  target_link_libraries(lvgl PRIVATE ${FREETYPE_LIBRARIES})
  ```
  
- linux 下用 buildroot 工具链来引入该库。



使用 LVGL 的 freeType 相关 API 可以直接从 指定的 ttf 字体文件 和 大小创建 LVGL 的 字体数据结构 `lv_font_t*`，然后就可以直接用 `lv_obj_set_style_text_font()` 来给 label 设置字体。

对于 SquareLine 等导出的 ui 代码，需要 给 每个 label 设置字体，目前没有全局设置字体，可以用如下方法：

```c
// to change the squareLine ui label fonts, add these lines into ui.h or lvgl.h, to disable all arr fonts, and use
// "getBasicFontSize_xx()" instead!! the effect is:
//  change from "lv_obj_set_style_text_font(ui_Labelxxx, &ui_font_fontReg24, LV_PART_MAIN | LV_STATE_DEFAULT);"
//  into lv_obj_set_style_text_font(ui_Label330, getBasicFontSize_24(), LV_PART_MAIN | LV_STATE_DEFAULT);

#define UI_FONT_FONTREG16 0
#define UI_FONT_FONTREG24 0
#define UI_FONT_FONTREG30 0
#define UI_FONT_FONTREG36 0
const lv_font_t* getBasicFontSize_16();
const lv_font_t* getBasicFontSize_24();
const lv_font_t* getBasicFontSize_30();
const lv_font_t* getBasicFontSize_36();
#define ui_font_fontReg16 (*getBasicFontSize_16())
#define ui_font_fontReg24 (*getBasicFontSize_24())
#define ui_font_fontReg30 (*getBasicFontSize_30())
#define ui_font_fontReg36 (*getBasicFontSize_36())
```



#### 生成静态字体数组 & squareLine 中字体管理

在 squareLine 中通过 font manager 选择一个字体文件、设置大小、设置范围（可以网搜某种语言的 unicode 编码范围，然后全部添加） 或者 字符集，然后创建字体，然后给每个 label 手动设置这个字体。

squareLine 默认使用 lvgl 自带 的字体（仅支持 ASIC 字符），并集成了 `从字体库创建` 这一功能，直接在这个软件里面 `fontManager` 操作即好。

https://docs.squareline.io/docs/dev_env/fontmanager



或者，使用 字体转换器（https://lvgl.io/tools/fontconverter） 得到 所用字体数组的 .c 文件 字体文件 并在 lvgl 使用，参考 https://www.bilibili.com/video/BV1CG4y157Px?p=67

squareLine 中其实是自带这个转换器，这个转换器也有 offline 版本的（https://github.com/lvgl/lv_font_conv），需要 node.js 来运行。



优点：

- squareLine 中操作方便，与 squareLine 做 ui 契合

缺点：

- 字体每种大小需要生成新的字体（可以让交互设计人员统一 UI 界面所有文本为 三种或四种 大小的字体，不过就限制交互设计了），生成的还很慢，每次修改起来麻烦。
- 取字体文件中的字符范围一般是一部分，所以容易出现未知字符。
- 生成的字体数组大小：这是生成包括最多字符、多国语言的字符集，还可以缩减字符集。提供了压缩功能，试了试，只对 2bpp 以及以上的有用（2、3、4bpp 对应不压缩是 36MB~80MB，启用压缩分别减小 10MB~40MB），对于 1bpp 没有用（30 pix：15MB，36 Pix：20MB）。
- 占 FLASH。所以不推荐这个用法。



#### LVGL 富文本实现 / 颜色 / 显示特殊符号 等

- 首先所有字体用 "freeType 字体解码库支持" 一段所提供的方法，即使用 ttf 字体。

- 想要 加粗、斜体，或者二者结合，lvgl freeType API 创建字体的时候传入设置。

- 缺少的字符往 ttf 字体 里面加即可。包括特殊符号、emoji 都可以。

  使用此方式设置显示特定字符 `lv_label_set_text(ui_LabelXXX, "\u2605");`。

  unicode 自定义编码范围 https://blog.csdn.net/booynal/article/details/127175804，`U+E000 ~ U+F8FF`。

- 设置一段文本中特定范围上颜色 `lv_label_set_text(obj, "#RRGGBB your_label#");`。

- 下划线、删除线，使用 lvgl 对 label 的 API。

- 文本中显示变量，可以约定 用 `%1`、`%2` 或者 等占位，在显示前替换为变量即可。



这个方法只可针对分离的各个 label 单独设置，ui 上没法连续连成一段，若不需要这种，则可用上面的方法，可以多封装封装，更方便使用。

lv_span 的好处是，可以在一段连续的文本中，设置 一段一段文本各不相同的 style（如颜色、字体（大小）、下划线 等）。



### 多语言支持 i18n



```c
// LanguageType and strings
//     缩写         UI               注
//     "en",       English          英语(English)
//     "fr",       Français         法语(French)
//     "de",       Deutsch          德语(German)
//     "es",       Español          西班牙语(Spanish)
//     "sv",       Svenska          瑞典语(Swedish)
//     "nl",       Nederlands       荷兰语(Dutch)
//     "ja",       日本語            日语(Japanese)
//     "zh-cn",    中文              中文(Chinese (China, Simplified)) same as "zh-CN-Hans" used for localazy and lv_i18n
//     "zh-tw",    中文繁體           中文繁体(Chinese (Taiwan, Traditional)), same as "zh-TW-Hant"
//     "pt_BR"     Português        巴西葡萄牙语(Brazilian Portuguese)
//     "hu"        Magyar nyelv     匈牙利语(Hungarian)
//     "it"        Italiano         意大利语(Italian)
//     "ko"        한국인            韩语(Korean)
//     "pl"        Język polski     波兰语(Polish)
```



#### 生成多语言文件 lv_i18n 方案（old）

（过往方案，废弃）



多语言支持官方手册 squareline

https://docs.squareline.io/docs/multilanguage

github 仓库，其 readme.md 详细说明了使用方法

https://github.com/lvgl/lv_i18n



网上教程文章

https://blog.csdn.net/weixin_43615005/article/details/128954698

https://blog.csdn.net/minorikawa_fuso/article/details/128314627

原理解析

https://zhuanlan.zhihu.com/p/672878099



nodejs 中文网 http://www.nodejs.com.cn/

npm 教程

- https://www.npmjs.cn/
- https://www.runoob.com/nodejs/nodejs-npm.html
- 简明 https://blog.csdn.net/jieyucx/article/details/131547948

1. 安装 node.js，https://nodejs.org/en/download/

   - 最好下载 bin 便携版 Windows Binary (.zip)（在 C 盘权限受限制的环境用安装版安装不动）。

     放到可联网的环境中，后面通过 npm 在线安装一些依赖包。

     **将 bin 所在目录加入环境变量**（推荐），或者不加之后用绝对路径调用 bin 可执行文件也行。

   - 安装  lv_il8n 包，依赖的包很多，一个个手动解决不现实，最好在线安装 lv_il8n 包：

     （在圈外 / 联网的环境 打开 一个 命令行，下面都是）**执行 `npm i lv_i18n -g`**。

     加入 `-g` 是全局安装，包被安装在 nodejs 安装目录的 node_modules 文件夹里，**将这个文件夹添加系统环境变量**，后面 包 直接可以找到，否则就是将包安装到当前目录 node_modules 文件夹里，污染源码，而且还得通过把这个文件夹加入环境变量或者在命令行通过路径找到 lv_i18n 包的路径来执行 lv_i18n 命令。。

     通过在线安装的版本这个是老的了，可再到 https://github.com/lvgl/lv_i18n 直接下载后替换 `nodejs\node_modules` 目录里面的 lv_i18n 文件夹，然后在 lv_i18n 目录里面打开 命令行 执行 `npm updae`，这样就是安装和解决所有依赖，这样就是最新的了，最新的有一些 bugfix。
     
     
     
     通过 npm 手动安装包：是 下载 包文件后（文件夹内有 package.json 包信息文件），命令行进入包目录直接执行 `npm install -g`，或者包外面目录执行 `npm i <包路径> -g`。
     
     npm 一些基本命令：
     
     ```bash
     npm i express -g  # 会安装 express 到配置的全局目录下
     npm uninstall express -g  # 卸载全局模块 express
     npm update express  # 更新最新版本的 express
     npm list 或者 npm ls  # 查看本地已安装模块的清单列表
     ```
     
     

2. 运行时遇到问题（按照上面步骤一般不会遇到运行问题，缺少的依赖库 npm 会自动解决）：

   - 运行时如遇到问题缺少 es6-error 模块 或者其它模块，同上面一样的 执行在线安装命令。

     离线手动安装 https://github.com/bjyoungblood/es6-error，同上面 手动安装包，但是依赖包很多，这样一个一个下麻烦且不一定下对。

   - 遇到 在此系统上禁止运行脚本 提示，https://blog.csdn.net/fanqiantao/article/details/109650213， powershell 输入 `set-executionpolicy remotesigned` 即可。

3. 运行 lv_i18n 提取所有 当前文件夹下程序文件里 要翻译字符串到 trans 文件夹下 各个语言的 yml 文件里：

   各语言规范编码 language and locale codes：https://www.andiamo.co.uk/resources/iso-language-codes/

   需要预先手动创建各个 `<语言编号>.yml` 文件，并添加一行 `<语言编号>: ~`，如 `en-GB: ~`。

   在工程的顶层目录运行：

   ```bash
   lv_i18n extract -s "./**/*.+(c|cpp|h|hpp)" -t "trans/*.yaml"
   ```

   测试用：

   - 创建 test.c 文件：

     ```c
     lv_obj_t* label1;
     void callback(lv_event_t* e) {
         if (state) {
             lv_i18n_set_locale("en-GB");
         }
         else {
             lv_i18n_set_locale("其他语言");
         }
         lv_label_set_text(label1, _("title1"));
         state = !state;
     }
     
     void lv_example_label_1(void)
     {
         lv_i18n_init(lv_i18n_language_pack);
         lv_i18n_set_locale("en-GB");
         label1 = lv_label_create(lv_scr_act());
         lv_obj_align(label1, LV_ALIGN_CENTER, 0, 100);
         lv_label_set_text(label1, _("title1"));
     	lv_label_set_text(label1, _("aaa"));
     	lv_label_set_text(label1, _("hello	ccc"));
     	lv_label_set_text(label1, _("iii %20"));
     	lv_label_set_text(label1, _("你好~~$^&(* yes"));
         lv_obj_t* btn = lv_obj_create(lv_scr_act());
         lv_obj_align(btn, LV_ALIGN_CENTER, 0, 0);
         lv_obj_set_size(btn,50,50);
         lv_obj_set_style_bg_color(btn, lv_color_hex(0x335566), 0);
         lv_obj_add_event_cb(btn, callback, LV_EVENT_CLICKED, NULL);
     }
     ```

   - 创建 en-GB.yml 文件：

     ```
     en-GB: ~
     ```

   - 在当下目录执行：

     ```bash
     lv_i18n extract -s ./test.c -t ./*.yml
     ```

   - 即把程序 test.c 中要翻译的字符串提取到了 en-GB.yml 文件里

4. 在各个语言的 yml 文件里面添加 翻译后的文案，这是手动添加。

   这一步，就可以把 各语言的 *.yaml 传到 localazy 或其它 类似的 多语言文案管理平台 进行翻译，之后 localazy 可以导出 `Rails i18nYAML` 格式的各语言文案文件，再进行下面 `lv_i18n compile ...` 的步骤 将文件 编译为 lv_i18n.c / .h 文件。

   注意，经测试，localazy 会把 上传上去的 `\n` 和 `\\` 再下载下来后 转换为 `\\n` 和 `\\\`，需要全局搜索替换来还原。。但是 `\"` 就是正常的。。

   

   对于上面的测试文件，执行 extract 后得到的结果是：

   ```yaml
   en-GB:
     title1: ~
     aaa: ~
     "hello\tccc": ~
     iii %20: ~
     你好~~$^&(* yes: ~
   ```

   上面的步骤，上传多语言管理平台，翻译再下载，本质就是将上面  `title1: ~` 中的 `~` 替换为 翻译后的文本。

5. 在工程的顶层目录，运行 lv_i18n 将 trans 文件夹下的 各个语言的 yml 文件编译成 .c .h 文件 放到 trans 文件夹下，以供 程序使用。

   编译生成的 c 程序就是将上面 原文（比如 `title1`）和 对应语言（比如 `标题1`） 的字符串 写成多个大数组，根据最后设置的语言，通过调用 `_("xx")` 查表返回而已。

   trans 文件夹需要预先手动创建。

   ```bash
   lv_i18n compile -t "trans/*.yaml" -o "trans"
   ```

   测试用：

   ```bash
   lv_i18n compile -t './*.yaml' -o "trans"
   ```

6. lv_i18n 的 c 程序 api 在 lv_i18n 文件夹下的 .h 文件里，调用即可。

   ```c
   #include "lv_i18n.h"
   
   int32_t ret = lv_i18n_init(lv_i18n_language_pack);
   if(!ret) { ... }
   ret = lv_i18n_set_locale("en-GB");
   if(!ret) { ... }
   
   ...
   
   ret = lv_i18n_set_locale("<其它语言编号>");
   if(!ret) { ... }
   
   ...
   
   // 这里就需要刷新所有 label
   ```



一些注意的地方：



添加翻译的文本一些注意：

- 文本最好都是一整句话，不要有半个句子，其它多语言会翻译不了或者硬翻译后多个这种半个句子连起来就是语法错误。
- 文本里有 变量 要显示的，即一个多语言字符串中间要带有变量来显示的，统一用 `%1、%2..` 来代替，程序里会查找替换。（继承自 qt 的写法，C++ 端用字符串替换即可），不要把一句话分成多段！
- 文本末尾最好不要留有空格，可能会被工具链上某个工具优化掉。
- UI 上显示文本的地方放一个 label，后端根据不同机型、功能的宏来区分显示。动态切多语言的方案就看上面。
- 条款文案之类的，有固定的具有法律效益的翻译文本，不要用其他人自己翻译的，手动往 localazy 上加上。
- 一些 ui 上遇到的显示不出来的特殊符号、格式错误等等，可能是个别语言翻译后，本地字体不支持等原因造成，要么就在 localazy 上手动修改为本地字体支持的，要么在字体文件里面添加支持（字体编辑可以用 fontForge 等软件。字体可以下载使用 google font [Browse Fonts - Google Fonts](https://fonts.google.com/)）。



需要特殊处理的地方：

把 lv_i18n.c 里面的：下面的按照顺序执行

- 经测试，localazy 会把 上传上去的 `\n` 和 `\\` 再下载下来后 转换为 `\\n` 和 `\\\`，需要全局搜索替换来还原。。但是 `\"` 就是正常的。。
  - `\\\` 全部替换为 `\\`。 
  - `\\n` 全部替换为 `\n`。
  - `\\"` 全部替换为 `\"`。

- 看一下有没有空字符串：搜索 `, ""}`，若有 则需要解掉（除了 localazy 上面主动 hide 掉的）



特殊注意的地方：

- 注意不要直接改 localazy 的内容（需要告诉其它人员），更新最新提取的文案文件到 localazy 上面就把改动覆盖回去了。

- 翻译好之后在 localazy 的 项目里，Tools -> File management 里面下载，选择所有语种、保持原始格式 以及 组织格式选择 `{file}/{locale}.{extension}`，下载 .yaml 文件。



#### 动态切换语言方案（推荐）

- 对于 UI 前端静态显示的文本：squareLine 生成的 ui 前端（ui 文件夹），要翻译的 label 都勾选 "to translate"，生成的程序会带上 lv_i18n 的 _("xxx") 标识，是个宏，即查找 xxx 字符串 对应语言的字符串并返回。

  使用 脚本 提取 ui 文件夹里面 所有带着个标记的函数，生成比如 `allTransFuns.h`，切语言的时候调一下，则刷新了 ui 文件夹 里面所有 静态 label 的语言。

  squareLine 1.5.3 版本 开始 支持导出 刷新 ui 多语言 label 的函数，但是这个版本还有 bug，已经给官方提（https://forum.squareline.io/t/ver-1-5-3-ui-page-screen-relocalize-not-containing-checkbox-and-others-translation/5991），后续也许会改。

- 提取标记的字符串和取得指定语言的字符串，这个可以自己实现，也可以使用库 `gettext`。

  官网 [gettext - GNU Project - Free Software Foundation](https://www.gnu.org/software/gettext/)。

  参考教程 [使用gettext进行多语言国际化 - 知乎](https://zhuanlan.zhihu.com/p/669282869)。[gettext安装及使用-CSDN博客](https://blog.csdn.net/xc_zhou/article/details/151229263)。

- 对于 程序控制动态生成的文本显示，比如组件的创建和删除等：
  - 对于所有 label，使用 `XXX::setTsLabel(lvObjPtr, ts("xxx"));` 来设一下（如下示例程序），里面记录这个 obj 和 文案的英文原始字符串，里面在切换语言的时候 会 刷一遍 这些 label obj，就可以在切换多语言的时候自动也刷新了这些 label。在动态组件删除的时候需要调用 `removeTsLabelObj()` 来从多语言切换中删除。

    程序控制要更新文本的 label，在 squareLine 里面不要勾 "to translate"。

    其中 所有 要多语言的字符串，使用 ts("xxx") 标识（目前暂时就是个 `#define ts(str)  str`），用于脚本提取并上传 localazy 或 什么多语言进行翻译和管理的地方。

    示例片段：

    ```c++
    // #define ts(str)  str
    
    std::unordered_map<lv_obj_t*, std::string> mTsLabels;
    
    int32_t XXX::setTsLabel(lv_obj_t * _lvObj, const std::string& _str)
    {
        if (_lvObj && lv_obj_check_type(_lvObj, &lv_label_class)) {
            lv_label_set_text(_lvObj, _(_str.c_str()));
            mTsLabels[_lvObj] = _str;
        }
        return 0;
    }
    
    int32_t XXX::removeTsLabelObj(lv_obj_t * _lvObj)
    {
        if (_lvObj && lv_obj_check_type(_lvObj, &lv_label_class)) {
            mTsLabels.erase(_lvObj);
        }
        return 0;
    }
    
    // 切换多语言时候，刷一遍所有 需要翻译的 label
    // all the lang trans needed labels that backend used, set and added by "setTsLabel()"
    for (auto it = mTsLabels.begin(); it != mTsLabels.end(); ) {
        if((it->first) && lv_obj_check_type((it->first), &lv_label_class)) {
            lv_label_set_text(it->first, _(it->second.c_str()));
            ++it;
        } else {
            LOGW("there is empty or none-label type obj in mTsLabels, obj: %p, str: \"%s\", del this.", (void*)it->first, it->second.c_str());
            it = mTsLabels.erase(it);
        }
    }
    ```




### 文件系统接口

官方文档参考 [File System (lv_fs_drv) - LVGL documentation](https://docs.lvgl.io/master/main-modules/fs.html)。

lvgl 源码已经集成了前几个 文件系统接口 API，选一个即可，win & linux 系统用 STDIO 或 POSIX 即可，mcu 移植了 fatfs 即用 FATFS。

```
LV_USE_FS_STDIO         API for fopen, fread, etc
LV_USE_FS_POSIX         API for open, read, etc
LV_USE_FS_WIN32         API for CreateFile, ReadFile, etc
LV_USE_FS_FATFS         API for FATFS (needs to be added separately). Uses f_open, f_read, etc
LV_USE_FS_LITTLEFS      API for LittleFS (library needs to be added separately). Uses lfs_file_open, lfs_file_read, etc
```



使用 lvgl 的文件 IO API，路径前要加 `前缀字母:`，前缀字母由 `lv_conf.h` 里面的 `LV_FS_STDIO_LETTER` 定义。

可详见 下面 `文件操作 lv_fs` 一节。



### 图片解码库显示图片



传统图片格式占用空间较大，可以尝试引入 webp 格式（有现成的编解码库），支持静态图片和动态图片，且占用空间显著减小。看到 LVGL V9 已经支持了。



图片解码也许稍微更多耗时，可以使用图片缓存，只解码一次，LVGL 内部支持，需要在 lv_conf.h 里面开启，依靠传入的 图片结构体的地址 lv_image_dsc_t* 判断每张独特的图片是否使用缓存的还是重新解码。



**显示图片的两种方式**

- C array（RAM or ROM）（见下面 `显示数组图片数据` 一节）。直接显示 解码后的 图片 RGB 数据。
- from file(s)（见下面 `图片文件解码显示` 一节）。显示图片文件，分具体编码格式的。



#### 显示数组图片数据

参考官方手册 https://docs.lvgl.io/master/overview/image.html#manually-create-an-image

下面例子，具体使用需要因地制宜。

```c
// temp_img.c
uint8_t my_img_data[] = {0x00, 0x01, 0x02, ...};

lv_image_dsc_t my_img_dsc = {
    .header.always_zero = 0,
    .header.w = 80,
    .header.h = 60,
    .data_size = 80 * 60 * LV_COLOR_DEPTH / 8,
    .header.cf = LV_COLOR_FORMAT_NATIVE,          /*Set the color format*/
    .data = my_img_data,
};

// temp_img.h
LV_IMG_DECLARE(my_icon_dsc); // 这个其实是 extern const lv_img_dsc_t var_name; 用于固定的数组
// extern lv_image_dsc_t my_img_dsc;

// main.c
#include "temp_img.h"

lv_obj_t * icon = lv_image_create(lv_screen_active(), NULL);

/*From variable*/
lv_image_set_src(icon, &my_icon_dsc);

// 为了显示图片数组，其实构造一个 lv_image_dsc_t 然后传给 lv_image_set_src() 就成
// lv_image_set_src() 可接受 lv_image_dsc_t 数组指针 和 图片文件路径，会自己区分。
// 若通过 lv_image_dsc_t 传入 编码的图片二进制流的数据，lvgl 内部也会判断并挨个调用支持的图片解码器尝试解码，直到成功解码并送显。
```



#### 图片文件解码显示

这里是 from file(s) 的方式显示图片。

[Image Support - LVGL documentation](https://docs.lvgl.io/master/libs/image_support/index.html)。



**图片格式判断**

用图片文件后缀名不准，会有后缀名与图片实际编码不一致的情况，通过图片文件内容判断图片格式参考： https://blog.csdn.net/qiangzi4646/article/details/80764262，或者 文档 `QT QML 总结备查` 的 `显示图片` 一节，有程序例子。



lvgl 的 `lv_image_set_src()` 接口里面判断本地文件图片格式的方式：是逐个图片格式的解码器去试

> When an image needs to be drawn, the library will try all the registered image decoders until it finds one which can open the image, i.e. one which knows that format.

但是看源码，比如 loadpng 库，里面还是根据文件后缀名是否 png 来判断：

> decoder_open() 里面 if(strcmp(lv_fs_get_ext(fn), "png") == 0) { ... }



**png**

 lvgl 官方源码中 自带 `loadpng` 库 并 集成了， `lv_conf.h` 里面打开 `LV_USE_PNG` 宏，然后 参考 上面链接里的例子

```c
img = lv_image_create(lv_screen_active());
/* Assuming a File system is attached to letter 'A'
 * E.g. set LV_USE_FS_STDIO 'A' in lv_conf.h */
lv_image_set_src(img, "A:lvgl/examples/libs/lodepng/wink.png");
```



也可以自己引入别的解码库并绑定 lvgl 回调 API，在 LVGL V9 版本中还引入了 libpng。



打开宏之后，这么模块的 init() 就在 lv_extra_init() 里面被打开，在执行 lv_init() 的时候就被调用。



**bmp**

 `lv_conf.h` 里面打开 `LV_USE_BMP` 宏即可。

```c
lv_image_set_src(my_img, "S:path/to/picture.bmp");
```

> **Limitations [BMP Decoder - LVGL documentation](https://docs.lvgl.io/master/libs/image_support/bmp.html#limitations)**
>
> - **Only uncompressed BMP files are supported. BMP images as C arrays ([`lv_image_dsc_t`](https://docs.lvgl.io/master/API/draw/lv_image_dsc_h.html#_CPPv414lv_image_dsc_t)) are not supported. This is because there is no practical difference between how uncompressed BMP files and LVGL's image format store the image data.**
> - The BMP file's color format needs to match the configured [`LV_COLOR_DEPTH`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_COLOR_DEPTH) of the display on which it will be rendered. You can use GIMP to save the image in the required format. Both RGB888 and ARGB888 work with [`LV_COLOR_DEPTH`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_COLOR_DEPTH) `32`
> - Color palettes are not supported.
> - **Because the whole image is not loaded, it cannot be zoomed or rotated.**



**jpg**

同上，lvgl 内部默认使用 TJpgDec 库。

使用其它 jpg 解码库，在 LVGL V9 版本中还引入了 libjpeg-turbo。



**gif**

```c
img = lv_gif_create(ui_bgPanel);
lv_gif_set_src(img, "L:C:/Users/.../xxx.gif");
lv_obj_center(img);
```



gif 动图显示，实践发现是解析一帧才显示一帧，如果机器性能有限则播放起来一卡一卡的，可以自己写个功能，调用 lvgl 的解码相关的 API，对一系列的图片先解码为解码后的二进制数据数组，然后用定时器逐个显示来播放。虽然这个需要解码的时间也比较显著而且占用很多内存。或许考虑其它方法。



#### 大尺寸图片在小 panel 里 显示的适配

```c
// 这样计算下，可正常显示
// img 的对其必须 设置为 CENTER，x 和 y 都设 0，假设 panel 宽 240 高 194，下面计算 zoom 比例（0~256），并偏移
// 这里是根据 外框的宽度 对图片进行缩放，图片的左右会贴合外框，如果图片比较高则适合这种，缩放后没有空隙
lv_img_set_src(modelImg, &ui_img_image_xxx_png);
lv_img_set_zoom(modelImg, (uint16_t)((240.0 / (double)ui_img_image_xxx_png.header.w) * 256.0));
lv_img_set_pivot(modelImg, ui_img_image_xxx_png.header.w / 2, ui_img_image_xxx_png.header.h / 2);

// 这里是根据 外框的高度 对图片进行缩放，图片的上下会贴合外框，如果图片比较宽则适合这种，缩放后没有空隙
// 中间那句改成这个
lv_img_set_zoom(modelImg, (uint16_t)((194.0 / (double)ui_img_image_xxx_png.header.h) * 256.0));

// 宽的图片按照高度填充，高的图片按照宽度填充
```



### 视频显示 / 对 ffmpeg 的支持

参考文档 [Video Support - LVGL documentation](https://docs.lvgl.io/master/libs/video_support/index.html)。支持 FFmpeg 和 GStreamer。



lvgl 调用 ffmpeg 的 API 显示任意格式图片和播放视频。开启了这个 则 上面的 独立图片 解码 选项就不能开了。



提供的 API 见 `lv_ffmpeg.h`，基本都是播放视频的，可以控制视频开始、暂停、继续、停止等，可以设置循环播放等。调用 `lv_ffmpeg_init()` 会把 lvgl 的 图片解码 回调 绑给 ffmpeg 的 API，即再调用 `lv_image_set_src()` 就是使用 ffmpeg 来解码、显示图片。

但是库比较重，按需求和约束来。



在 linux 上，显示本地图片（输入图片文件路径）可以上 ffmpeg，支持所有图片格式，还可以播放视频，显示内存图片（如读压缩包里面图片，网络下载到内存的图片），使用 lvgl 图片数组显示的方式。

对于 mcu 等 显示本地图片（注册文件系统 API，读 FLASH 等地方的图片文件）可以用 lvgl 自带的 各独立格式的图片解码器（上面 `图片解码库显示图片` 一节的方法）。



## 关于 crash (Segmentation fault) 的跟踪



注意，下面会列出追踪问题的过程，可以看看，解决实际工程问题，最终结论的方法更重要。



结论总结：

- 多线程中调用 lvgl 的 API 全部加互斥锁（这个开销比较大） 或者 保证在同一个线程里面被调用，并保证执行顺序，除了 lv_event 和 lv_timer 的回调函数 等地方里面不用加（这些是在 lv_timer_handler() 里面被调用，即这些都是运行在 lvgl 的 context 里面）。

  具体看移植文档 [Overview - LVGL documentation](https://docs.lvgl.io/master/integration/overview.html#)。

  - 包括 lv_mem_alloc() 这种 API。
  - squareLine 生成的 ui 开头的 API 全部加 同样的 互斥锁，并保证执行顺序。
  - 包括 squareLine 生成的 动画 相关 API。
  - lv_timer_handler() 以及其它所有 lv_ 相关的 API 都要加（lv_tick_inc() 可以不用加互斥锁）。

- 操作 obj 之前 先检查 判空，例如：

  使用 ui_comp_get_child()（squareLine 生成 代码里面的 API，用于获取一个 compontent 组件 obj 的子 obj） （这个里面发送 get_child 的 event 然后死等返回）返回的 lv_obj_t* 变量，在对其使用 lvgl 的 API之前，先检查该指针是否有效。

- 特定 widget 类型的 obj  不能用 其它 widget 类型的 API 去 set/get，可以用 `lv_obj_check_type()` 来检查。

- lv_obj_is_valid() 函数应该全局不能被调用。原因看下面。



以下是一些 crash 跟踪过程：

查了一些lvgl仓库相关的issue: https://github.com/lvgl/issues?q=_lv_event_mark_deleted

可以尝试的:
1、CHECK_LV_OBJ 中的 lv_obj_is_valid() 遇到 crash，可以去掉，官方说这个 API 不安全，实际上 LVGL 源码里面也基本没用这个API，see https://github.com/lvgl/lvgl/issues/6035:

> lv_obj_is_valid is not safe to use this way. It can happen that a widget wwas freed and on it's exact memory address an other widget was allocateed.
>
> lv_obj_is_valid will say that it's valid, but it's still not the widget thhat you wanted.



squareLine 1.4.x 版本：

lv_obj_is_valid() 函数应该全局不能被调用，这个太容易 crash 了，比如 squareLine 生成的 ui_theme_manager.c 里面调用到就有crash的时候。。索性将这个文件里面的所有 都改掉：之后 squareLine 导出 ui，就不用更新 ui_theme_manager.c 这个文件了，这个一般也不更新，就固定了

```c
if ( object_p!=NULL && lv_obj_is_valid(object_p) ) {
改成
if ( object_p!=NULL ) {
    
if (object_p==NULL || !lv_obj_is_valid(object_p) || theme_variable_p==NULL) return;
改成
if (object_p==NULL || theme_variable_p==NULL) return;
    
然后 _ui_local_style_property_setting_create() 函数里面的需要结合上下文分析下逻辑，由：
if (style_property_setting_p->object_p == NULL) empty_style_property_setting_p = style_property_setting_p; //if found empty position, register it
                else if ( !lv_obj_is_valid( style_property_setting_p->object_p ) ) { //if not, free up an entry of a deleted widget
                    empty_style_property_setting_p = style_property_setting_p;
                    style_property_setting_p->object_p = NULL;
                }
修改成：（即 else 里面的直接删掉）
if (style_property_setting_p->object_p == NULL) empty_style_property_setting_p = style_property_setting_p; //if found empty position, register it
```

ui_theme_manager.c 在修改并提交一次后，后面都应该不要更新，所以以后每次更新 ui 文件夹，git 执行一下：

```bash
git checkout -- ./frontend/ui/ui_theme_manager.c
```



squareLine 1.5.x 版本：

ui_theme_manager.c 已经被官方修正了，可以直接用导出的。



lvgl 仓库 关于 lv_obj_is_valid() 替代品 的讨论：https://github.com/lvgl/lvgl/issues/6395

v9 对每个 obj 用上了 id，这个可以有。



2、lv_event_mark_deleted出现问题,可能在于事件链成环了永远无法退出遍历循环,或者事件代码出错,可以加代码防止出现这个试试

https://github.com/lvgl/lvgl/issues/6035



https://github.com/lvgl/lvgl/issues/2388

这个里面说到 lv_event_send 里面的e是栈内存，改成了申请的谁内存就不出错了，试试。首先还是把 LVGL 的 API 调用 的互斥锁加全，或者保证都在一个线程里面运行。



进一步跟踪：

经过测试，多线程运行 LVGL 不加锁，必现 segment falut 在 _lv_event_mhark_deleted()，查看变量是 event->code 是乱码，由于在eventsend 里面 event 的链表是用栈临时搭建的节点处理后再退出函数释放掉，对于多线程若不加锁则很容易访问到 event 的野指针。。也印证了上面 https://github.com/lvgl/issues/2388 这个里面说到 lv_event_send 里面的 e 是栈内存，改成了申请的堆内存就不出错了。。

经过本地测试工程测试，加全互斥锁后（或者都保证运行在一个线程里面），运行很好，高频操作和刷新 UI 没有遇到 crash。



LVGL 的 API 不是线程安全的，多线程应用中，官方建议：

**调用 LVGL的 API `lv_xx()`，保证两点：1、按照程序里面的执行顺序执行，2、互斥 或者 都在一个线程里面执行（使用单线程的线程池的提交 或者 单线程执行的函数的队列）**，即可基本保证 LVGL 的稳定运行。



由于一开始用不熟悉、多人合作、工程量大等，手动加互斥锁 或者 保证运行在一个线程里面，没有得到保证，为了检查 所有 LVGL的 API `lv_xx()` 是否都运行在一个线程里面，可以通过 GCC 的 `-finstrument-functions` 编译选项 给所有 函数添加 入口 和 出口 函数，来检查。



## SquareLine & LVGL 工程注意事项、前后端对接方案、产品差异构建



### SquareLine 经验 & 规范 相关



#### 软件设置 & 控件命名等规范



- 软件设置：

  Undo history size：10

  存太多历史会急剧占内存，尤其工程比较大的时候，再者，这个软件 Undo 极其不好用，轻易 Undo 很容易丢东西！对于这个软件要养成习惯尽量不用 Undo，每一步操作都当作不可撤销的，时刻清醒操作。

  且官方提醒（https://forum.squareline.io/t/v1-4-0-cpu-usage-is-too-high/2616/4） 目前 1.4.0 版本 Undo 设置比较大 会非常占 内存 和 CPU，直接关掉 off 软件会快很多。

- 工程设置：

  DISPLAY PROPERTIES

  - Width: 1280，Height: 720，Depth: 32 bit
  - Rotation: 0 degree，Offset X: 0，Offset Y: 0，Shape: Rectangle

  Object naming（1.4.0 之后的版本支持）：[Screen_Widget]_Name（选择后就不要改了！！！否则程序里面用到 obj 的要跟着改）

  BOARD PROPERTIES

  - Board Group: Desktop
  - Board: VS Codewith SDL for development on PC
  - LVGL：8.3.11（改为需要的）

  LVGL Include Path: lvgl.h

  Multilanguage support: Enable

  Call functions export file: .C

  Force export all images: √（不勾上这个，则没有放置的 comp，其中用到的 img 不会导出...）

- SquareLine 工程 的 Compoment 可以在不同 工程之间复用。

- 首要注意在 SquareLine 里面添加每个组件的命名规范，都要有意义命名，尤其是 screen name、obj name（event name 不会导出到 ui 所以可以不设置）、call function name（对于按键 btn 的 call back function name，这里建议要设置与 obj name 相同） 等，因为导出代码后这些直接体现在源码中，方便看。

  各个控件的 SquareLine 做法规范：

  - 前置规则，所有控件的命名都需用驼峰命名法，不能有空格！
  - 各个控件的命名按照下表规则加类型后缀。

  | 控件                                      | 做法                                                         | 命名                                                         |
  | ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 页面                                      | 新建 screen。<br />添加 `SCREEN_LOAD_START` 事件，执行 `call function`，函数名格式为：`<screen_name>Init`，如 `XxxPageInit`，留着后续可能添加一些 page load 时候 需要执行的工作。<br />添加 `SCREEN_UNLOAD_START` 事件，执行 `call function`，函数名格式为：：`<screen_name>DeInit`。 | name 要以 `Page` 结尾，<br />如 `XxxPage`。                  |
  | 按键                                      | 使用 panel 做（lvgl 的 button 控件带点击动态导致感觉反应迟钝所以弃用）。<br />均为 `LV_EVENT_CLICKED` 事件。<br />panel 默认带的 boder 设置 width 为 0，设置 press 状态 下的 Style，添加 click 事件，执行 `call function`，函数名一般与 这个控件 name 相同即可。<br />并且，所有 btn 的 press lock 这个 flag 都去掉，不勾选这个是 press 后鼠标移开 控件就会恢复 defult 状态而不会响应 click。<br />squareLine 中放置按键看一下 press 状态，要有变化，一些按键还有 disable、checked 状态 的 Style 要设置。 | name 以 `Btn` 结尾。<br />如： `XxxBtn`。<br />全局唯一，要有意义，一般为 `所属页面-所属功能-按键功能` 格式。 |
  | 开关 / 选择框(开关类)，下拉框(多项选择类) | 对应 switch / checkbox，chooselist，均做为设置好的 component 直接调用。<br />均为 `LV_EVENT_VALUE_CHANGED` 事件。<br />其它与上类似处理，如 obj name、call function name 规范等。<br />为了 UI 操作比较跟手，开关之类的，可以点击后 先切换，打不开、失败之类的再切回去。 | name 结尾分别为：<br />`Switch` / `CheckBox`，`Choose`。<br />这三个控件的信息都存在程序后端，首次打开页面和更新都是后端控制，前端不保存信息（开关状态、下拉框内部选项等）。<br /> |
  | 进度条 / 滑动条                           | 对应 Bar 控件 或 slider 控件                                 | name 结尾标注：`Bar` 或 `Slider`，<br />如：XxxBar。         |
  | 文字                                      | 使用 label。<br />需要照顾多尺寸、多语言情况下的显示情况，调整 label 的长宽，设置换行、省略号或者滚动等文本超长时候的显示模型。 | 对于要 c/c++ 后端程序去 改变 / 设置 文本的 label：要其 obj name 以 `Str` 结尾，如 `xxxStr`（可以适当缩减长度，界面中唯一标识且看得懂即可）。<br />其它 label 的 name 无要求。 |
  | 图片                                      | 放上 image 控件，后端程序设置其 source 即可。<br />图片控件必须在一个 parent panel 里面，且这个 panel 的长款必须是确定的 px 或者 某种大小。<br />图片上面的文字、按键都要有深色背景，防止和图片的干扰。 | name 以 `Img` 结尾，其它规则同上。                           |
  | 动态 List                                 | 里面可动态增减 obj，带滚动条。做成 component 如 `InstListViewPanel`。<br />list 里面的 obj 不要加 `Scroll on focus` 这个 flag，否则一点就跳过去很烦。 | name 包含 `InstList` 。<br />                                |
  |                                           |                                                              |                                                              |
  | 各种可复用的用c++封装的组件               | 如 各种弹窗、键盘、菜单项 等等。<br />squareLine 里面 和 c++ 均遵循继承和多态的封装习惯。 |                                                              |
  |                                           |                                                              |                                                              |




#### 设计 & 生成 ui 相关



- 设计 & 生成 ui 相关。

  - 因为 squareline 每次生成界面代码，ui 文件夹 均会被覆盖，除了 ui_events.c 里面 回调函数里面，所以可以直接在生成代码的 ui_events.c 里面 回调函数里面 填上自己的 回调函数，每次 执行 生成 ui 代码 这里不会覆盖。在 ui_events.c 文件里面手动添加自己相关的头文件，以及填充回调函数，squareLine 再导出 ui 这些不会覆盖丢掉。但是！若执行生成 模板工程，则整个目录将被覆盖，这里就没了。。

  - 纯前端的，比如点击按键其他组件会移动，等等这些 UI 上的固定的动作或动画，都在 SquareLine Studio 去做，然后给界面上所有 具有 点击功能 的地方 都 设置 回调函数。

    但是 跳转界面 不要在 SquareLine Studio 里面做，因为可能随着需求增加，需要后端程序控制复杂的页面跳转逻辑。
    
    一般的，一个控件先设置好 default、press、checked 和 disable 四个状态时的外观（视情况只设置用到的也许，btn 一般为 default、press），然后添加各种 event。
    
    添加 多个 event，后添加的在 squareLine 排在上面，生成的程序会是 从上往下执行；若是在一个 event 里面的多个 action，生成的程序 会是 从下往上执行。
    
    一般， event 里面要先 调用回调函数，再执行其它动作如跳转页面，在 squareLine 里面设置 event 时候，最后添加一个 ACTION 为 CALL FUNCTION（先添加的在下边，实际在程序里面会最后调用），要先添加其它 ACTION，这样生成的代码会先 先 调用回调函数 再执行其它动作。当然会有例外，有的 btn 是先添加 clicked 执行给自己添加 checked，然后再 添加 在 checked 的时候 call function。
    
    在 squareLine 里面 设置 state 的变化为 event 的触发，之后只改变 state 是不会触发 event 的，比如 BtnA 设置 event 为 clicked 后 给自己加 checked 状态，然后 再添加一个 event 为 checked 后再执行一个 action，开始模拟运行，只运行 “clicked 后 给自己加 checked 状态”，不会执行 “checked 后再执行一个 action”，思考为 执行第一个 action 单纯为 lv_obj_add_state，并不会 lv_event_send，所以第二个 action 不会执行。
    
  - 添加 event 的 action 调 函数，函数名尽量从 obj 的 name 直接复制过来（再修改或不修改）。obj 的 name 重复会有报错，而 函数名一样 不会报错，如果有重复，则会出现两个按键调用一个 函数。

    已经确定的 obj name 和 回调函数 name 之后不要动了（尽量）。

  - 所有交互控件（btn / checkBox / switch / choose）都要添加对应的 回调函数。都生成在 ui_event.c 里面，方便后续做埋点之类的。

  - 所有的交互控件，可点击的，flag 里面 都去掉 Press lock，即 当点击 未松开 但 移开 之后，不会响应。

  - 所有的 checkBox 和 switch 默认都是 不选择 和 关闭 的状态，和需要后端拿数据的 choose 都是空的，即都从后端去设置，即 前端 UI 不保存信息。

- 新添加 panel，默认是带 border 这个 style 的，可以 设置 其 Border width 为 0 即可清掉。而且还默认带 paddings，这个里面的 width 一般都设置 0，则 往这个 panel 里面添加 子控件会以 这个 panel 的真正边缘计算位置。

- 所有与后端交互的地方，都留回调函数，即 squareLine 里面添加 event 是 call function 即可，后端填空。有变化的控件，比如 图片、文字 等等，放上留空，然后后端控制即可。

- 复用的控件，建立 component，在 squareLine 里重复使用，并且导出代码后这个 comp 也会导出成 一个 obj，提供了一些 API（在 在生成代码的 `ui/components` 文件夹里面 .h），后端可以创建（在 compoment 名字文件的 .h 文件里），get 其所有子 obj（在 `ui_comp.h`），还有每一种 component 的 init 的 hook 回调函数等（在 `ui_comp_hook.h`，A hook is called at the end of each component create function allowing to add custom features.）。这个逻辑适用于比如弹窗等。详见下面 `SquareLine Component 使用` 里面的使用例子。

  - 一些 ui 上固定的 component，就直接放到 ui 上，并添加响应的 btn cb 和 设置 text 与 勾选或不勾选 To be translated。

    添加到 ui 上的 组件实例，其子 obj 再命名 在 导出代码后不会出现，寻找其 子 obj 需要用 get_child() 方法 见下面 `SquareLine Component 使用` 一节。
    
  - component 里面的文本，除非是固定的，要例化之后再给文本的 就不要勾选 To be translated（temp text 这种临时文本不需要翻译）。参考上面多语言章节。

  - 一般 component 里面的 按键的 callback 都要在 后端去 add cb 并实现功能，**squareLine 里面 创建/编辑 component 的时候 不添加任何 call function**，因为 squareLine 用这个 component 往界面上加多个，然后这多个 component 的实例的 call function 都一样 并且声明放到了 ui_event.h 里面就不好，除非有例外才用。
    
  - squareLine 里面创建的 component 都在工程文件夹 components 里面，可以复制粘贴到其它工程进行复用。

  - 暂时不用的 screen 或者部分 ui 界面，勾选 `Don't export screen`。另一种方法，但不推荐：为了省生成 ui 代码的空间需要删掉，但是不要立马删掉（保不齐后面又用到），先打包成 component，这样就存下来了，ui 上的就可以删掉了，如果后面又用到，那么 ui 上先添加这个 component 然后再解散（点击 `DETACH`） 就还原了。

- 当作按键的组件，里面的 panel 可能比较多比较复杂，为了简化点击的事件传播链，在编辑组件的时候，最后添加一个 长宽均为 100% 的 透明的 顶层 obj 下的 panel（一般命名为 EventBubblePanel），将其 flag 勾选上 clickable 和 event bubble，再将其 顶层 obj 的 flag 勾选上 clickable 即可。如果要 设置 这个 组件 实体 可点击 或 不可点击，只要设置 去掉 EventBubblePanel 和 顶层 obj 的 clickable 这个 flag 即可。

- 组件的布局，嵌套的是使用相对位置。排列的，用 Flex Flow 方式，即 panel 设置 layout 为 flex，可以设置其子控件的排列方式。放置控件的大小尽量用 百分比 设置，这样会随着 parent obj 变化而变化，复用性和兼容性更强。

- listView。设置类似 qt listView 的效果，用于如 设置项列表、文件浏览列表 等等。具体看 squareLine 工程里的实现：添加一个 panel（名 xxxInstListPanel，表示这是个 装各种 控件 instance 的 list 的 panel），并打开 Scrollable，其它 scroll flag 除了 Scroll chain 均打开，设置其确定的宽高度（px 或 % 单位），Paddings 里面 pad 上下左右均设为 0 且 pad row / column 按需设置。那么往这个 xxxInstListPanel 里面 create obj，新建的 obj 会自动排列，实现动态增减其中的项。

  - Scrollbar mode，一般选择 AUTO，即当内容超过外框后就一直显示 滚动条。

  - 对于自动或手动滚动显示效果的做法，可以是：比如 4x4 个 component 放到 一个 InstList 里面，4行4列，设置对齐 snap 特性（可选），不设置能手动滑动，然后程序中，定时上下翻页即可，即使用 lv_scroll_xx() 相关 API，可选设置使用 动画 的方式滑过去。

    后端添加 snap 和 给上下翻页按键加功能，见 `API 备查` 里面。翻页组件比如 pagingPanel。 

  - list 里面各项之间一般还加分割线，如果外框 panel 宽度固定 且 里面各项宽度加起来要正好填充这个宽度，可以这么做到只中间加：假设外框 panel 宽度 640，然后在里面添加两个 321 宽度 的 btn panel，这两个 btn panel 只设置 一侧有 border 线即可。如果里面 btn panel 是组件，则每个组件可以 一侧有 border 线 宽度 先为 0，在程序中创建后，再把中间组件的这些 border 线 宽度 设为 1 并最后一个保持 为 0，即达到列表项中间都有分割线的效果。

- UI 上 一些 label 给的默认值，宽度要足够占最长的位，且内容要预期的格式但是字符明显是默认值或人为设定值，与实际值区分。如 序列号为 1234567-7788110，机器名称为 XXX-666-223，使用时长为 999h，固件版本号为 00.00.00.01 等等。

- 字体管理，考虑到涉及到多语言等情况，直接参考 `多字体 & 字库支持` 一节中推荐的做法。

- 主题管理，V1.4.1 版本及之后比较好用了，可以用：先定义一些标准颜色，所有 ui 上的 obj 以及 组件 的 panel、文字 等控件的颜色均用标准色组成，然后定义多套，可以随时切换。参考 https://docs.squareline.io/docs/themes。

- 更多内容见 `优化相关` 一节里面。



squareLine 导出 ui 可以用脚本：

https://docs.squareline.io/docs/commandline

例子：You can export (and overwrite) the `ui` folder with: `./SquareLine_Studio.x86_64 -batchmode -logFile - -projectfile "ExampleProject/SquareLine_Project.spj" -exportfolder "ExampleProject/export" -ui_exportfolder "ExampleProject/export/SquareLine_Project/ui"`。



#### 软件使用上的一些问题 和 解决

- squareLine 软件 遇到的不便和问题，给官方 Forum 提了了几个，看看后续版本会不会支持上：

  https://forum.squareline.io/t/some-inconveniences-and-reduced-efficiency-during-use-hoping-add-target-obj-searching-and-so-on/2389

- 如遇到 软件打开一个工程打不开，但是打开别的工程可以，先备份一份工程文件夹，再去工程的 backup 文件夹里，拿出 最近打开不的版本的 前一个，替换外面的工程文件，再试试。

- squareLine 打开的时间长了会很占内存以至于开始卡（软件问题，之后新版本（1.4.0）好一些），要么增加电脑内存，要么软件关了再重新进。

  如果 squareLine 工程比较大 导致 内存 或 cpu 占用高，导致很卡：
  - 若卡，软件主视图的右上角有图片图标，使用有锯齿的，减小软件压力。
  - 卡了不行了就重新打开软件。这软件一阵一阵的，有时候 CPU 占用很高就卡，有时候 内存 占用很高就卡，有时候就比较正常。
  - 如果实在卡的不行了就没有好过，考虑个中下策：可以再开一个工程 在里面做 UI，然后整个打包生成一个 组件，再转移、添加到 主工程里面。
  - 关于将 一个 大型、复杂 UI 划分成 多个 squareLine 工程，然后进行合并和一起使用：https://forum.squareline.io/t/v1-4-0-cpu-usage-is-too-high/2616/2，可行，但不推荐。

- 不要在 `initial actions` 里面添加 切页，软件会无法模拟运行，一运行就闪退。

- 导出 ui，某些组件里面总有 TemporaryImage，且用脚本导出的时候是必现的组件，发现这些组件是没有添加到 ui 上的，就尝试将这些组件添加到 ui 上 再隐藏，再导出发现没问题了。。

- 问题：运行脚本去生成 ui，程序里面出现过 组件里面 少设置东西 的情况，在 squareLine 里面点击导出又好了，但有时候 squareLine 导出的也有这样的问题。所以统一，每次 squareLine 导出，先删掉 ui 文件夹。



SquareLine 优化使用 相关

在 SquareLine Studio 里面

- 尽量不用透明度（显著占用CPU）.
- 切换屏幕在性能一般的机器上尽量不用平移动画（比如 MOVE LEFT）（会有严重的撕裂），可以渐隐的方式（FADE OUT），但可不用动画，设置转换时间和延时均为 0。
- 软件有 bug，偶尔抽抽，若点击播放、设置属性没有变化、没有响应，重启软件试试。
- 不要点 撤回 ctrl + z，会随机回退很多步，或者干脆软件开始摆烂，对于没保存很危险，干脆不要点上一步了。。



#### 导出代码处理 & 优化 / 检查项 & 添彩项



导出代码后的处理：

- 对于如果使用 squareLine 内置的字体管理（不推荐，参考 上面 `多字体 & 字库支持` 章节，推荐使用 ttf 字体文件），有时导出后，明明没有更新 字体 相关的设置，但字体文件在 git 里面 显示有改动，其实在 gerrit 上一看 改动的增加大小分别正好是 源文件大小，那就不要更新 字体文件到 提交里面。 

- **需要特殊处理的地方：**根据 crash 一节，ui_theme_manager.c 在修改并提交一次后，后面都应该不要更新，所以以后每次更新 ui 文件夹，git 执行一下：

  ```bash
  git checkout -- ./frontend/ui/ui_theme_manager.c
  ```



后期需要 polish 优化处理的地方，以及检查的地方：



- 检查所有 screen 中：
  - screen load start 事件 call function（`xxxPageInit()`）。所有 nav btn 的 call function（相同按键调用相同函数）。
  
  - 所有 label 的字体检查：
  
    - 纯数字用内置字体，其它用 生成的字体。
  
    - 要翻译的 label 勾选了 翻译选项，不用翻译的不勾。
  
      squareLine 工程使能 多语言 选项后，导出代码会在 `ui.h` 里面会带 `#include "lv_i18n.h"`，按需来。
  
      squareLine 的控件里的文本选择了  `To be translated` 选项，导出程序后会有多出的 `_` 字符在字符串前，是 lv_i18n 检查的标记，按需来。
  
    - 所有 label 的 长宽，对于数字 宽度要够，对于多语言的各语言的文本则长宽要够，或者设置为 换行、省略号 或 滚动 等显示方式。
  
      要考虑有的变化的文本的长度很长的情况，比如 一些 后端设置的 title 如 wifi 名字 等，可以设置固定宽度 然后设置 滚动循环显示，以此类推。
  
  - 所有控件的命名是否合规。
  
  - 所有 页面内的 btn 均有 call function；其它 行为 和 event 检查。
  
  - 多个 screen 重复出现的可以做成组件。
  
  - 有的 component 的顶层 obj 会默认带了 不应该带的 x、y 的设置（不为 0），可以在 component 文件夹里面搜索 lv_obj_set_x 和 lv_obj_set_y 来找出所有应该设置为 0 却没有的，并且要设置对齐为 CENTER，在 squareLine 里面 编辑组件 更正一遍。
  
- 根据 “关于 crash (Segmentation fault) 的跟踪” 一节里面的总结进行检查，保证执行顺序，多线程间调用 lv_xxx() 的 API  加 互斥锁 或 保证都在一个线程里面。



添彩的地方：这些基本功能，可各个写个类来封装，方便调用。

- 点击 panel 放大展开的 动画，目前 squareLine 设置 动画 必须按照初始值，也就是 每个不同位置的 obj 必须单独做 动画。但是渐显渐隐 的动画 比较好做。优化 ui 可以设置一些动画。可以看看 LVGL Demos [Demos — LVGL](https://lvgl.io/demos) 找找感觉，由专业交互设计人员进行设计。

- 多种 Themes，squareLine 1.4.0 版本之后 可以每个 控件 选择 颜色 的 时候可以添加给 某个 theme；

  可以至少提供 light 和 dark 这 亮暗 两种风格；可以想想增加灵活度，增加多种预设，增加背景图片选择等，丰富选择，让每个用户屏幕都不一样更有个性。

  可后端去做，遍历所有 obj 来添加，写起来估计也不好写，看后面需求吧。

- 放一些 gif 提示图之类的。

- 放一些 label 渐隐渐显（lv_obj_fade_xx()）、变色（需要自写） 等的强提示。也可以用于，页面 打开 和 关闭 时候 各种界面元素 的 出现 和 消失 的动画；squareLine 官方例子里面很多。

- 更多请参考 专业的 UI 设计教程。



### SquareLine Component 使用

**squareLine 工程间复用**

具有共性、可复用的组件、功能块，在 squareLine 中做成 component，会在 squareLine 工程的 components 文件夹下 生成 .ecomp 后缀名的文件，这个文件可以复制到不同 squareLine 工程的 components 文件夹中 进行复用。



**SquareLine Component c 端调用**

squareLine 生成 ui 代码后，每个 component 会在 ui/components 文件夹下生成 组件的 .c 文件，在 c 端进行调用、复用。

这里例子在 timer 500ms 周期 回调中 执行 创建、删除 和 隐藏、显示，来做到 这个 组件 component 在 UI 界面上的 弹出显示 和 关闭消失。这里是直接在 lv_scr_act()（获取 当前页面 lv_obj_t*） 下面创建的。

```c
lv_obj_t * kb;
lv_obj_t * switchXXX;

void my_timer(lv_timer_t * timer)
{
    static bool flap = false;
    flap = !flap;
    if(flap) {
        switchXXX = ui_XXX_create(lv_scr_act()); // 创建 component
        lv_obj_add_flag(kb, LV_OBJ_FLAG_HIDDEN);
    } else {
        lv_obj_del(switchXXX); // 删除 component
        lv_obj_clear_flag(kb, LV_OBJ_FLAG_HIDDEN);
    }
}

void ui_init(void)
{
    ...
    kb = ui_XXX_create(lv_scr_act());
    lv_timer_t * timer = lv_timer_create(my_timer, 500,  NULL);
    ...
}
```



**往 listView 里面添加 component**

若一个 panel 设置了 flex 排序 和 有 scroll，那么往这个 obj 给 create obj，新建的 obj 会自动排列，这样可以实现个 listView，动态增减其中的项。



**获取 component 的 子 obj**

若 组件 中有 label、图片 等，可以通过 其 顶层 obj 寻找 其 子对象 obj 来对其设置。

在 component 的 .h 文件里面留出了 init() 函数 和 其各 子 obj 的 index 宏定义，通过 定义在 `ui_hook.h` 的 `lv_obj_t * ui_comp_get_child(lv_obj_t * comp, uint32_t child_idx)` 来获取其子 obj，由此控制子 obj（设置 str、设置图片、添加 btn cb 等等）。所有组件的 .h 被 include 在 `ui_hook.h` 里面，而这个又被 include 在 `ui.h` 里面，所以 暴露/包含 `ui.h` 就包含了所有。例子如下：

```c
lv_obj_t* temp;
lv_obj_t* ui_temppppp;

void my_timer(lv_timer_t * timer)
{
    static bool flap = false;
    int32_t ret = -1;
    flap = !flap;
    if(flap) {
        lv_label_set_text(temp, "const char *text");
    } else {
        lv_label_set_text(temp, "dddd");
    }
}

void ui_init(void)
{
    ...
    // 创建个 comp
    ui_temppppp = ui_XXXIconPanel_create(ui_XXXInstListPanel);
    // 获取其某个子 obj，是个 label，然后在 my_timer() 里面周期性更改其 text
    temp = ui_comp_get_child(ui_temppppp, UI_COMP_XXXICONPANEL_XXXINFOPANEL_XXXSTR);
    lv_timer_t * timer = lv_timer_create(my_timer, 500,  NULL);
    ...
}
```



**约定俗成**

见上面 `SquareLine 规范 & 经验 相关` 里面的说明。



## API 备查



注意本文主要成型于 LVGL V8 时期，有些 API 和最新版有出入，参考 源码 [lvgl/src at master · lvgl/lvgl](https://github.com/lvgl/lvgl/tree/master/src) 中的 `lv_api_map_vX.X.h` 文件里面的定义查看新旧版本的 API。

有的功能可能被删除或者被取代为更好的了，所以要看自己使用版本对应的文档和源码。

以下，列出的源码为 LVGL V8 的，但是一些给出的链接为最新官网文档了。



### 大小端切换

lv_conf.h 里面

```c
/*For big endian systems set to 1*/
#define LV_BIG_ENDIAN_SYSTEM 0
```



小端高字节在高地址，大端低字节在高地址。



各常见处理器结构的大小端：

> - **ARMv7-A**: In ARMv7-A, the mapping of instruction memory is always little-endian.
>
> - ARMv7-R: SCTLR.IE, bit[31], that indicates the instruction endianness configuration.
> - **ARMv7-M**: Armv7-M supports a selectable endian model in which, on a reset, a control input determines whether the endianness is big endian (BE) or little endian (LE). This endian mapping has the following restrictions: The endianness setting only applies to data accesses. Instruction fetches are always little endian. All accesses to the SCS are little endian, see System Control Space (SCS) on page B3-595.
> - ARMv8-aarch32: aarch32: When using AArch32, having the CPSR.E bit have a different value to the equivalent System Control register EE bit when in EL1, EL2, or EL3 is now deprecated
> - **ARMv8-aarch64**: aarch64: This data endianness is controlled independently for each Execution level. For EL3, EL2 and EL1, the relevant register of SCTLR_ELn.



### obj 相关 API

#### lv_obj.h

创建 obj、状态设置 等等 杂项

- lv_init，lv_deinit，lv_is_initialized

- lv_obj_create

- lv_obj_add_flag，lv_obj_clear_flag，lv_obj_has_flag，lv_obj_has_flag_any，下面是所有 flag

  ```c
  LV_OBJ_FLAG_HIDDEN          = (1L << 0),  /**< Make the object hidden. (Like it wasn't there at all)*/
  LV_OBJ_FLAG_CLICKABLE       = (1L << 1),  /**< Make the object clickable by the input devices*/
  LV_OBJ_FLAG_CLICK_FOCUSABLE = (1L << 2),  /**< Add focused state to the object when clicked*/
  LV_OBJ_FLAG_CHECKABLE       = (1L << 3),  /**< Toggle checked state when the object is clicked*/
  LV_OBJ_FLAG_SCROLLABLE      = (1L << 4),  /**< Make the object scrollable*/
  LV_OBJ_FLAG_SCROLL_ELASTIC  = (1L << 5),  /**< Allow scrolling inside but with slower speed*/
  LV_OBJ_FLAG_SCROLL_MOMENTUM = (1L << 6),  /**< Make the object scroll further when "thrown"*/
  LV_OBJ_FLAG_SCROLL_ONE      = (1L << 7),  /**< Allow scrolling only one snappable children*/
  LV_OBJ_FLAG_SCROLL_CHAIN_HOR = (1L << 8), /**< Allow propagating the horizontal scroll to a parent*/
  LV_OBJ_FLAG_SCROLL_CHAIN_VER = (1L << 9), /**< Allow propagating the vertical scroll to a parent*/
  LV_OBJ_FLAG_SCROLL_CHAIN     = (LV_OBJ_FLAG_SCROLL_CHAIN_HOR | LV_OBJ_FLAG_SCROLL_CHAIN_VER),
  LV_OBJ_FLAG_SCROLL_ON_FOCUS = (1L << 10), /**< Automatically scroll object to make it visible when focused*/
  LV_OBJ_FLAG_SCROLL_WITH_ARROW  = (1L << 11), /**< Allow scrolling the focused object with arrow keys*/
  LV_OBJ_FLAG_SNAPPABLE       = (1L << 12), /**< If scroll snap is enabled on the parent it can snap to this object*/
  LV_OBJ_FLAG_PRESS_LOCK      = (1L << 13), /**< Keep the object pressed even if the press slid from the object*/
  LV_OBJ_FLAG_EVENT_BUBBLE    = (1L << 14), /**< Propagate the events to the parent too*/
  LV_OBJ_FLAG_GESTURE_BUBBLE  = (1L << 15), /**< Propagate the gestures to the parent*/
  LV_OBJ_FLAG_ADV_HITTEST     = (1L << 16), /**< Allow performing more accurate hit (click) test. E.g. consider rounded corners.*/
  LV_OBJ_FLAG_IGNORE_LAYOUT   = (1L << 17), /**< Make the object position-able by the layouts*/
  LV_OBJ_FLAG_FLOATING        = (1L << 18), /**< Do not scroll the object when the parent scrolls and ignore layout*/
  LV_OBJ_FLAG_OVERFLOW_VISIBLE = (1L << 19), /**< Do not clip the children's content to the parent's boundary*/
  
  LV_OBJ_FLAG_LAYOUT_1        = (1L << 23), /**< Custom flag, free to use by layouts*/
  LV_OBJ_FLAG_LAYOUT_2        = (1L << 24), /**< Custom flag, free to use by layouts*/
  
  LV_OBJ_FLAG_WIDGET_1        = (1L << 25), /**< Custom flag, free to use by widget*/
  LV_OBJ_FLAG_WIDGET_2        = (1L << 26), /**< Custom flag, free to use by widget*/
  LV_OBJ_FLAG_USER_1          = (1L << 27), /**< Custom flag, free to use by user*/
  LV_OBJ_FLAG_USER_2          = (1L << 28), /**< Custom flag, free to use by user*/
  LV_OBJ_FLAG_USER_3          = (1L << 29), /**< Custom flag, free to use by user*/
  LV_OBJ_FLAG_USER_4          = (1L << 30), /**< Custom flag, free to use by user*/
  ```

- lv_obj_add_state，lv_obj_clear_state，lv_obj_get_state，lv_obj_has_state，下面是所有 state

  ```c
  LV_STATE_DEFAULT     =  0x0000,
  LV_STATE_CHECKED     =  0x0001,
  LV_STATE_FOCUSED     =  0x0002,
  LV_STATE_FOCUS_KEY   =  0x0004,
  LV_STATE_EDITED      =  0x0008,
  LV_STATE_HOVERED     =  0x0010,
  LV_STATE_PRESSED     =  0x0020,
  LV_STATE_SCROLLED    =  0x0040,
  LV_STATE_DISABLED    =  0x0080,
  
  LV_STATE_USER_1      =  0x1000,
  LV_STATE_USER_2      =  0x2000,
  LV_STATE_USER_3      =  0x4000,
  LV_STATE_USER_4      =  0x8000,
  ```

- lv_obj_get_group

- 其它不常用杂项



#### lv_obj_tree.h

- lv_obj_del，删除 obj 本身
- lv_obj_clean，清除 obj 所有子对象
- lv_obj_del_delayed，延后指定毫秒后内部调用删除 obj
- lv_obj_del_async，使用 lv_async_call 删除 obj，lv_async_call 注册的回调函数将在 下次 lv_timer_handler 被调用的时候执行
- lv_obj_set_parent，lv_obj_get_parent
- lv_obj_get_child，lv_obj_get_child_cnt，lv_obj_get_index - get 孩子 obj 的 index，lv_obj_tree_walk - 遍历所有孩子 obj（提供回调函数）
- lv_obj_swap，两个 obj 交换位置
- lv_obj_move_to_index，moves the object to the given index in its parent. When used in listboxes, it can be used to sort the listbox items.
- lv_obj_get_screen
- lv_obj_get_disp



#### lv_obj_scrool.h

- 很多 api，滚动相关的。
- 是否启用滚动
- 滚动模式
- 滚动方向
- snap 对齐点
- 滚动到某个位置 x、y（是否带过渡动画）
- 滚动到某个 obj。见下面 `listView 的 snap 和 上下翻页` 一节里面
- 当前所在位置 等等。



#### lv_obj_pos.h

- 读写 obj 的 x、y

  经测试， squareLine 生成代码中设置长宽均通过 lv_obj_set_style_xxx()，所以**读取长宽也得通过 lv_obj_get_style_xxx() 函数**，用 lv_obj_get_height() 这种只会返回 0。。

- 长宽 size

- lv_obj_set_align，设置对其，相对位置设置

- lv_obj_align，lv_obj_align_to，lv_obj_center

- lv_obj_set_ext_click_area，扩展这个 obj 的 可点击范围

- lv_obj_hit_test，返回一个给定坐标是否有 obj



lv_obj_style.h，lv_obj_style_gen.h

-  style 相关，很多 api，建议在 suqareLine 里面可视化操作 进行 塑形



### style

官方参考手册

- style [Styles - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/styles/index.html)。
- style property [Style Properties - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/styles/style-properties.html)。



#### style APIs（以渐变色举例）

基础 style 的创建：lv_style.h

```c
/**
 * Initialize a style
 * @param style pointer to a style to initialize
 * @note Do not call `lv_style_init` on styles that already have some properties
 *       because this function won't free the used memory, just sets a default state for the style.
 *       In other words be sure to initialize styles only once!
 */
void lv_style_init(lv_style_t * style);

/**
 * Clear all properties from a style and free all allocated memories.
 * @param style pointer to a style
 */
void lv_style_reset(lv_style_t * style);
```



配置 style 细节的各种 APIs：lv_style_gen.h

为 `lv_style_xxx()` 系列 API，用于构造一个通用 style，然后可以给任意 obj 设置上，可以做到 通用设置 style，比如 用于 切换主题。

并以渐变色举例

```c
// 即各种 针对 某个 style 细节的 set()
lv_style_set_xxx()

/* ------------------------------- */

// 渐变色设置 stop 的数量由 lv_conf.h 下面的宏定
/*Number of stops allowed per gradient. Increase this to allow more stops.
 *This adds (sizeof(lv_color_t) + 1) bytes per additional stop*/
#define LV_GRADIENT_MAX_STOPS 4

// 官方参考实例，设置 背景色 渐变色，https://docs.lvgl.io/master/common-widget-features/styles/style-properties.html#background
// 下面根据这个例子修改

static lv_style_t style; // 建个 style
lv_style_init(&style);   // 初始化，里面会给 内部 property 申请一些内存，然后下面就是各种细节调节设置 set()

// 渐变色中 两个 stop 的位置
// 0~255，对应 从最左到最右
uint8_t stop0 = 150;
uint8_t stop1 = 180;

/*Make a gradient*/
static lv_grad_dsc_t grad;
grad.dither = LV_DITHER_NONE;
grad.dir = LV_GRAD_DIR_HOR;
grad.stops_count = 2;
grad.stops[0].color = lv_palette_main(LV_PALETTE_RED);
grad.stops[0].frac  = stop0; // 0~255，对应 从最左到最右
grad.stops[1].color = lv_palette_main(LV_PALETTE_BLUE);
grad.stops[1].frac  = stop1;

lv_style_set_bg_grad(&style, &grad);
lv_style_set_bg_opa(&style, LV_OPA_COVER);

lv_obj_add_style(ui_bgPanel, &style, LV_PART_MAIN | LV_STATE_DEFAULT);

// 读出 parent obj 的宽高
// 经测试， squareLine 生成代码中设置长宽均通过 lv_obj_set_style_xxx()，
// 所以读取长宽也得通过 lv_obj_get_style_xxx() 函数，用 lv_obj_get_height() 这种只会返回 0。。
lv_coord_t parent_h = lv_obj_get_style_height(ui_bgPanel, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_coord_t parent_w = lv_obj_get_style_width(ui_bgPanel, LV_PART_MAIN | LV_STATE_DEFAULT);
LV_LOG_USER("style h: %d", parent_h);
LV_LOG_USER("style w: %d", parent_w);

// 在 stop0 的位置画个竖线，标注渐变开始的地方
lv_obj_t* verLine0 = lv_obj_create(ui_bgPanel);
lv_obj_set_width(verLine0, 1);
lv_obj_set_height(verLine0, 200);
lv_obj_set_align(verLine0, LV_ALIGN_TOP_LEFT);
lv_obj_set_x(verLine0, (uint32_t)(((double)stop0 / (double)255) * (double)parent_w));
lv_obj_set_style_bg_color(verLine0, lv_color_hex(0x000000), LV_PART_MAIN | LV_STATE_DEFAULT); // 设颜色
lv_obj_set_style_border_width(verLine0, 0, LV_PART_MAIN | LV_STATE_DEFAULT); // 去掉 border

// 在 stop1 的位置画个竖线，标注渐变停止的地方
lv_obj_t* verLine1 = lv_obj_create(ui_bgPanel);
lv_obj_set_width(verLine1, 1);
lv_obj_set_height(verLine1, 200);
lv_obj_set_align(verLine1, LV_ALIGN_TOP_LEFT);
lv_obj_set_x(verLine1, (uint32_t)(((double)stop1 / (double)255) * (double)parent_w));
lv_obj_set_style_bg_color(verLine1, lv_color_hex(0x000000), LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_border_width(verLine1, 0, LV_PART_MAIN | LV_STATE_DEFAULT);
```



#### obj style APIs

给 具体的 控件 obj 增减 style 等的基础 APIs：lv_obj_style.h

```c
/**
 * Add a style to an object.
 * @param obj       pointer to an object
 * @param style     pointer to a style to add
 * @param selector  OR-ed value of parts and state to which the style should be added
 * @example         lv_obj_add_style(btn, &style_btn, 0); //Default button style
 * @example         lv_obj_add_style(btn, &btn_red, LV_STATE_PRESSED); //Overwrite only some colors to red when pressed
 */
void lv_obj_add_style(struct _lv_obj_t * obj, lv_style_t * style, lv_style_selector_t selector);

/**
 * Add a style to an object.
 * @param obj       pointer to an object
 * @param style     pointer to a style to remove. Can be NULL to check only the selector
 * @param selector  OR-ed values of states and a part to remove only styles with matching selectors. LV_STATE_ANY and LV_PART_ANY can be used
 * @example lv_obj_remove_style(obj, &style, LV_PART_ANY | LV_STATE_ANY); //Remove a specific style
 * @example lv_obj_remove_style(obj, NULL, LV_PART_MAIN | LV_STATE_ANY); //Remove all styles from the main part
 * @example lv_obj_remove_style(obj, NULL, LV_PART_ANY | LV_STATE_ANY); //Remove all styles
 */
void lv_obj_remove_style(struct _lv_obj_t * obj, lv_style_t * style, lv_style_selector_t selector);

/**
 * Remove all styles from an object
 * @param obj       pointer to an object
 */
static inline void lv_obj_remove_style_all(struct _lv_obj_t * obj);



/**
 * Notify all object if a style is modified
 * @param style     pointer to a style. Only the objects with this style will be notified
 *                  (NULL to notify all objects)
 */
void lv_obj_report_style_change(lv_style_t * style);

/**
 * Notify an object and its children about its style is modified.
 * @param obj       pointer to an object
 * @param part      the part whose style was changed. E.g. `LV_PART_ANY`, `LV_PART_MAIN`
 * @param prop      `LV_STYLE_PROP_ANY` or an `LV_STYLE_...` property.
 *                  It is used to optimize what needs to be refreshed.
 *                  `LV_STYLE_PROP_INV` to perform only a style cache update
 */
void lv_obj_refresh_style(struct _lv_obj_t * obj, lv_part_t part, lv_style_prop_t prop);

/**
 * Enable or disable automatic style refreshing when a new style is added/removed to/from an object
 * or any other style change happens.
 * @param en        true: enable refreshing; false: disable refreshing
 */
void lv_obj_enable_style_refresh(bool en);
```



直接给 obj 设置 style 细节的 APIs：lv_obj_style_gen.h

为 `lv_obj_set_style_xxx()` 系列 API，直接设置 obj 的 某个 style。

```c
// 即各种 针对 具体 obj 的 某个 style 细节的 get() 和 set()
lv_obj_get_style_xxx()
lv_obj_set_style_xxx()

// 如设置 背景色
// 其中 selector 为选择 part 和 state 的 或，来对不同 part 在不同 state 的变化 进行配置
void lv_obj_set_style_bg_color(struct _lv_obj_t * obj, lv_color_t value, lv_style_selector_t selector);
// 实例
lv_obj_set_style_bg_color(ui_bgPanel, lv_color_hex(0x2F302F), LV_PART_MAIN | LV_STATE_DEFAULT);

// 设置渐变色，就可以直接写成如下
uint8_t stop0 = 150;
uint8_t stop1 = 180;

static lv_grad_dsc_t grad;
grad.dither = LV_DITHER_NONE;
grad.dir = LV_GRAD_DIR_HOR;
grad.stops_count = 2;
grad.stops[0].color = lv_palette_main(LV_PALETTE_RED);
grad.stops[0].frac  = stop0; // 0~255，对应 从最左到最右
grad.stops[1].color = lv_palette_main(LV_PALETTE_BLUE);
grad.stops[1].frac  = stop1;

lv_obj_set_style_bg_grad(ui_bgPanel, &grad, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_bg_opa(ui_bgPanel, LV_OPA_COVER, LV_PART_MAIN | LV_STATE_DEFAULT); // 可以不带

// 注意，设置 grad 之后要再设置其它颜色，或者设置新的 grad，要先 取消旧的 grad 效果，先调如下一句，再设新的
// disable all grad style first!! or the old grad style will last exist
lv_obj_set_style_bg_grad(_obj, nullptr, _selector);
```



#### min / max height / width



设置一个 obj 或者 label 的 最大宽度 或者 高度，如：

```c
lv_obj_set_style_min_width(ui_Label257, 0, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_max_width(ui_Label257, 300, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_min_height(ui_Label257, 0, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_max_height(ui_Label257, 200, LV_PART_MAIN | LV_STATE_DEFAULT);
```



对于 label，设置宽度为 随着 content 变化，再设置最大宽度，设置 滚动的方式，则可以实现，一个 label 宽度小于最大宽度的时候，其宽度随着 文本内容变化，超过最大宽度则开始滚动。



还可以：

设置一个 label 长文本，发现会截断，所以用下面的，设置加长！！！

```c
// the default obj max height of lvgl is 8191(by using "lv_obj_get_style_max_height()" discover this)...
// in "LV_USE_LARGE_COORD" is 0 in "lv_conf.h"
// so here expand it!!! set "LV_USE_LARGE_COORD" to 1
lv_obj_set_style_max_height(ui_TermsPageMainTextStr, 66666, 0);
```



#### fade in / out

参考 lvgl 提供的 API `lv_obj_fade_in()` 和 `lv_obj_fade_out()`，其内部本质是创建 lv_anim 并在周期回调里面改变 obj 的 opa。

```c
/**
 * Fade in an an object and all its children.
 * @param obj       the object to fade in
 * @param time      time of fade
 * @param delay     delay to start the animation
 */
void lv_obj_fade_in(struct _lv_obj_t * obj, uint32_t time, uint32_t delay);

/**
 * Fade out an an object and all its children.
 * @param obj       the object to fade out
 * @param time      time of fade
 * @param delay     delay to start the animation
 */
void lv_obj_fade_out(struct _lv_obj_t * obj, uint32_t time, uint32_t delay);
```



#### transform

为 `lv_style_set_transform_xxx()` 系列 API，可以针对 一个 obj （其可以包含多个 子 obj）设置 旋转、缩放 等等。例如：

```c
lv_obj_style_set_transform_width();
lv_obj_style_set_transform_height();

lv_obj_set_style_transform_angle(ui_Label257, 900, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_transform_zoom(ui_Label257, 500, LV_PART_MAIN | LV_STATE_DEFAULT);

lv_obj_set_style_transform_pivot_x(ui_Label257, 5, LV_PART_MAIN | LV_STATE_DEFAULT);
lv_obj_set_style_transform_pivot_y(ui_Label257, 5, LV_PART_MAIN | LV_STATE_DEFAULT);
```



### 富文本 lv_span

参考 官方手册 和 例子 

[Spangroup (lv_spangroup) - LVGL documentation](https://docs.lvgl.io/master/widgets/spangroup.html)。

[Span example - LVGL documentation](https://docs.lvgl.io/master/examples.html#span)。

这个好处是，可以在一段连续的文本中，设置 一段一段文本各不相同的 style（如颜色、字体（大小）、下划线 等）。

lv_span.h

```c
// 创删 spangroup obj(包含多个 span，每一个是一个设置独立效果的 text) 相关 APIs
// 在 spangroup 下创建各个 span 相关 APIs
/**
 * Create a spangroup object
 * @param par pointer to an object, it will be the parent of the new spangroup
 * @return pointer to the created spangroup
 */
lv_obj_t * lv_spangroup_create(lv_obj_t * par);

/**
 * Create a span string descriptor and add to spangroup.
 * @param obj pointer to a spangroup object.
 * @return pointer to the created span.
 */
lv_span_t * lv_spangroup_new_span(lv_obj_t * obj);

/**
 * Remove the span from the spangroup and free memory.
 * @param obj pointer to a spangroup object.
 * @param span pointer to a span.
 */
void lv_spangroup_del_span(lv_obj_t * obj, lv_span_t * span);
```



```c
// 获取 child(spangroup 下的各个 span) 相关 APIs
/**
 * Get a spangroup child by its index.
 *
 * @param obj   The spangroup object
 * @param id    the index of the child.
 *              0: the oldest (firstly created) child
 *              1: the second oldest
 *              child count-1: the youngest
 *              -1: the youngest
 *              -2: the second youngest
 * @return      The child span at index `id`, or NULL if the ID does not exist
 */
lv_span_t * lv_spangroup_get_child(const lv_obj_t * obj, int32_t id);

/**
 *
 * @param obj   The spangroup object to get the child count of.
 * @return      The span count of the spangroup.
 */
uint32_t lv_spangroup_get_child_cnt(const lv_obj_t * obj);
```



```c
// 设置 spangroup
/**
 * Set the align of the spangroup.
 * @param obj pointer to a spangroup object.
 * @param align see lv_text_align_t for details.
 */
void lv_spangroup_set_align(lv_obj_t * obj, lv_text_align_t align);

/**
 * Set the overflow of the spangroup.
 * @param obj pointer to a spangroup object.
 * @param overflow see lv_span_overflow_t for details.
 */
void lv_spangroup_set_overflow(lv_obj_t * obj, lv_span_overflow_t overflow);

/**
 * Set the indent of the spangroup.
 * @param obj pointer to a spangroup object.
 * @param indent The first line indentation
 */
void lv_spangroup_set_indent(lv_obj_t * obj, lv_coord_t indent);

/**
 * Set the mode of the spangroup.
 * @param obj pointer to a spangroup object.
 * @param mode see lv_span_mode_t for details.
 */
void lv_spangroup_set_mode(lv_obj_t * obj, lv_span_mode_t mode);

/**
 * Set lines of the spangroup.
 * @param obj pointer to a spangroup object.
 * @param lines max lines that can be displayed in LV_SPAN_MODE_BREAK mode. < 0 means no limit.
 */
void lv_spangroup_set_lines(lv_obj_t * obj, int32_t lines);
```



```c
// 刷新 API
// If spangroup object mode != LV_SPAN_MODE_FIXED you must call lv_spangroup_refr_mode() after you have modified span style(eg:set text, changed the font size, del span).
/**
 * update the mode of the spangroup.
 * @param obj pointer to a spangroup object.
 */
void lv_spangroup_refr_mode(lv_obj_t * obj);
```



```c
// 设置其中每一个 span 的 text 并独立设置 style
// 看官方 example 即可

// 例子
lv_span_t * span = lv_spangroup_new_span(spans);
lv_span_set_text(span, "China is a beautiful country.");
lv_style_set_text_color(&span->style, lv_palette_main(LV_PALETTE_RED));
lv_style_set_text_decor(&span->style, LV_TEXT_DECOR_UNDERLINE);
lv_style_set_text_opa(&span->style, LV_OPA_50);
```



### 文件操作 lv_fs

[File System (lv_fs_drv) - LVGL documentation](https://docs.lvgl.io/master/main-modules/fs.html).

先在 `lv_conf.h` 里面选择一个 IO 底层接口，这里选择 `LV_USE_FS_STDIO`，且 设置 这个接口的标识符为 `L`，所以所有填入 lv_fs_open() 等 API 的 文件路径的开头必须加上 `L:`，例如：`L:C:/Users/.../XXXPic.png`。



```c
/*File system interfaces for common APIs */

/*API for fopen, fread, etc*/
#define LV_USE_FS_STDIO 1
#if LV_USE_FS_STDIO
    #define LV_FS_STDIO_LETTER 'L'     /*Set an upper cased letter on which the drive will accessible (e.g. 'A')*/
    #define LV_FS_STDIO_PATH ""         /*Set the working directory. File/directory paths will be appended to it.*/
    #define LV_FS_STDIO_CACHE_SIZE 0    /*>0 to cache this number of bytes in lv_fs_read()*/
#endif
```



APIs：

- lv_fs_get_letters
- lv_fs_get_ext，返回文件扩展名
- lv_fs_open
- lv_fs_close
- lv_fs_read
- lv_fs_write
- lv_fs_seek，当前文件读写指针移动到 指定位置，或移动到文件末尾
- lv_fs_tell，返回当前 文件读写指针 位置
- lv_fs_dir_open
- lv_fs_dir_read
- lv_fs_dir_close



例子：

```c
// 下面的 file_path 是 win 上的 路径，linux 上的类似，如 "L:/Users/.../XXXPic.png"
// use lv_fs_open, fila path have a prefix like "L:" see "LV_FS_STDIO_LETTER" in lv_conf.h
#define file_path "L:C:/Users/.../gCodePic.png"

const std::string imgFilePath = file_path;

lv_fs_file_t file_ptr;
lv_fs_res_t res = lv_fs_open(&file_ptr, imgFilePath.c_str(), LV_FS_MODE_RD);
if(LV_FS_RES_OK != res) {
    LV_LOG_ERROR("lv_fs_open err");
    return -ENOENT;
}

// get file size
uint32_t file_size = 0;
res = lv_fs_seek(&file_ptr, 0, LV_FS_SEEK_END);
if(LV_FS_RES_OK != res) {
    LV_LOG_ERROR("lv_fs_seek err");
    lv_fs_close(&file_ptr);
    return -EPERM;
}
res = lv_fs_tell(&file_ptr, &file_size);
if(LV_FS_RES_OK != res) {
    LV_LOG_ERROR("lv_fs_tell err");
    lv_fs_close(&file_ptr);
    return -EPERM;
}

// read all file content into "lv_img_dsc.data"
res = lv_fs_seek(&file_ptr, 0, LV_FS_SEEK_SET);
if(LV_FS_RES_OK != res) {
    LV_LOG_ERROR("lv_fs_seek 2 err");
    lv_mem_free((void*)lv_img_dsc.data);
    lv_fs_close(&file_ptr);
    return -EPERM;
}
uint32_t file_br = 0;
res = lv_fs_read(&file_ptr, (void*)lv_img_dsc.data, file_size, &file_br);
if((LV_FS_RES_OK != res) || (file_br != file_size)) {
    LV_LOG_ERROR("lv_fs_read err");
    lv_mem_free((void*)lv_img_dsc.data);
    lv_fs_close(&file_ptr);
    return -EIO;
}

lv_fs_close(&file_ptr);
```



### 二维码 lv_qrcode

[QR Code - LVGL documentation](https://docs.lvgl.io/master/libs/qrcode.html).

lv_qrcode.h 里面

```c
/**
 * Create an empty QR code (an `lv_canvas`) object.
 * @param parent point to an object where to create the QR code
 * @param size width and height of the QR code
 * @param dark_color dark color of the QR code
 * @param light_color light color of the QR code
 * @return pointer to the created QR code object
 */
lv_obj_t * lv_qrcode_create(lv_obj_t * parent, lv_coord_t size, lv_color_t dark_color, lv_color_t light_color);

/**
 * Set the data of a QR code object
 * @param qrcode pointer to aQ code object
 * @param data data to display
 * @param data_len length of data in bytes
 * @return LV_RES_OK: if no error; LV_RES_INV: on error
 */
lv_res_t lv_qrcode_update(lv_obj_t * qrcode, const void * data, uint32_t data_len);

/**
 * DEPRECATED: Use normal lv_obj_del instead
 * Delete a QR code object
 * @param qrcode pointer to a QR code object
 */
void lv_qrcode_delete(lv_obj_t * qrcode);
```

这几个 API 是 lvgl 对 qrcodegen.c / .h 的封装。



例子：

```c
const char qrStr[] = "www.baidu.com";

lv_color_t bg_color = lv_palette_lighten(LV_PALETTE_LIGHT_BLUE, 5); // 二维码背景色
lv_color_t fg_color = lv_palette_darken(LV_PALETTE_BLUE, 4);        // 二维码前景色

lv_obj_t *qr = lv_qrcode_create(ui_bgPanel, 200, fg_color, bg_color); // 200 为 正方形二维码 边长像素
if(!qr) {
    LV_LOG_ERROR("lv_qrcode_create err");
    return -1;
}
lv_res_t res = lv_qrcode_update(qr, qrStr, sizeof(qrStr)); // 每次更改 二维码 内容 qrStr，必须再调用这个刷新
if(LV_RES_OK != res) {
    LV_LOG_ERROR("lv_qrcode_update err");
    return -1;
}

lv_qrcode_delete(qr); // 删除 & 释放 二维码 obj
```



### 颜色 lv_colors

官方参考手册 [Color (lv_color) - LVGL documentation](https://docs.lvgl.io/master/main-modules/color.html)。

RBG 直接合成（Red, Green and Blue）

```c
/*All channels are 0-255*/
lv_color_t c = lv_color_make(red, green, blue);

/*Same but can be used for const initialization too */
lv_color_t c = LV_COLOR_MAKE(red, green, blue);

/*From hex code 0x000000..0xFFFFFF interpreted as RED + GREEN + BLUE*/
lv_color_t c = lv_color_hex(0x123456);
```



RBG 颜色 变亮或变暗调节，混合颜色

```c
// Lighten a color.
// 0: no change
// 255: white
lv_color_t lv_color_lighten(lv_color_t c, lv_opa_t lvl);

// Darken a color.
// 0: no change
// 255: black
lv_color_t lv_color_darken(lv_color_t c, lv_opa_t lvl);

// Lighten or darken a color. 
// 0: black
// 128: no change
// 255: white
lv_color_t lv_color_change_lightness(lv_color_t c, lv_opa_t lvl);

// Mix two colors with a given ratio
// 0: full c2
// 255: full c1
// 128: half c1 and half c2
lv_color_t lv_color_mix(lv_color_t c1, lv_color_t c2, uint8_t mix);

// typedef uint8_t lv_opa_t;
// lv_opa_t 可填入 0~255，或者下面的枚举项
/*
    LV_OPA_TRANSP = 0,
    LV_OPA_0      = 0,
    LV_OPA_10     = 25,
    LV_OPA_20     = 51,
    LV_OPA_30     = 76,
    LV_OPA_40     = 102,
    LV_OPA_50     = 127,
    LV_OPA_60     = 153,
    LV_OPA_70     = 178,
    LV_OPA_80     = 204,
    LV_OPA_90     = 229,
    LV_OPA_100    = 255,
    LV_OPA_COVER  = 255,
*/
```



HSV 直接合成（Hue, Saturation and Value）

```c
//h = 0..359, s = 0..100, v = 0..100
lv_color_t c = lv_color_hsv_to_rgb(h, s, v);

//All channels are 0-255
lv_color_hsv_t c_hsv = lv_color_rgb_to_hsv(r, g, b);


//From lv_color_t variable
lv_color_hsv_t c_hsv = lv_color_to_hsv(color);
```



Palette 调色板调成

```c
// 直接从基础色获得
lv_color_t lv_palette_main(lv_palette_t p);
/* enum lv_palette_t 可选的：
    LV_PALETTE_RED,
    LV_PALETTE_PINK,
    LV_PALETTE_PURPLE,
    LV_PALETTE_DEEP_PURPLE,
    LV_PALETTE_INDIGO,
    LV_PALETTE_BLUE,
    LV_PALETTE_LIGHT_BLUE,
    LV_PALETTE_CYAN,
    LV_PALETTE_TEAL,
    LV_PALETTE_GREEN,
    LV_PALETTE_LIGHT_GREEN,
    LV_PALETTE_LIME,
    LV_PALETTE_YELLOW,
    LV_PALETTE_AMBER,
    LV_PALETTE_ORANGE,
    LV_PALETTE_DEEP_ORANGE,
    LV_PALETTE_BROWN,
    LV_PALETTE_BLUE_GREY,
    LV_PALETTE_GREY,
*/

// 从基础色 再加上 明暗 来调出
lv_color_t lv_palette_lighten(lv_palette_t p, uint8_t lvl); // lvl 只能为 1~5
lv_color_t lv_palette_darken(lv_palette_t p, uint8_t lvl);  // lvl 只能为 1~4

// 如：
lv_color_t bg_color = lv_palette_lighten(LV_PALETTE_LIGHT_BLUE, 5);
lv_color_t fg_color = lv_palette_darken(LV_PALETTE_BLUE, 4);
```



### 切换 Screen

参考 [Screens - LVGL documentation](https://docs.lvgl.io/master/common-widget-features/screens.html)。

lv_disp.h

- lv_scr_act()，获取当前 screen obj。

- lv_scr_load() 或 lv_disp_load_scr()，切换到指定 screen obj，即切页。

  填入新的 screen 的 obj（需要已经初始化过的）；默认无过渡动画，默认不删除 old 的 screen。

- lv_scr_load_anim()（前面两个 api 都是调用这个），可以指定切页动画的切页

  填入新的 screen 的 obj，选择切换动画，填入过渡时间、延时，是否删除当前 old 的 screen（在下次 timer handle 时候删除）



如果 UI 涉及 切页按键 有不固定的的切页逻辑，比如在不同的情况下同一个切页按键点击后会跳转到不同的页面，那么就需要针对性设计。



### listView 的 snap 和 上下翻页

```c
lv_obj_set_scroll_snap_y(ui_XXXInstListPanel, LV_SCROLL_SNAP_START);
lv_obj_update_snap(ui_XXXInstListPanel, LV_ANIM_ON);


void XXXPagingPanelUpBtn(lv_event_t * e)
{
	if(lv_obj_get_scroll_top(ui_XXXInstListPanel) > 0) {
		lv_obj_scroll_to_y(ui_XXXInstListPanel, 
			lv_obj_get_scroll_top(ui_XXXInstListPanel) - 200, 
			LV_ANIM_ON);
	}
}

void XXXPagingPanelDownBtn(lv_event_t * e)
{
	if(lv_obj_get_scroll_bottom(ui_XXXInstListPanel) > 0) {
		lv_obj_scroll_to_y(ui_XXXInstListPanel, 
			lv_obj_get_scroll_top(ui_XXXInstListPanel) + 200, 
			LV_ANIM_ON);
	}
}
```



### 添加事件 & 事件处理

给 某一个 obj 发送一个事件

```c
/**
 * Send an event to the object
 * @param obj           pointer to an object
 * @param event_code    the type of the event from `lv_event_t`
 * @param param         arbitrary data depending on the widget type and the event. (Usually `NULL`)
 * @return LV_RES_OK: `obj` was not deleted in the event; LV_RES_INV: `obj` was deleted in the event_code
 */
lv_res_t lv_event_send(struct _lv_obj_t * obj, lv_event_code_t event_code, void * param);
```



添加事件回调函数

```c
/**
 * Add an event handler function for an object.
 * Used by the user to react on event which happens with the object.
 * An object can have multiple event handler. They will be called in the same order as they were added.
 * @param obj       pointer to an object
 * @param filter    and event code (e.g. `LV_EVENT_CLICKED`) on which the event should be called. `LV_EVENT_ALL` can be sued the receive all the events.
 * @param event_cb  the new event function
 * @param           user_data custom data data will be available in `event_cb`
 * @return          a pointer the event descriptor. Can be used in ::lv_obj_remove_event_dsc
 */
struct _lv_event_dsc_t * lv_obj_add_event_cb(struct _lv_obj_t * obj, lv_event_cb_t event_cb, lv_event_code_t filter, void * user_data);

// e.g.
lv_obj_add_event_cb(btn, btn_event_cb, LV_EVENT_CLICKED, NULL); /*Assign a callback to the button*/
```



事件处理，典型如下，获取 event code 和 obj 再做逻辑

```c
static void event_handler(lv_event_t * e)
{
    lv_event_code_t eventCode = lv_event_get_code(e);
    lv_obj_t * obj = lv_event_get_target(e);
    void * user_data = lv_event_get_user_data(e);
    if(eventCode == LV_EVENT_CLICKED) {
        ...
    }
}
```



去除一个 obj 所有 event

```c
/**
 * Remove an event handler function for an object.
 * @param obj       pointer to an object
 * @param event_cb  the event function to remove, or `NULL` to remove the firstly added event callback
 * @return          true if any event handlers were removed
 */
bool lv_obj_remove_event_cb(struct _lv_obj_t * obj, lv_event_cb_t event_cb);

/**
 * Remove an event handler function with a specific user_data from an object.
 * @param obj               pointer to an object
 * @param event_cb          the event function to remove, or `NULL` only `user_data` matters.
 * @param event_user_data   the user_data specified in ::lv_obj_add_event_cb
 * @return                  true if any event handlers were removed
 */
bool lv_obj_remove_event_cb_with_user_data(struct _lv_obj_t * obj, lv_event_cb_t event_cb,
                                           const void * event_user_data);

```



一点东西，看源码， switch、checkbox 这两个控件在 struct 的  “构造函数” 里面 加上了 flag `LV_OBJ_FLAG_CHECKABLE`，然后看 lvgl src 源码里面 `lv_obj.c` 的 `lv_obj_event()`，有这个 flag 的 会 根据 checked 的 变化 发送  `LV_EVENT_VALUE_CHANGED`  event。



### 模拟点击



参考 `lv_monkey.c` 的实现。[Monkey - LVGL documentation](https://docs.lvgl.io/master/debugging/monkey.html)。



### 睡眠管理

参考 [Overview - LVGL documentation](https://docs.lvgl.io/master/integration/overview.html#sleep-management)。



一段时间不操作：

1. 首先进入屏保，屏幕全屏换成一个图片什么的。
2. 再一段时间不操作：降低屏幕亮度。
3. 再一段事件不操作：进入休眠序列



进入睡眠序列：

1. 关闭屏幕背光电源
2. 停掉 lvgl 事件处理 timer，参考上面链接里面
3. 关闭一些外设，只保留退出休眠的外设
4. 处理器进入低功耗模式



退出休眠序列，与上面的相反即可。



### 定时器

参考 [Timer (lv_timer) - LVGL documentation](https://docs.lvgl.io/master/main-modules/timer.html)。



```c
void my_timer(lv_timer_t * timer)
{
  /*Use the user_data*/
  uint32_t * user_data = timer->user_data;
  printf("my_timer called with user data: %d\n", *user_data);

  /*Do something with LVGL*/
  if(something_happened) {
    something_happened = false;
    lv_button_create(lv_screen_active(), NULL);
  }
}

...

static uint32_t user_data = 10;
lv_timer_t * timer = lv_timer_create(my_timer, 500,  &user_data);

...

lv_timer_del(timer);
```



> **Set parameters**
>
> You can modify some timer parameters later:
>
> - lv_timer_set_cb(timer, new_cb)
> - lv_timer_set_period(timer, new_period)
>
> **Repeat count**
>
> You can make a timer repeat only a given number of times with lv_timer_set_repeat_count(timer, count). The timer will automatically be deleted after it's called the defined number of times. Set the count to `-1` to repeat indefinitely.
>
> **Enable and Disable**
>
> You can enable or disable a timer with lv_timer_enable(en).
>
> **Pause and Resume**
>
> lv_timer_pause(timer) pauses the specified timer.
>
> lv_timer_resume(timer) resumes the specified timer.



### 截屏并保存为文件

[Snapshot - LVGL documentation](https://docs.lvgl.io/master/main-modules/draw/snapshot.html)。

基本实现

```c
lv_img_dsc_t* snapshot = lv_snapshot_take(lv_scr_act(), LV_IMG_CF_TRUE_COLOR_ALPHA);
// 将数据 snapshot->data 从LV 默认格式 RGBA 转为 ARGB，再进行下面的编码和保存
lodepng_encode32_file(filename, snapshot->data, snapshot->header.w, snapshot->header.h);
// 成功后释放内存
lv_snapshot_free(snapshot);
```



保存为 jpg 图片，需要个 jpg 编码库，很多，比如 使用 Github 开源的 tiny_jpeg.h。



### 杂项

#### lv_mem

```c
void * lv_mem_alloc(size_t size);
void lv_mem_free(void * data);
```



在 lv_conf.h 里面配置 lvgl 使用 标准库的 malloc/free 还是 内建指定大小数组作为 使用内存。



#### lvgl version

```c
// 在 lvgl.h 里面
#define LVGL_VERSION_MAJOR 8
#define LVGL_VERSION_MINOR 3
```



#### Top and sys layers

[Screen Layers - LVGL documentation](https://docs.lvgl.io/master/main-modules/display/screen_layers.html#)。

> LVGL uses two special layers named `layer_top` and `layer_sys`. Both are visible and common on all screens of a display. **They are not, however, shared among multiple physical displays.** The `layer_top` is always on top of the default screen (`lv_scr_act()`), and `layer_sys` is on top of `layer_top`.
>
> The `layer_top` can be used by the user to create some content visible everywhere. For example, a menu bar, a pop-up, etc. If the `click` attribute is enabled, then `layer_top` will absorb all user clicks and acts as a modal.
>
> ```
> lv_obj_add_flag(lv_layer_top(), LV_OBJ_FLAG_CLICKABLE);
> ```
>
> The `layer_sys` is also used for similar purposes in LVGL. For example, it places the mouse cursor above all layers to be sure it's always visible.



```c
    lv_obj_t* topObj = lv_layer_top();
    lv_color_t topColor = lv_obj_get_style_bg_color(topObj, LV_PART_MAIN);
    lv_opa_t topOpa = lv_obj_get_style_text_opa(topObj, LV_PART_MAIN);
    bool isHide = lv_obj_has_flag(topObj, LV_OBJ_FLAG_HIDDEN);

    lv_obj_t * obj1 = lv_btn_create(topObj);
    lv_obj_center(obj1);

    // lv_obj_set_style_bg_opa(topObj, LV_OPA_COVER, 0); 
    // lv_obj_add_flag(topObj, LV_OBJ_FLAG_HIDDEN);
```



top layer 在最上层。



#### OBJ ID

参考 [Widget ID - LVGL documentation](https://docs.lvgl.io/master/debugging/obj_id.html)。



#### Img 显示使用内置图标

所有内置图标图形见 [Overview - LVGL documentation](https://docs.lvgl.io/master/main-modules/fonts/overview.html#symbols)。

lv_symbol_def.h

创建图片然后使用即可，如

```c
lv_obj_t * img = lv_img_create(obj);
lv_img_set_src(img, LV_SYMBOL_USB );
...

// 添加鼠标图片如
// add mouse pointer a image, use lvgl internal image
lv_obj_t * mouse_cursor = lv_img_create(lv_scr_act());
lv_img_set_src(mouse_cursor, LV_SYMBOL_HOME);
lv_indev_set_cursor(ptr_indev, mouse_cursor);
```



## Debugging



[Debugging - LVGL documentation](https://docs.lvgl.io/master/debugging/index.html)。



## 优化相关

**基本**

- 首先看官方的 FAQ 和 移植相关文档。
- 无关的东西不加入编译。
- 仔细调整 `lv_conf.h` 、`lv_drv_conf.h` 等文件
  - buf pool 足够大（至少平时使用量的两倍），见 `lv_conf.h` 的 `LV_MEM_SIZE`，在各种设置内存池的地方，设置宽裕，各处的 cache 机制尽量都用上。
  - 图片缓存可以大一些，内存换速度。
  - 修改 `lv_conf.h` 里的 `LV_DISP_ROT_MAX_BUF` 提高软件旋转的速度。
  - 屏幕刷新，若内存充足则尽量使用 双 buf，内存紧张则使用 最小 1/10 单 buf，例子见 `lvgl\examples\porting\lv_port_disp_template.c`。
  - Linux 上显示 尽量使用 DRM 机制，可查可配的信息更多，FB 机制 已逐渐被弃用。 



**来自官方**

- 官网给出 **常见问题**（以下给出原文和机翻）

  > **如何加快我的用户界面？[FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html#how-do-i-speed-up-my-ui)。**
  >
  > - Turn on compiler optimization and enable instruction- and data-caching if your MCU has them.
  > - Increase the size of the display buffer.
  > - Use two display buffers and flush the buffer with DMA (or similar peripheral) in the background.
  > - Increase the clock speed of the SPI or parallel port if you use them to drive the display.
  > - If your display has an SPI port consider changing to a model with a parallel interface because it has much higher throughput.
  > - Keep the display buffer in internal RAM (not in external SRAM) because LVGL uses it a lot and it should have fast access time.
  > - Consider minimizing LVGL CPU overhead by updating Widgets:
  >   - only once just before each display refresh, and
  >   - only when it will change what the end user sees.
  >
  > 
  >
  > - 打开编译器优化并启用缓存（cache，如果您的 MCU 有）
  > - 增加显示缓冲区（display buffer）的大小
  > - 使用两个显示缓冲区并在后台使用 DMA（或类似外设）刷新缓冲区
  > - 如果使用 SPI 或并行端口驱动屏幕，请提高它们的时钟速度
  > - 如果您的屏幕有 SPI 端口，请考虑更改为具有并行接口的型号，因为它具有更高的吞吐量
  > - 将显示缓冲区保留在内部 RAM（而不是外部 SRAM）中，因为 LVGL 经常使用它并且它应该具有快速访问时间
  >
  > 
  >
  > **如何减少闪存/ROM的使用？[FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html#how-do-i-reduce-flash-rom-usage)。**
  >
  > You can disable unused features (such as animations, file system, GPU etc.) and widget types in *lv_conf.h*.
  >
  > If you are using GCC/CLANG you can add `-fdata-sections -ffunction-sections` compiler flags and `--gc-sections` linker flag to remove unused functions and variables from the final binary. If possible, add the `-flto` compiler flag to enable link-time-optimisation together with `-Os` for GCC or `-Oz` for CLANG and newer GCC versions.
  >
  > 
  >
  > 您可以在 `lv_conf.h` 中 禁用 所有未使用的功能（例如动画、文件系统、GPU 等）和对象类型。
  >
  > 如果您使用 GCC/CLANG，则可以添加 `-fdata-sections -ffunction-sections` 编译器标志（compiler flags）和 `--gc-sections` 链接器标志（linker flag），以从最终二进制文件中删除未使用的函数和变量。如果可能，请添加 `-flto` 编译器标志（compiler flag）以启用链接时优化（link-time-optimisation），以及 `-Os`（适用于 GCC）或 `-Oz`（适用于 CLANG）。
  >
  > 
  >
  > **如何减少 RAM 使用量 [FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html#how-do-i-reduce-ram-usage)。**
  >
  > - Lower the size of the *Display buffer*.
  > - Reduce [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_MEM_SIZE) in *lv_conf.h*. This memory is used when you create Widgets like buttons, labels, etc.
  > - To work with lower [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_MEM_SIZE) you can create Widgets only when required and delete them when they are no longer needed.
  >
  > 
  >
  > - *减小显示缓冲区*的大小
  >
  > - 减少 `lv_conf.h` 中的 [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_internal.html#c.LV_MEM_SIZE)  。当您创建按钮、标签等对象时，会使用此内存。（即够用就行）
  >
  > - 要使用 更低的 [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_internal.html#c.LV_MEM_SIZE)，您可以仅在需要时创建对象，并在不再需要时删除它们
  >
  >   To work with lower [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_internal.html#c.LV_MEM_SIZE) you can create objects only when required and delete them when they are not needed anymore



**来自网络**

LVGL 优化帧率技巧 https://www.itgh.cn/post/aiecg2b1.html

> 1. 减少屏幕刷新次数。LVGL 的默认刷新率为 60Hz，这意味着每秒会刷新屏幕 60 次。如果您的应用程序不需要如此高的刷新率，可以将其降低到更低的值，例如 30Hz 或更低。这将减少屏幕刷新次数，从而提高帧率。
> 2. 减少屏幕元素数量。屏幕上的元素越多，LVGL 就需要更多的时间来处理和渲染它们。因此，减少屏幕上的元素数量可以提高帧率。您可以通过以下方式来减少元素数量：
>    - 删除不必要的元素
>    - 合并相似的元素
>    - 使用更简单的元素代替复杂的元素
> 3.  使用缓存LVGL。支持缓存，这意味着您可以将屏幕上的元素缓存起来，以便下次使用时不需要重新渲染。这可以提高帧率，因为 LVGL 不需要重新渲染缓存的元素。
> 4. 使用异步更新LVGL。支持异步更新，这意味着您可以将更新操作放在后台线程中，从而避免阻塞主线程。这可以提高帧率，因为主线程可以继续处理其他任务，而不必等待更新操作完成。
> 5.  优化图形渲染LVGL。使用 GPU 来渲染图形，因此优化图形渲染可以提高帧率。以下是一些优化图形渲染的技巧：
>    - 使用简单的图形元素
>    - 避免使用透明度
>    - 避免使用渐变
>    - 避免使用阴影和反射
> 6. 使用硬件加速。LVGL 支持硬件加速，这意味着您可以使用 GPU 来加速图形渲染。如果您的设备支持硬件加速，可以启用它以提高帧率。
> 7. 使用 LVGL 的优化选项LVGL 提供了一些优化选项，可以帮助您提高帧率。以下是一些常用的优化选项
>    - LV_ANTIALIAS：启用抗锯齿
>    - LV_DPI：设置屏幕 DPI
>    - LV_COLOR_DEPTH：设置颜色深度
>    - LV_VDB_SIZE：设置虚拟显示缓冲区的大小
>
> 总之，优化 LVGL 的帧率需要综合考虑多个因素，包括屏幕刷新率、屏幕元素数量、缓存、异步更新、图形渲染、硬件加速和 LVGL 的优化选项。通过优化这些因素，您可以提高 LVGL 的帧率，从而提高应用程序的性能和响应速度。



通过改 buf 大小，各种测试

https://blog.csdn.net/weixin_43862847/article/details/109318017



优化界面来优化帧率

https://blog.csdn.net/qq_18454025/article/details/134536768



不使用画点函数 flush，开 O2 优化等级，DPI 计算，堆栈设置，

buf 大小（双 buf 快于 单 buf，全屏大小 buf 优于 1/4 大小 buf， 优于 1/8 大小 buf）

https://www.bilibili.com/read/cv17894963/



## 问题解决

- 启用 LVGL 自带 log：[Logging - LVGL documentation](https://docs.lvgl.io/master/debugging/log.html)。



- 支持操作系统、外置内存、以及硬件加速（LVGL已内建支持STM32 DMA2D、SWM341 DMA2D、NXP PXP和VGLite）。

  跟进 LVGL 最新进展！！！



- 官网给出 **常见问题**（以下机翻）：[FAQ - LVGL documentation](https://docs.lvgl.io/master/introduction/faq.html)。

> **LVGL 无法启动、随机崩溃或显示屏上不绘制任何内容。可能是什么问题？**
>
> - Try increasing [`LV_MEM_SIZE`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_MEM_SIZE).
> - Be sure your display works without LVGL. E.g. paint it to red on start up.
> - Enable [Logging](https://docs.lvgl.io/master/debugging/log.html#logging).
> - Enable assertions in `lv_conf.h` (`LV_USE_ASSERT_...`).
> - If you use an RTOS:
>   - Increase the stack size of the task that calls [`lv_timer_handler()`](https://docs.lvgl.io/master/API/misc/lv_timer_h.html#_CPPv416lv_timer_handlerv).
>   - Be sure you are using one of the methods for thread management as described in [Operating Systems and Threads](https://docs.lvgl.io/master/integration/overview.html#threading).
>
> 
>
> - 尝试增加 LV_MEM_SIZE.
> - 确保 lv_disp_t 和 lv_indev_t 是 lv_fs_drv_t 全局的或静态的。
> - 确保您的显示器在没有 LVGL 的情况下也能正常工作。例如，在启动时将其涂成红色。
> - 启用日志记录
> - 在 lv_conf.h 中启用断言( LV_USE_ASSERT_... )
> - 如果您使用 RTOS
>   - 增加调用 lv_timer_handler() 所在线程的堆栈大小
>   - 确保您使用了互斥体，如下所述：操作系统和中断
>
> 
>
> **我的显示驱动程序没有被调用。我错过了什么？**
>
> Be sure you are calling [lv_tick_inc](https://docs.lvgl.io/master/API/tick/lv_tick_h.html#_CPPv411lv_tick_inc8uint32_t)(x) as prescribed in [Tick Interface](https://docs.lvgl.io/master/integration/overview.html#tick-interface) and are calling [`lv_timer_handler()`](https://docs.lvgl.io/master/API/misc/lv_timer_h.html#_CPPv416lv_timer_handlerv) as prescribed in [Timer Handler](https://docs.lvgl.io/master/integration/overview.html#timer-handler).
>
> Learn more in the [Tick Interface](https://docs.lvgl.io/master/integration/overview.html#tick-interface) and [Timer Handler](https://docs.lvgl.io/master/integration/overview.html#timer-handler) sections.
>
> 
>
> 确保您在 中断 中调用 `lv_tick_inc (x)` 和 在 main 的 `while(1)` 中调用 `lv_timer_handler()` 。
>
> 在Tick 界面和计时器处理程序部分了解更多信息。
>
> 
>
> **为什么显示驱动程序只被调用一次？仅刷新显示屏的上部。**
>
> Be sure you are calling [lv_display_flush_ready](https://docs.lvgl.io/master/API/display/lv_display_h.html#_CPPv422lv_display_flush_readyP12lv_display_t)(drv) at the end of your "*display flush callback*" as per the [Flush Callback](https://docs.lvgl.io/master/main-modules/display/setup.html#flush-callback) section.
>
> 
>
> 确保您在“显示刷新回调”结束时调用`lv_disp_flush_ready (drv)`。
>
> 
>
> **为什么我在屏幕上只看到垃圾？**
>
> There is probably a bug in your display driver. Try the following code without using LVGL. You should see a square with red-blue gradient.
>
> ```c
> #define BUF_WIDTH 255
> uint16_t buf[BUF_WIDTH];
> uint32_t i;
> for(i = 0; i < BUF_WIDTH; i++) {
>   lv_color_t c = lv_color_mix(lv_color_hex(0xff0000), lv_color_hex(0x00ff00), i);
>   buf[i] = lv_color_to_u16(c);
> 
>   lv_area_t a;
>   a.x1 = 5;
>   a.x2 = a.x1 + BUF_WIDTH - 1;
>   a.y1 = 10 + i;
>   a.y2 = 10 + i;
>   my_flush_cb(NULL, &a, (void*) buf);
> }
> ```
>
> 
>
> **为什么我在屏幕上看到无意义的颜色？**
>
> The configured LVGL color format is probably not compatible with your display's color format. Check [`LV_COLOR_DEPTH`](https://docs.lvgl.io/master/API/lv_conf_h.html#c.LV_COLOR_DEPTH) in *lv_conf.h*.
>
> 
>
> LVGL 的颜色格式可能与您显示器的颜色格式不兼容。在 lv_conf.h 中检查 LV_COLOR_DEPTH_。
>
> 
>
> **如何使用操作系统？**
>
> To work with an operating system where tasks can interrupt each other (preemptively), you must ensure that no LVGL function call be called while another LVGL call is in progress. There are several ways to do this. See the [Operating Systems and Threads](https://docs.lvgl.io/master/integration/overview.html#threading) section to learn more.
>
> 
>
> 要使用任务可以相互中断（抢占式）的操作系统，您应该使用互斥锁来保护 LVGL 相关的函数调用。请参阅 操作系统和中断 部分以了解更多信息。
>



## LVGL 源码编码规范

[Coding Style - LVGL documentation](https://docs.lvgl.io/master/contributing/coding_style.html)。


