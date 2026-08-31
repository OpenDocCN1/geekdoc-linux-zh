
# Android 入口

[Android](http://en.wikipedia.org/wiki/Google_Android "wikipedia entry") 是 Google 和开放手机联盟（Open Handset Alliance）开发的一款软件平台和操作系统，专为小型设备和智能手机设计。

包含 Android 开发相关的各个方面，从新手入门、Android Linux 内核、Android 系统、应用开发到 Android 社区以及各类基于 Android 开发的产品信息。

# 新手入门

Android 系统概览，从系统版本、历史、设计、架构到工具和各类教程。

## Introduction to Android

> 来源：[eLinux.org](http://eLinux.org/Android_Intro "http://eLinux.org/Android_Intro")

### Android Intro

#### Overview

Android 是 Google 和开放手机联盟编写的软件平台和操作系统，适用于小型设备与智能手机。

[Android 维基百科条目](http://en.wikipedia.org/wiki/Google_Android)是了解 Android 功能、历史和方向的绝佳资源。此处不再重复该网站上的信息。

Android 的官方网站是[`www.android.com/`](http://www.android.com/)。从这里可以找到以下链接：

- [Android Market](http://www.android.com/market/)——开发者可以在此发布（免费或付费）在 Android 设备上运行的应用程序，用户也可以在此下载这些应用。
- [Android 开发者网站](http://developer.android.com/index.html)——软件开发者可以在这里学习如何为 Android 设备编写应用，或修改 Android 软件本身。
- [Android 开源项目](http://source.android.com/)——可在此找到 Android 操作系统（包括 Linux 内核、库、Dalvik VM 及 Android 系统的其余部分）的源代码。
- [Android 在嵌入式系统中的发展](https://training.linuxfoundation.org/free-linux-training/download-training-materials/growth-of-android-in-embedded-systems)——该 Linux 培训出版物包含大量关于 Android 在传统嵌入式 Linux 领域当前（截至 2013 年初）地位的优质资料。

点击“What is Android”选项卡会跳转到[`www.android.com/about/`](http://www.android.com/about/)页面，其中包含一些高层要点和一段有关 Android 历史简介的视频。

#### Videos

##### Prototype Video

2007 年 11 月，Google 发布了一段展示早期 Android 原型功能的视频。参见[`www.youtube.com/watch?v=1FJHYqE0RDg`](http://www.youtube.com/watch?v=1FJHYqE0RDg)

##### G1 Product Video

第一款基于 Android 的手机产品是 G1，由 HTC 制造，并由 T-Mobile 销售。

G1 的首页位于[`www.t-mobileg1.com/`](http://www.t-mobileg1.com/)，该网站包含大量介绍 G1 和 Android 功能的视频和解说。

Engadget 对 G1 功能的手把手测评视频（2008 年 9 月）：[`www.engadget.com/2008/09/23/video-android-walkthrough-on-t-mobile-g1/`](http://www.engadget.com/2008/09/23/video-android-walkthrough-on-t-mobile-g1/)

#### Technical Information

一个良好的技术信息起点是 Google 的[“What is Android?”页面](http://developer.android.com/guide/basics/what-is-android.html%7C)

另一个包含技术信息的好地方是 [Android FAQ](http://android-dls.com/wiki/index.php?title=Android_FAQ)

此外，还可以参考本站的 [Android Architecture](http://eLinux.org/Android_Architecture "Android Architecture")。

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

- [Android](http://eLinux.org/Category:Android "Category:Android")

## Design and Architecture

> 来源：[eLinux.org](http://eLinux.org/Android_Architecture "http://eLinux.org/Android_Architecture")

### Android Architecture

参见 Google 的[“What is Android?”页面](http://developer.android.com/guide/basics/what-is-android.html)了解 Android 组件的概览和架构图。

该页面上的图表几乎出现在我所见过的所有关于 Android 技术主题的演示中（除了我自己的演示）。

#### Architecture Diagram

以下是 Android 架构图，摘自[此处](http://developer.android.com/images/system-architecture.jpg)。

![Android-system-architecture.jpg](http://eLinux.org/File:Android-system-architecture.jpg)

另见 [Android 内部结构图](http://www.makelinux.net/android/internals/)

Android 主要包含以下几个层级：

- 应用程序（用 Java 编写，在 Dalvik 上执行）
- 框架服务与库（主要用 Java 编写）
  - 应用程序和大部分框架代码在虚拟机中执行
- 原生库、守护进程和服务（用 C 或 C++ 编写）
- Linux 内核，其中包括：
  - 用于硬件、网络、文件系统访问和进程间通信的驱动程序

#### Overview presentations

- [Android 不仅仅是 Linux 上的 Java](http://kobablog.wordpress.com/2011/05/22/android-is-not-just-java-on-linux/)
  - Tetsuyuki Kobayashi 的关于 Android 概览的精彩演示
- Karim Yaghmour 的 Android 内部结构演示
  - [`www.opersys.com/blog/android-internals-101103`](http://www.opersys.com/blog/android-internals-101103)
  - 可在该页面找到视频和幻灯片
- [Mythbusters_Android.pdf](http://eLinux.org/images/2/2d/Mythbusters_Android.pdf "Mythbusters Android.pdf") Matt Porter 在 ELC Europe 上的演示
  - 包含一些展示 Android 有问题的代码和策略的片段

#### Breakdown of running Android system

快速了解 Android 内容和启动时运行的程序，请访问：

- [`benno.id.au/blog/2007/11/13/android-under-the-hood`](http://benno.id.au/blog/2007/11/13/android-under-the-hood)

#### Relation to the Linux kernel

这里是 [Greg Kroah-Hartman 关于 Android 的演示](http://github.com/gregkh/android-presentation/downloads)，来自 CELF 2010 大会，讨论了 Google/Android 如何与 Linux 社区合作（或不合作）。

#### Java

Java 被用作应用程序编程语言，但会将其转换为非 Java 字节码，以供自定义解释器（Dalvik）在运行时解释执行。

##### Java/面向对象哲学

在实现 Android 系统时，实用性比纯粹性更重要。

Dianne Hackborn 是从事 Android 开发的的主要工程师之一，她写道：

> 我并不是一个不喜欢面向对象设计的 C 程序员。事实上，在 Android 之前，我的主要语言是 C++……老实说，Java 真的很烦人，它引入了太多开销，而这些在 C++ 中我可以用非常优雅的面向对象概念以更轻量的方式实现。
>
> 尽管 Java 有很多优点使其适合 Android，但它也存在不少设计缺陷和不足，因此我们无法做到完全完美的面向对象。
>
> 最后，展望未来，我们的 API 约定是以一种允许我们在当时可用的硬件上交付性能良好的系统的方式来定义的。随着情况的变化（虽然在缓慢变化，但还远远不够），这可能会改变……然而，我可能会倾向于保留这些 API 约定，仅仅是为了与现有的一切保持一致。当然，如果 Android 取得成功，并且在十年后我们正在设计一套全新的下一代 Android 框架……那么，世界将会不同。

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

- [Android](http://eLinux.org/Category:Android "Category:Android")

## Necessary tools

> 来源：[eLinux.org](http://eLinux.org/Android_Tools "http://eLinux.org/Android_Tools")

### Android Tools

以下是一些对 Android 开发有用的开发工具

#### Android SDK

##### 主机端工具



## Android SDK

### host-side tools

#### adb

`adb` is the android debugger - it also doubles as file transfer agent. The setup consists of an `adbd` on the target in the `/sbin` directory. On the host two programs are run: the `adb` application (in the SDK's `tools` directory) and an adb server, started by the `adb` application.

For emulators, adb will usually run automagically.

For real boards - with debugging over USB, you might need to do work, as is documented here: [`developer.android.com/guide/developing/device.html#setting-up`](http://developer.android.com/guide/developing/device.html#setting-up).

For real boards that do not have a USB connection but have Ethernet instead, you might need to do a few tricks.

* make sure that `adbd` runs on the board. If it doesn't run, you might want to check the `init.rc` file.
* make sure that the network connection between host and the board is working - test pinging both ways.
* on the host, type the following (you need to specify the board's IP address on the host):

```
ADBHOST=<target-ip> tools/adb kill-server
ADBHOST=<target-ip> tools/adb shell
```

* you should now get a prompt on the board, you can exit the prompt if you want.
* `tools/adb devices` should now list the device.

##### Running adbd on non-Android systems

It is sometimes useful to use `adbd` on non-Android embedded Linux systems. Here is a patch that can be applied to adb (source as of 2014-04-05) to change it to avoid "Android-isms" in the build. Instructions are in a `README.NONANDROID.TXT` file.

[File:0001-Add-support-for-non-Android-use-of-adbd.patch](http://eLinux.org/File:0001-Add-support-for-non-Android-use-of-adbd.patch "File:0001-Add-support-for-non-Android-use-of-adbd.patch")

This patch can be applied to your adb source by cd'ing to the directory `/system/core/adb`, applying the patch with:

```
$ git am 0001-Add-support-for-non-Android-use-of-adbd.patch
```

#### aapt

The Android Asset Packaging Tool is used to create, inspect and manage Android packages.

You can use this to see details about a package, it's resources, and xml information.

The [Android developer page on aapt](http://developer.android.com/guide/developing/tools/aapt.html) is somewhat meager.

See [Android aapt](http://eLinux.org/Android_aapt "Android aapt") for substantially more information.

#### ddms

The Dalvik Debug Monitor Server is a host-based tool which interacts with and Android target system and can show numerous bits of information, including the log, cpu and memory utilization, and lots of details about individual processes.

See the [DDMS developer guide](http://developer.android.com/guide/developing/tools/ddms.html)

#### Fastboot

[Android Fastboot](http://eLinux.org/Android_Fastboot "Android Fastboot") is a tool to boot and manipulate the partitions on an Android development phone.

#### Toolchains

Android provides pre-built toolchains (C/C++ compilers and linkers), but requires the installation of a java compiler (JDK) from an external source.

As of NDK version r5 (December 2010), the toolchains can now be used in standalone cross-compiler mode. See `docs/STANDALONE-TOOLCHAIN.html` in the NDK for information about this. Previously, the toolchains could be used within the build system, but it was difficult and error prone to compile native programs outside the Android build system with them.

#### Emulator

* Emulator - See [`developer.android.com/guide/developing/tools/emulator.html`](http://developer.android.com/guide/developing/tools/emulator.html)

The emulator is a version of QEMU, which mimics the instruction set of an ARM processor, and the hardware that one might find on a mobile phone. The emulator runs on an x86 system, but executes an ARM linux kernel and programs. The flow of control is:

* application ->
* dalvik VM ->
* C/C++ libraries ->
* ARM linux kernel ->
* emulated instructions and hardware (QEMU)->
* C libraries->
* x86 kernel ->
* real hardware

#### traceview

* Google's main page describing traceview: [`developer.android.com/guide/developing/tools/traceview.html`](http://developer.android.com/guide/developing/tools/traceview.html)

* [`www.bottomlesspit.org/file_download/2/Android_SDK_Traceview_tool.pdf`](http://www.bottomlesspit.org/file_download/2/Android_SDK_Traceview_tool.pdf)

    * good overview presentation by Olivier Bilodeau

    * presentation with speaker notes: [`www.bottomlesspit.org/file_download/3/Android_SDK_Traceview_tool_w_speakernotes.pdf`](http://www.bottomlesspit.org/file_download/3/Android_SDK_Traceview_tool_w_speakernotes.pdf)

* [Performance Tuning Android Applications](http://newfoo.net/2009/04/18/performance-tuning-android-applications.html)

    * straightforward article discussing traceview use to find an application bottleneck. April 2009.

### target-side tools

#### am

Activity Manager - can be used to start applications at the command line, or send intents to running applications.

#### dumpstate

dumps the state of the system. It scans the `/proc` filesystem, and collects various system properties, and puts them in a single report, suitable for sending to someone for support or development help.

#### logcat

This is the user tool for accessing the Android system log. This is implemented at a special option in adb (I'm not sure what the difference is between "adb logcat" and "adb shell logcat")

You can find lots of information about logcat on the [Android logger](http://eLinux.org/Android_logger "Android logger") page, and at [`developer.android.com/guide/developing/tools/adb.html#logcat`](http://developer.android.com/guide/developing/tools/adb.html#logcat)

#### monkey

#### procrank

procrank shows a listing of processes on the system, sorted by one of the memory utilization metrics. See [Android Memory Usage#procrank](http://eLinux.org/Android_Memory_Usage#procrank "Android Memory Usage")

#### service

Can be used to send an individual service message.

```
Usage: service [-h|-?]
       service list
       service check SERVICE
       service call SERVICE CODE [i32 INT | s16 STR] ...
Options:
   i32: Write the integer INT into the send parcel.
   s16: Write the UTF-16 string STR into the send parcel.
```

On one forum, I saw that you could switch between portrait and landscape with:

```
$ service call window 18 i32 1 # to set to landscape on the emulator
$ service call window 18 i32 0 # to set to portrait on the emulator
```

service list will show a list of different services that can be communicated with.

#### sqlite3

sqlite3 is a command-line database client program, for manipulating sqlite databases.

See [`www.higherpass.com/Android/Tutorials/Accessing-Data-With-Android-Cursors/`](http://www.higherpass.com/Android/Tutorials/Accessing-Data-With-Android-Cursors/) for a tutorial and some examples of using sqlite.

#### toolbox

toolbox is the equivalent of `busybox` on an Android system. That is, it is a multi-function program that provides many difference commands from a single binary. this includes things like: `ps`, `ls`, `top`, `stop`, `start` - commands to stop and start services on an Android system

See [Android toolbox](http://eLinux.org/Android_toolbox "Android toolbox") for details about individual commands.

## other tools



### agcc

`agcc` - A wrapper tool for compiling native Android apps (linked directly to bionic)

- See [`android-tricks.blogspot.com/2009/02/hello-world-c-program-on-using-android.html`](http://android-tricks.blogspot.com/2009/02/hello-world-c-program-on-using-android.html)

### bootchart

- See [Using Bootchart on Android](http://eLinux.org/Using_Bootchart_on_Android "Using Bootchart on Android")

### busybox

Android ships with a utility suite (called `toolbox`) that is not `busybox`.

You can get a binary `busybox` for Android [here](http://benno.id.au/blog/2007/11/14/android-busybox). The site includes instructions for easy installation on your device.

If you're interested in including `busybox` into a platform build:

- Precompiled binaries [here](https://github.com/Gnurou/busybox-android)
- A [presentation](https://video.linux.com/videos/busybox-integration-on-android) on how to build (or not) and integrate `busybox` into platform build (slides available [here](https://events.linuxfoundation.org/images/stories/pdf/lf_abs12_sun.pdf)).

### smem

`smem` - a tool for analyzing the memory usage on a system

- See [Using smem on Android](http://eLinux.org/Using_smem_on_Android "Using smem on Android") for more information

### strace

`strace`

- Statically linked binary available at: [`benno.id.au/blog/2007/11/18/android-runtime-strace`](http://benno.id.au/blog/2007/11/18/android-runtime-strace)
- Instructions for building Android `strace` - [`discuz-android.blogspot.com/2008/01/create-google-android-strace-tool.html`](http://discuz-android.blogspot.com/2008/01/create-google-android-strace-tool.html)

## Eclipse

The officially supported integrated development environment (IDE) is [Eclipse](http://www.eclipse.org/) (currently 3.4 or 3.5) using the Android Development Tools (ADT) Plugin, though developers may use any text editor to edit Java and XML files then use command line tools (Java Development Kit and Apache Ant are required) to create, build and debug Android applications as well as control attached Android devices (e.g., triggering a reboot, installing software package(s) remotely).

## Hardware

### Serial Cable for G1

You can build a serial cable to use with the G1, which is helpful to see kernel boot messages on the serial console.

See [`www.instructables.com/id/Android_G1_Serial_Cable`](http://www.instructables.com/id/Android_G1_Serial_Cable)

Back to [Android Portal](http://eLinux.org/Android_Portal "Android Portal")

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Glossary

> From: [eLinux.org](http://eLinux.org/Android_Glossary "http://eLinux.org/Android_Glossary")

# Android Glossary

Here are some Android terms (some even with definitions!!)

See also the developer glossary at: [`developer.android.com/guide/appendix/glossary.html`](http://developer.android.com/guide/appendix/glossary.html)

Back to [Android Portal](http://eLinux.org/Android_Portal "Android Portal")

## Contents

1. A
2. B
3. C
4. D
5. E
6. F
7. G
8. H
9. I
10. J
11. K
12. L
13. M
14. N
15. O
16. R
17. S
18. T
19. V
20. W
21. Z

## A

[aapt](http://eLinux.org/Android_aapt "Android aapt") - Android Asset Packaging Tool - a tool for creating, inspecting and modifying Android application packages.

`Activity` - A single focused thing the user can do on an Android device. Also, a java class in the Android framework, which is used as the superclass for an `Activity` implementation. See [`developer.android.com/reference/android/app/Activity.html`](http://developer.android.com/reference/android/app/Activity.html). "An Activity presents a visual user interface for one focused endeavor the user can undertake." See Activity on the page: [`developer.android.com/guide/topics/fundamentals.html`](http://developer.android.com/guide/topics/fundamentals.html)

`adb` - Android Debug Bridge - a tool for communicating between the host and a target Android system (including an emulator running on the host). See [`developer.android.com/guide/developing/tools/adb.html`](http://developer.android.com/guide/developing/tools/adb.html)

`ADP1` - Android Developer Phone 1

`ANR` - Application Not Responding - this is a type of bug where Android believes a process has hung. The system may kill the process, and leave information about it in `/data/anr` for post-mortem analysis.

`Android` - A robot resembling a human being - the name of the operating system produced by Google for mobile phones. Apparently, Andy Rubin, one of the original founders of Android, Inc. loves robots.

`AndroidManifest.xml` - A file describing the contents, permissions and other attributes of an Android application package. See [`developer.android.com/guide/topics/manifest/manifest-intro.html`](http://developer.android.com/guide/topics/manifest/manifest-intro.html)

`Android, Inc.` - A company founded by Andy Rubin and others to create a mobile phone operating system. Android, Inc. was acquired by Google in 2005.

`ASE` - Android Scripting Environment - the old name of Scripting Layer for Android. See Android Scripting

## B

`Binder` - An Interprocess Communication (IPC) mechanism. See [`cs736-android.pbworks.com/IPC-Binder`](http://cs736-android.pbworks.com/IPC-Binder) and [`groups.google.com/group/android-developers/msg/dc0e0e872de9b0d2`](http://groups.google.com/group/android-developers/msg/dc0e0e872de9b0d2)

`Bionic` - small C library used in Android devices

`Bootchart` - A mechanism to create visual charts of a Linux boot sequence, including the timing of process start and execution. See [Using Bootchart on Android](http://eLinux.org/Using_Bootchart_on_Android "Using Bootchart on Android")

## C

`Cliq` - The US name for the Motorola Android phone.

`Content Provider` - A piece of software on an Android system that provides information (content) to other software elements. See [`developer.android.com/guide/topics/providers/content-providers.html`](http://developer.android.com/guide/topics/providers/content-providers.html). Also, a class which is the superclass for code which acts as a content provider. See the [ContentProvider class documentation](http://developer.android.com/reference/android/content/ContentProvider.html)

`Cupcake` - The code name for Android version 1.5.

## D

`Dalvik` - Virtual Machine in which Android applications are run. This VM executes Dalvik bytecode, which is compiled from programs written in the Java language. Note that the Dalvik VM is not a Java VM (JVM).

Every Android application runs in its own process, with its own instance of the Dalvik virtual machine. Dalvik has been written so that a device can run multiple VMs efficiently. The Dalvik VM executes files in the Dalvik Executable (`.dex`) format which is optimized for minimal memory footprint. The VM is register-based, and runs classes compiled by a Java language compiler that have been transformed into the `.dex` format by the included `dx` tool.

See Android Dalvik VM for more information

`Donut` - The code name for Android version 1.6

`Dream` - Code name for the mobile phone hardware publicly called the t-Mobile G1, in the United States.

`Droid` - The name for an upcoming Android phone by Motorola (I believe this is the high-end phone, and Cliq is the low-end phone?)

## E

`Eclair` - The code name for Android version 2.1

## F

`fastboot` - a program which communicates with the developer firmware, and which is capable of loading new software on the ADP1 phone (including re-writing the flash partitions on the device). See [Android Fastboot](http://eLinux.org/Android_Fastboot "Android Fastboot")

`FreeType` - An open-source set of fonts and font system

`Froyo` - *Frozen Yogurt* - The code name for Android version 2.2

## G

`G1` - The name of the first Android-based mobile phone, from t-Mobile.

`Galaxy` - The name of the first Samsung Android phone



`Gingerbread` 是 Android 2.3 版本的代号。

`Goldfish` 是由模拟器提供的虚拟 ARM 平台的名称。它执行 ARM926T 指令，并具有用于输入和输出的钩子——例如读取模拟器中的按键或显示视频输出。有一个 `goldfish` 配置文件，用于编译可在该模拟平台上运行的 Linux 内核。

`Google` 是一家大型网络搜索公司，也是 Android 的主要开发者。

## H

`Honeycomb` 是 Android 3.0 版本的代号，尤其针对平板电脑设计。

## I

`Ice Cream Sandwhich` 指 Android 2.4 或 3.1 版本，是 `Gingerbread` 和/或 `Honeycomb` 的后续版本（可能表明开发分支）。参见 [`techcrunch.com/2011/01/11/android-ice-cream-sandwich/`](http://techcrunch.com/2011/01/11/android-ice-cream-sandwich/)。

`init` 是 Android 系统中运行的第一个用户空间程序。它不是标准的 Linux 风格 `init` 程序（后者会处理 `/etc/inittab` 文件），而是处理根文件系统根目录中名为 `init.rc` 的脚本。参见 [Android Booting#'init'](http://eLinux.org/Android_Booting#.27init.27 "Android Booting")。

`Intent` 是一种在不同 Android 组件之间发送消息的机制。消息通过 `Intent` 对象传递，该对象是一个数据结构，包含要执行的操作描述或已发生事项的公告。

## J

`Java` 是一种最初由 Sun 开发、现用于开发 Android 应用程序的编程语言。需要注意的是，虽然 Android 应用使用 `Java` 语言，但 Java 字节码和 Java 虚拟机并未被使用。更多信息参见 `Dalvik` 条目。

`JDK` 指 Java 开发工具包。

`Jellybean` 是 Android 4.1、4.2 和 4.3 版本的代号。

`JNI`（Java 本地接口，[维基百科条目](http://wikipedia.org/wiki/Java_Native_Interface)）是一种编程框架，允许 Java 代码调用“本地”代码（即用其他语言（如 C、C++ 或汇编）编译的代码），或被其调用。

## K

`KitKat` 是 Android 4.4 版本的发布名称。

## L

`Linux` 是一个开源操作系统内核，最初由 Linus Torvalds 开发，后由全球数千名开发者不断完善。

`Live-android` 是一个创建[Android 自启动光盘](http://code.google.com/p/live-android/)的项目，用于在通用 x86 平台上运行 Android。

`logcat` 是一条查看系统日志中消息的命令。参见 [Android logger](http://eLinux.org/Android_logger "Android logger")。

## M

`manifest file` 参见 `AndroidManifest.xml`。

`mahimahi` 是用于 Nexus One 产品开发板的内核机器名称。

`MSM`（移动站调制解调器）是高通公司制造的芯片组。例如，可在包含 Snapdragon 芯片组的手机（如 HTC Desire/Nexus One）中找到。

## N

`NDK`（[原生开发工具包](http://developer.android.com/sdk/ndk/index.html)）是一组工具、构建文件和指令，用于生成与 Android 系统配合使用的原生代码（通常是库）。原生库通常用作 `JNI` 的一部分（允许 Java 代码调用 C 代码，反之亦然）。

## O

`OpenGL ES` 是用于 Android 应用程序的 3D 图形系统和 API。

## R

`repo` 是 Android 仓库管理器。它是基于 `git` 工具的包装程序（用 Python 编写），用于管理构成整个 Android 代码库的多个 git 仓库。参见 [`source.android.com/download/using-repo`](http://source.android.com/download/using-repo)。

`rild`（无线接口层守护进程）是处理 Android 系统其余部分与“无线接口”（即基于 Android 的手机系统中的电话部分）之间通信的守护进程。在模拟器中，由于不存在电话硬件，因此有一程序运行以模拟无线接口。

## S

`Saphire`

`SL4A`（Android 脚本层）是一个执行环境，允许用户使用脚本语言（如 Python 或 Ruby）而非 Java 来编写 Android 程序。参见 Android Scripting。

`SGL` 是 Android 应用程序的 2D 图形层。

`SQLite` 是一个功能强大且轻量级的关系数据库引擎，由 Android 系统组件使用，并可供所有 Android 应用程序使用。

## T

`TARGET_PRODUCT` 是构建系统使用的环境变量，用于指示软件应针对的产品。该变量及其他 `TARGET_*` 变量通过 `build/envsetup.sh` 文件中的 `choosecombo()` 函数设置。如果未设置，当你 `source` 完 `build/envsetup.sh` 后运行 `m` 别名时，`TARGET_*` 变量将使用默认值。否则，请使用 `choosecombo()` 函数进行设置。

例如：`$ cd mydroid ; source build/envsetup.sh ; choosecombo`

`TARGET_PRODUCT` 的选项取决于仓库中 `build/target/products` 和 `vendor/*/*/AndroidProducts.mk` 文件下的 `AndroidProducts.mk` 条目。

`toolbox` 是 Android 系统中的一个多功能程序名称。该程序包含可让 `toolbox` 扮演不同程序和工具的代码。通常 `toolbox` 存储在 `/system/bin` 中，并通过符号链接指向其他名称。运行时，它使用 `argv[0]` 决定模拟哪个程序。在这方面，它与 `busybox` 非常相似，后者是许多其他嵌入式 Linux 系统使用的另一多功能程序。

`Trout` 是 HTC Dream 硬件（用于 T-Mobile G1 和 ADP1）的 ARM Linux 内核机器 ID。参见 [`www.arm.linux.org.uk/developer/machines/list.php?id=1440`](http://www.arm.linux.org.uk/developer/machines/list.php?id=1440)。

## V

`vold`（卷守护进程）是 Android 系统中负责管理文件系统（卷）挂载和卸载的进程。

## W

`wakelocks` 是 Android 电源管理的内核机制。当线程持有 wakelock 时，内核将避免进入低功耗状态。

返回 [Android Portal](http://eLinux.org/Android_Portal "Android Portal")。

## Z

`zygote` 是第一个 Dalvik 虚拟机实例，系统中启动的所有其他 Java 应用程序都是从 `zygote` 派生而来。

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# 教程和课程材料

> 来源：[`eLinux.org`](http://eLinux.org/Android_Tutorials "http://eLinux.org/Android_Tutorials")

# Android 教程

以下是一些 Android 和 Android 开发的“入门”教程：

*   [`vis.berkeley.edu/courses/cs160-sp08/wiki/index.php/Getting_Started_with_Android`](http://vis.berkeley.edu/courses/cs160-sp08/wiki/index.php/Getting_Started_with_Android)

*   [一些在 Android 上从零构建 Linux 应用和库的简单 HOWTO](http://forum.xda-developers.com/showthread.php?t=631818)

    *   包含构建 `busybox`、`jupp`（文本编辑器）、`libFLAC`、`xvid`、`nmap` 和 `dropbear` 等附加组件的说明。

*   [从 Panda 开箱到构建并加载应用](http://eLinux.org/Android_Tutorials_Unbox_to_App "Android Tutorials Unbox to App")

    *   包含 Panda 开箱、所需硬件、获取预构建 Panda 构建、编程、安装 Android 工具以及构建和安装应用到 Panda 上的说明。还包括指向演示应用“DisableSuspend” 的链接。本教程的特色构建来自 [`www.linaro.org`](http://eLinux.org/index.php?title=Linaro&action=edit&redlink=1 "Linaro (page does not exist)")，这是一个致力于改善 ARM 上游支持的组织。其中包含了所需的所有步骤。

## 目录

*   1 YouTube AndroidDevelopers 频道

*   2 Karim Yaghmour 的演示

    *   2.1 Karim 的课程材料

*   3 Michael Haim 的演示

*   4 Free Electrons Android 课程材料

## YouTube AndroidDevelopers 频道

YouTube 上的 Android Developers 频道中有大量视频（包括教程）。



参见[`www.youtube.com/profile?user=androiddevelopers#g/u`](http://www.youtube.com/profile?user=androiddevelopers#g/u)

## Karim Yaghmour 的演示文稿

*   [Android Internals](http://www.opersys.com/blog/abs-march2011) - Karim 在 [Android Builders Summit](http://events.linuxfoundation.org/events/android-builders-summit) 2011 上的演示。

*   [Porting Android to New Hardware](http://www.opersys.com/blog/abs-march2011) - Karim 在 [Android Builders Summit](http://events.linuxfoundation.org/events/android-builders-summit) 2011 上的演示。

*   [Android For Embedded Linux Developers](http://www.opersys.com/blog/andevcon-march2011) - Karim 在 [AnDevCon](http://www.andevcon.com/) 2011 上的演示。

*   [Understanding the Android System Server](http://www.opersys.com/blog/andevcon-march2011) - Karim 在 [AnDevCon](http://www.andevcon.com/) 2011 上的演示。

### Karim 的课程资料

点击课程页面上的“Courseware”缩略图：

*   [`www.opersys.com/training/embedded-android`](http://www.opersys.com/training/embedded-android)

*   [`www.opersys.com/training/android-development`](http://www.opersys.com/training/android-development)

*   [`www.opersys.com/training/embedded-linux`](http://www.opersys.com/training/embedded-linux)

*   [`www.opersys.com/training/linux-device-drivers`](http://www.opersys.com/training/linux-device-drivers)

## Michael Haim 的演示文稿

此外，Michael Haim 制作了大量关于 Android 主题的有用演示。可在[`www.abelski.com/`](http://www.abelski.com/)获取。

你需要创建一个账户才能使用这些资源，但它们对个人和学术用途是免费的。

以下类别提供了演示：

*   Android 基础知识

*   Android 工作坊

*   App 小部件开发

*   高效编程

*   Android 测试

*   Android 内部机制

## Free Electrons Android 课程资料

Free Electrons 在标准的 Creative Commons BY-SA 3.0 许可下发布了他们完整的 Android 培训材料：[`free-electrons.com/blog/free-android-training-materials/`](http://free-electrons.com/blog/free-android-training-materials/) 。它包含超过 400 页的幻灯片和实操实验。

有一个公共的`git`树和`LaTeX`源码格式，便于你根据需求调整这些材料（如果你是一名培训师）、翻译它们并为它们做出贡献。

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Android 历史

> 来源：[eLinux.org](http://eLinux.org/Android_History "http://eLinux.org/Android_History")

# Android 历史

此页面包含一些关于 Android 历史的趣闻。

## 目录

*   1 概述
*   2 2005年
*   3 2007年
*   4 2008年
*   5 2009年
*   6 2010年

## 概述

*   [Google 的开源 Android 操作系统将解放无线网络](http://www.wired.com/techbiz/media/magazine/16-07/ff_android?currentPage=all) Wired 文章，2008年6月

    *   描述了 Rubin 与 Page 的首次会面，以及 Google 对 Android 的整体策略。

    *   一些附加评论（见最后 4 段）位于：[被遗忘的 Android 历史](http://news.netapex.org/?page_id=463)

## 2005年

2007年8月 - Google 收购 Android Inc.

*   参见 [Google 收购 Android 用于其移动设备战略](http://www.businessweek.com/technology/content/aug2005/tc20050817_0949_tc024.htm)

    *   Business Week，2005年8月

## 2007年

*   参见 [I, Robot: 谷歌手机背后的男人](http://www.nytimes.com/2007/11/04/technology/04google.html?_r=1)

    *   纽约时报关于 Andy Rubin 的文章，2007年11月

2007年11月 - 开放手机联盟成立

## 2008年

2008年10月 - 首款手机 G1 在美国发售。

## 2009年

2009年2月 - [开放嵌入式软件基金会](http://www.oesf.org/) (OESF) 在日本[成立](http://techon.nikkeibp.co.jp/english/NEWS_EN/20090325/167661/)。

2009年4月 - 1.5 更新（代号“CupCake”）

2009年7月 - [Mentor Graphics 收购 Embedded Alley](http://www.linuxfordevices.com/c/a/News/Mentor-Graphics-acquires-Embedded-Alley/)

2009年9月 - [1.6 SDK 发布](http://www.androidcentral.com/android-donut-16-sdk-released-possibly-coming-users-next-month)（代号“Donut”）

2009年9月至11月 - Motorola、Samsung、HTC、Sony/Ericsson 宣布推出新款 Android 手机。

2001年10月 - 2.0 SDK 发布（代号“Eclair”）

2009年11月 - Google [宣布](http://googleblog.blogspot.com/2009/10/announcing-google-maps-navigation-for.html) [Maps Navigation](http://www.google.com/mobile/navigation/index.html#p=default) 计划

*   商业分析：[Google 重新定义颠覆：“低于免费”的商业模式](http://abovethecrowd.com/2009/10/29/google-redefines-disruption-the-%E2%80%9Cless-than-free%E2%80%9D-business-model/)

## 2010年

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# 版本

> 来源：[eLinux.org](http://eLinux.org/Android_Versions "http://eLinux.org/Android_Versions")

# Android 版本

## 目录

*   1 版本
    *   1.1 版本 1.1
    *   1.2 版本 1.5 (cupcake)
    *   1.3 版本 1.6 (donut)
    *   1.4 版本 2.1 (eclair)
    *   1.5 版本 2.2 (froyo)
    *   1.6 版本 4.4 (kitkat)
*   2 碎片化
    *   2.1 处理 API 级别
    *   2.2 需要支持多个版本

## 版本

更多详细信息，请参阅[Android 版本历史的维基百科页面](http://en.wikipedia.org/wiki/Android_version_history)

以下已发布的不同 Android 版本：

| 版本号 | 代号 | API 级别 | 主要特点 |

| --- | --- | --- | --- |

| 1.1 | *未知* | 2 | 基础版本，包含 Android 系统、电话、相机、基于 webkit 的浏览器、Google 搜索、联系人、日历、云同步、安卓市场等。 |

| 1.5 | Cupcake | 3 | 摄像机模式、视频和图片上传到网络、自动蓝牙连接、动画屏幕过渡 |

| 1.6 | Donut | 4 | 语音搜索 |

| 2.1 | Eclair | 7 | 更多屏幕分辨率、动态壁纸、MS Exchange 支持、UI 改版 |

| 2.2 | Froyo | 8 | Dalvik JIT、USB 网络共享、语音拨号、V8 和 javascript、Adobe Flash 支持 |

| 4.4 | KitKat | 19 | 低内存改进、传感器批处理、全屏 UI、ART 实验性测试 |

参见[维基百科文章](http://en.wikipedia.org/wiki/Android_(operating_system)#Update_history)了解关于不同版本的良好信息。

### 版本 1.1

SDK 于 2009年2月发布

### 版本 1.5 (cupcake)

SDK 于 2009年4月发布

内核版本：`2.6.27`

### 版本 1.6 (donut)

SDK 于 2009年9月发布

内核版本：`2.6.29`

### 版本 2.1 (eclair)

SDK 于 2009年10月发布

内核版本：`2.6.29`

### 版本 2.2 (froyo)

SDK 于 2010年5月发布

内核版本：`2.6.32`

### 版本 4.4 (kitkat)

SDK 于 2013年10月31日发布

内核版本：`3.10`?

Android 4.4 信息链接

*   官方 Android 博客文章：

    *   [`officialandroid.blogspot.com/2013/10/android-for-all-and-new-nexus-5.html`](http://officialandroid.blogspot.com/2013/10/android-for-all-and-new-nexus-5.html)

*   面向消费者的亮点：

    *   [`www.android.com/versions/kit-kat-4-4/`](http://www.android.com/versions/kit-kat-4-4/)

*   平台亮点：

    *   [`developer.android.com/about/versions/kitkat.html`](http://developer.android.com/about/versions/kitkat.html)

*   Android 开发者博客文章：

    *   [`android-developers.blogspot.com/2013/10/android-44-kitkat-and-updated-developer.html`](http://android-developers.blogspot.com/2013/10/android-44-kitkat-and-updated-developer.html)

*   API 亮点：

    *   [`developer.android.com/about/versions/android-4.4.html`](http://developer.android.com/about/versions/android-4.4.html)

*   SDK 更新：



- [`developer.android.com/tools/revisions/platforms.html`](http://developer.android.com/tools/revisions/platforms.html)

# Fragmentation

## Dealing with API levels

Developers should specify which API level their application requires or is known to work with.

See [`developer.android.com/guide/appendix/api-levels.html`](http://developer.android.com/guide/appendix/api-levels.html).

## Need to support multiple versions

Dianne Hackborn had this to say about fragmentation, after a developer complained about having to support different versions of Android:

Developers will never be able to rely on there only being one version to target. Never. Please drop that from your mind. This is not the case on Windows, it is not the case on MacOS X, it is not the case on any platform that is not uber-tightly controlled.

That would mean that every user, of every Android device, would be delivered free updates as long as they are using the device. This would completely prevent very interesting Android devices like the Dell Streak (which due to its interesting design requires some customizations to the platform), and would significantly limit the ability of manufacturers to push Android into other interesting places.

This would also very greatly slow down the development of the platform. Every release of Android would need to be extensively QAed on every existing Android device before it could go out to any of them. There are currently > 50 such devices, and that number is growing exponentially. Android just can't scale if that final productization and QA phase is not spread out to the manufacturers. A core part of what makes our Android model work is that most products are owned by their manufacturer.

Here's a very small example: you say that manufacturers would be responsible for the kernel. Obviously, that is required because the kernel needs to talk with whatever their hardware is. However, pretty much every release of the platform has snapped up to a more recent version of the Linux kernel. The QA for that version of the platform is done against that kernel on a small set of specific devices. For what you propose, it would either need to be QAed across all possible kernels, or require that all manufacturers upgrade to the newer kernel before it can go out to any devices.

I honestly think that developers who are demanding there be only one version they need to think about are living in a strange fantasy world. Windows developers have always needed to think about 3 or so active versions of Windows. From the stats I have seen there are regularly two very active versions of MacOS X that users run. Heck, if you are a web developer you need to consider different browsers and different versions implementing different versions of web standards.

I can more understand the issues from users, who want to be able to upgrade their current device to a newer version. Even there, though, if you compare us against another company that say releases a major platform update every year... we're not that bad. Look at the devices that have been out... how many at this point haven't received a significant platform update in the year since they came out? I think not many -- very few of them have been around for more than a year, and at this point the bulk of those have received at least one update. The main difference is that Android has gone through 3-4 significant updates in a year... so sure, not every one of those goes to every device, but I do think the manufacturers are showing that they are going to do some work to snap their devices to a more recent version, and I also think that as they are learning about Android and going through this upgrade experience the first few times they are learning how to better handle it.

At the end of the day Android is not a single monolithic uniform environment. That isn't what Android is intended to be, and honestly I think that this is something that should be pretty clear from day one. I consider that one of Android's strengths.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Linux 内核

Android 使用 Linux 作为底层的内核，并且对 Linux 做了改造，为智能设备定制了诸多新特性。

## Where to obtain

> From: [eLinux.org](http://eLinux.org/Android_Kernel_Download "http://eLinux.org/Android_Kernel_Download")

## Android Kernel Download

See [`source.android.com/source/building-kernels.html`](http://source.android.com/source/building-kernels.html).

Most of the following information is outdated.

### Main Google Android Kernels

The main Google repository with Android source code is at: [`android.googlesource.com/`](https://android.googlesource.com/).

There are (as of July 2014) 4 main separate kernel repositories at that site:

- `common`
- `exynos`
- `goldfish`
- `lk`
- `samsung`
- `tegra`
- `msm`
- `omap`

To download one of these and use it directly, you can use `git`. For example (do not use the `git` protocol to clone):

```bash
git clone https://android.googlesource.com/kernel/common.git kernel
```

To preserve your sanity, it's probably worth downloading this into a `kernel` directory in your overall Android source directory scheme.

You can use `repo`, following the instructions at [`source.android.com/download`](http://source.android.com/download), to pull down the entire Android source. However, when you download the rest of the Android source code using the `repo` command, you do **not** automatically get a kernel tree included. That is, a kernel git tree is not referenced in the default Android manifest file.

To add projects, such as the kernel, to your overall Android repository scheme, you add the appropriate kernel repository to your local `manifest.xml` file. This file is located in the `.repo` directory.

To include the `kernel/common` tree, include a line like this in `.repo/manifest.xml`:

```xml
<project path="kernel/common" name="kernel/common" />
```

The complete list of projects, including other kernel options besides `kernel/common`, is listed on [`android.googlesource.com/`](https://android.googlesource.com/).

Note that the default revision for git repositories is specified in the `<default>` tag in `manifest.xml` as `revision="master"`, but the `kernel/common` repository may not have a head called `master`. In that case, if you just type `repo sync kernel/common`, you may see the message:

```text
error: revision master in kernel/common not found
```

Typically, the heads in the `kernel/common` repository will be called `android-2.6.x` (where `x` is the kernel number); specifying this number in the manifest should allow `repo` to sync properly, i.e.:

```xml
<project path="kernel/common" name="kernel/common" revision="android-2.6.27"/>
```

You can view the heads by clicking on the project link from [`android.git.kernel.org/`](http://android.git.kernel.org/).

For more about `repo`, see [`source.android.com/download/using-repo`](http://source.android.com/download/using-repo).

### Other Repositories with Android-specific changes

- Linux kernel for omap and beagle-board, by Embinux: [`labs.embinux.org/git/cgit.cgi/repo/kernel.git`](http://labs.embinux.org/git/cgit.cgi/repo/kernel.git)
  - Clone with:

    ```bash
    git clone git://labs.embinux.org/repo/kernel.git kernel
    ```

### 'Raw' Android kernel patches

I do not know of any freely available patches for the Linux kernel with the Android fixes, as of November 2009. I have, however, heard of multiple efforts to extract the patches to make it easier to port the Android kernel features onto newer Linux kernels.

Here is a way of extracting raw Android patches at a certain point in time, though this may be dated:



```
(Do not use the git protocol to clone the source)
git clone https://android.googlesource.com/kernel/common.git android-kernel
cd android-kernel
git checkout --track -b android-2.6.32 origin/android-2.6.32
git fetch --tags git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-2.6.32.y.git
git shortlog v2.6.32.9..HEAD
git format-patch v2.6.32.9..HEAD 
```

Sum total 173 patches for the 2.6.32.9 kernel as of writing.

If anyone knows where raw android kernel patches are available, please add a link here. See also the [Android Kernel Features](http://eLinux.org/Android_Kernel_Features "Android Kernel Features") page for more information about individual kernel features.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# How to build

> From: [eLinux.org](http://eLinux.org/Android_Kernel_Build "http://eLinux.org/Android_Kernel_Build")

# Android Kernel Build

How to build an Android kernel.

The Android build system may or may not automatically rebuild a kernel for you.

This page documents how to build an Android kernel, independent of the regular Android "distribution" build system.

[FIXTHIS - nothing here yet.]

## Building an Individual application

Steps required to compile individual application package in Android SDK.

1.  Go to build directory under Android sdk directory

2.  Execute `source source envsetup.sh`

3.  Go to corresponding application directory

4.  Issue `mm` command to build the application only

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# How to install (on phone, on emulator, etc.)

> From: [eLinux.org](http://eLinux.org/Android_Kernel_Installation "http://eLinux.org/Android_Kernel_Installation")

# Android Kernel Installation

How to use a new kernel with the emulator or on a product.

In general, this will be very product-specific.

## Contents

*   1 With the G1/ADP1

    *   1.1 Installing a boot image

*   2 With the emulator

*   3 On a board using an SDCARD

    *   3.1 OMAP EVM

## With the G1/ADP1

On the ADP1, you can boot using a specific kernel using `fastboot`, which will send it to the board as part of the bootup sequence. Specify the kernel as one of the parameters to the `fastboot boot` option. See [`www.gotontheinter.net/content/fastboot-cheat-sheet`](http://www.gotontheinter.net/content/fastboot-cheat-sheet) for details.

### Installing a boot image

You can create a "boot" image directly, and install that to the boot or recovery flash partition manually. This can be done either using a running kernel or using `fastboot`.

See these instructions for doing that: [`android-dls.com/wiki/index.php?title=HOWTO:_Unpack,_Edit,_and_Re-Pack_Boot_Images`](http://android-dls.com/wiki/index.php?title=HOWTO:_Unpack,_Edit,_and_Re-Pack_Boot_Images)

Also, you can install the kernel into a recovery image, and install the recovery image using the system recovery procedure.

## With the emulator

You can specify the kernel to use with the emulator using the `-kernel` command line option.

There are some interesting notes about using the emulator without specifying a AVD file at: [`groups.google.com/group/android-platform/browse_thread/thread/591290fde1e9865a`](http://groups.google.com/group/android-platform/browse_thread/thread/591290fde1e9865a)

## On a board using an SDCARD

### OMAP EVM

For an OMAP EVM, using the Android image available from Mistral, place a new `uImage` on the SDCARD at the root the `vfat` partition. The bootloader will run the commands (from where??) to load the `uImage` and boot it.

Note that for the OMAP EVM, you need to have the board configured to boot from `sdcard`, rather than from flash.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# What version to use

> From: [eLinux.org](http://eLinux.org/Android_Kernel_Versions "http://eLinux.org/Android_Kernel_Versions")

# Android Kernel Versions

## Contents

*   1 Kernel versions known to run Android

    *   1.1 2.6.23

    *   1.2 2.6.25

    *   1.3 2.6.26

    *   1.4 2.6.29

    *   1.5 2.6.32

    *   1.6 2.6.35

*   2 Selecting a kernel tree for a new port

*   3 Android git kernel trees

## Kernel versions known to run Android

### 2.6.23

The first-generation Google-TV products (released about November, 2010) used kernel version 2.6.23\. It is speculated that this is due to existing binary driver support for the Intel chipsets used in those products.

### 2.6.25

The original (version 1.0) of Android for the G1/ADP1 used Linux version 2.6.25

### 2.6.27

The 1.5 release of Android (cupcake) for the G1/ADP1 used Linux version 2.6.27

### 2.6.29

As of September, 2009, the `kernel/common.git` tree for Android has a 2.6.29 kernel. Donut uses this kernel.

### 2.6.32

As of July 2010, the `kernel/common.git` tree for Android has a 2.6.32 kernel. This kernel is used by Froyo.

### 2.6.35

Gingerbread used kernel version 2.6.35.

## Selecting a kernel tree for a new port

This article has good information on porting Android to a new device. Note that it debates which kernel tree is appropriate to start with, for porting to a new device:

*   [`www.linuxfordevices.com/c/a/Linux-For-Devices-Articles/Porting-Android-to-a-new-device/`](http://www.linuxfordevices.com/c/a/Linux-For-Devices-Articles/Porting-Android-to-a-new-device/)

## Android git kernel trees

As of July 2010, the [android repository on kernel.org](http://android.git.kernel.org/) had the following kernel trees:

`kernel/common.git` This is the kernel tree that matches what is put into official Android products by Google or its partners

`kernel/experimental.git` some experimental stuff

`kernel/linux-2.6.git` mirror of Linus' kernel tree. This is a reference for the kernel tree used in Android

`kernel/lk.git` not a kernel tree, but a bootloader

`kernel/msm.git` kernel for MSM (Qualcomm chip used in many HTC products)

`kernel/omap.git` mirror of kernel tree maintained by texas instruments., supporting OMAP chips. usually based on `kernel.org` latest version, android products w OMAP chip can use this kernel port.

`kernel/tegra.git` nvidia kernel tree

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Kernel features

> From: [eLinux.org](http://eLinux.org/Android_Kernel_Features "http://eLinux.org/Android_Kernel_Features")

# Android Kernel Features

## Contents

*   1 Kernel features unique to Android

    *   1.1 Resources

    *   1.2 Temporary including in mainline 'staging'

    *   1.3 Android mainlining project

*   2 List of kernel features unique to Android

    *   2.1 Binder

    *   2.2 ashmem

    *   2.3 pmem

    *   2.4 logger

    *   2.5 wakelocks

    *   2.6 oom handling

    *   2.7 Alarm timers

        *   2.7.1 POSIX Alarm Timers

    *   2.8 paranoid network security

    *   2.9 timed output / timed gpio

    *   2.10 RAM-CONSOLE

    *   2.11 other kernel changes

*   3 Kernel configuration options

## Kernel features unique to Android

In the course of development, Google developers made some changes to the Linux kernel. The amount of changes is not extremely large, and is on the order of changes that are customarily made to the Linux kernel by embedded developers (approximately 250 patches, with about 3 meg. of differences in 25,000 lines). The changes include a variety of large and small additions, ranging from the wholesale addition of a flash filesystem (YAFFS2), to very small patches to augment Linux security (paranoid networking patches).

Various efforts have been made over the past few years to submit these to changes to mainline (mostly by Google engineers, but also by others), with not much success so far.

### Resources



A very good overview of the changes is available in a talk by John Stultz at ELC 2011. (The talk has a somewhat misleading name.)

- [Android OS for Servers](http://eLinux.org/images/8/89/Elc2011_stultz.pdf "Elc2011 stultz.pdf") - John Stultz, ELC 2011
  - This talks breaks down the differences between an Android Linux kernel and a stock Linux kernel, and provides information about the features of each.
- [`www.lindusembedded.com/blog/2010/12/07/android-linux-kernel-additions/`](http://www.lindusembedded.com/blog/2010/12/07/android-linux-kernel-additions/)
  - Lindus Embedded (Alex Gonzalez) has a listing of kernel changes based on an Android kernel for the Freescale MX51 SOC, with some good information about each change.
- [`yidonghan.wordpress.com/2010/01/28/porting-android-to-a-new-device/`](http://yidonghan.wordpress.com/2010/01/28/porting-android-to-a-new-device/)
  - Peter McDermott's excellent description of his work to port Android to the Nokia N810.
  - Also, see his annotated list of modified and added kernel files, at: [`www.linuxfordevices.com/files/misc/porting-android-to-a-new-device-p3.html`](http://www.linuxfordevices.com/files/misc/porting-android-to-a-new-device-p3.html)
  - See the project site [at sourceforge](http://android-n810.sourceforge.net/).
- [`www.slideshare.net/jollen/android-os-porting-introduction`](http://www.slideshare.net/jollen/android-os-porting-introduction)
  - Jollen Chen's excellent presentation on system-level Android features, including an overview of kernel features unique to Android: *Note: Parts of the presentation are in Chinese*

## Temporary including in mainline 'staging'

Some changes were temporarily added at the "staging" driver area in the stock kernel, but were removed due to lack of support. See [Greg KH blog post on -staging for 2.6.33](http://www.kroah.com/log/linux/staging-status-12-2009.html), where he announces the **removal** of various Android drivers from -staging.

## Android mainlining project

Several groups and individuals are working to get kernel changes from Android mainlined into the Linux kernel.

Please see [Android Mainlining Project](http://eLinux.org/Android_Mainlining_Project "Android Mainlining Project") for more information.

## List of kernel features unique to Android

Here is a list of changes/addons that the Android Project made to the linux kernel. As of September, 2011, these kernel changes are not part of the standard kernel and are only available in the Android kernel trees in the Android Open Source project.

This list does not include board- or platform-specific support or drivers (commonly called "board support").

### Binder

Binder is an Android-specific interprocess communication mechanism, and remote method invocation system.

See [Android Binder](http://eLinux.org/Android_Binder "Android Binder")

### ashmem

- ashmem - Android shared memory
  - implementation is in `mm/ashmem.c`

According to the Kconfig help "The ashmem subsystem is a new shared memory allocator, similar to POSIX SHM but with different behavior and sporting a simpler file-based API."

Apparently it better-supports low memory devices, because it can discard shared memory units under memory pressure.

To use this, programs open `/dev/ashmem`, use `mmap()` on it, and can perform one or more of the following ioctls:

- `ASHMEM_SET_NAME`
- `ASHMEM_GET_NAME`
- `ASHMEM_SET_SIZE`
- `ASHMEM_GET_SIZE`
- `ASHMEM_SET_PROT_MASK`
- `ASHMEM_GET_PROT_MASK`
- `ASHMEM_PIN`
- `ASHMEM_UNPIN`
- `ASHMEM_GET_PIN_STATUS`
- `ASHMEM_PURGE_ALL_CACHES`

From a thread on android-platform [source](http://groups.google.com/group/android-platform/browse_thread/thread/2fa6ba5ef9f81d22/0b91a39d108d02fc)

You can create a shared memory segment using:

```
fd = ashmem_create_region("my_shm_region", size);
if(fd < 0)
    return -1;
data = mmap(NULL, size, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
if(data == MAP_FAILED)
    goto out;
```

In the second process, instead of opening the region using the same name, for security reasons the file descriptor is passed to the other process via binder IPC.

The `libcutils` interface for `ashmem` consists of the following calls: (found in `system/core/include/cutils/ashmem.h`)

- `int ashmem_create_region(const char *name, size_t size);`
- `int ashmem_set_prot_region(int fd, int prot);`
- `int ashmem_pin_region(int fd, size_t offset, size_t len);`
- `int ashmem_unpin_region(int fd, size_t offset, size_t len);`
- `int ashmem_get_size_region(int fd);`

### pmem

- PMEM - Process memory allocator
  - implementation at: `drivers/misc/pmem.c` with include file at: `include/linux/android_pmem.h`
  - Brian Swetland says:

```
The pmem driver is used to manage large (1-16+MB) physically contiguous
regions of memory shared between userspace and kernel drivers (dsp, gpu,
etc).  It was written specifically to deal with hardware limitations of
the MSM7201A, but could be used for other chipsets as well.  For now,
you're safe to turn it off on x86.
```

David Sparks wrote the following: [source](http://groups.google.com/group/android-framework/msg/06bb9d8c294ce6d7)

```
2. ashmem and pmem are very similar. Both are used for sharing memory
between processes. ashmem uses virtual memory, whereas pmem uses
physically contiguous memory. One big difference is that with ashmem,
you have a ref-counted object that can be shared equally between
processes. For example, if two processes are sharing an ashmem memory
buffer, the buffer reference goes away when both process have removed
all their references by closing all their file descriptors. pmem
doesn't work that way because it needs to maintain a physical to
virtual mapping. This requires the process that allocates a pmem heap
to hold the file descriptor until all the other references are closed.

3. You have the right idea for using shared memory. The choice between
ashmem and pmem depends on whether you need physically contiguous
buffers. In the case of the G1, we use the hardware 2D engine to do
scaling, rotation, and color conversion, so we use pmem heaps. The
emulator doesn't have a pmem driver and doesn't really need one, so we
use ashmem in the emulator. If you use ashmem on the G1, you lose the
hardware 2D engine capability, so SurfaceFlinger falls back to its
software renderer which does not do color conversion, which is why you
see the monochrome image.
```

### logger

- logger - system logging facility
  - This is the kernel support for the 'logcat' command
  - The kernel driver for the serial devices for logging are in the source code `drivers/misc/logger.c`
  - See [Android logger](http://eLinux.org/Android_logger "Android logger") for more information about the kernel code
  - See Android Logging System for an overview of the system it supports

### wakelocks

- wakelock - used for power management files `kernel/power/wakelock.c`
  - Holds machine awake on a per-event basis until wakelock is released
  - See Android Power Management for detailed information

### oom handling

- oom handling modifications
  - lowmem notifications
  - implementation at: `drivers/misc/lowmemorykiller.c`
  - also at: `security/lowmem.c`

Informally known as the Viking Killer, the OOM handler simply kills processes as available memory becomes low. The kernel module follows rules for this that are supplied from user space in two ways:

1. init writes information about memory levels and associated classes:
2. The write value must be consistent with the above properties.
3. Note that the driver only supports 6 slots, so we have combined some of the classes into the same memory level; the associated processes of higher classes will still be killed first.
   - From `/init.rc`:



```
write /sys/module/lowmemorykiller/parameters/adj 0,1,2,4,7,15
write /sys/module/lowmemorykiller/parameters/minfree 2048,3072,4096,6144,7168,8192
```

1. User space sets the `oom_adj` of processes to put them in the correct class for their current operation. This redefines the meaning of `oom_adj` from that used by the standard OOM killer to something that is more aggressive and controlled.

These `oom_adj` levels end up being based on the process lifecycle defined here: [`developer.android.com/guide/topics/fundamentals.html#proclife`](http://developer.android.com/guide/topics/fundamentals.html#proclife)

### Alarm timers

This is the kernel implementation to support Android's `AlarmManager`. It lets user space tell the kernel when it would like to wake up, allowing the kernel to schedule that appropriately and come back (holding a wake lock) when the time has expired regardless of the sleep state of the CPU.

#### POSIX Alarm Timers

Note that POSIX Alarm timers, which implement this functionality (but not identically), was accepted into mainline Linux in kernel version 3.0.

See [Waking Systems from Suspend](https://lwn.net/Articles/429925/) and [`lwn.net/Articles/439364/`](http://lwn.net/Articles/439364/).

### paranoid network security

*   paranoid network security
    *   See [Android_Security#Paranoid_network-ing](http://eLinux.org/Android_Security#Paranoid_network-ing "Android Security")

### timed output / timed gpio

Generic gpio is a mechanism to allow programs to access and manipulate gpio registers from user space.

Timed output/gpio is a system to allow chaning a gpio pin and restore it automatically after a specified timeout. See `drives/misc/timed_output.c` and `drives/misc/timed_gpio.c`. This exposes a user space interface used by the vibrator code.

On ADP1, there is a driver at:

```
# cd /sys/bus/platform/drivers/timed-gpio
# ls -l
--w-------    1 0        0            4096 Nov 13 02:11 bind
lrwxrwxrwx    1 0        0               0 Nov 13 02:11 timed-gpio -> ../../../../devices/platform/timed-gpio
--w-------    1 0        0            4096 Nov 13 02:11 uevent
--w-------    1 0        0            4096 Nov 13 02:11 unbind
```

Also, there is a device at:

```
# cd /sys/devices/platform/timed-gpio
# ls -lR
.:
lrwxrwxrwx    1 0        0               0 Nov 13 01:34 driver -> ../../../bus/platform/drivers/timed-gpio
-r--r--r--    1 0        0            4096 Nov 13 01:34 modalias
drwxr-xr-x    2 0        0               0 Nov 13 01:34 power
lrwxrwxrwx    1 0        0               0 Nov 13 01:34 subsystem -> ../../../bus/platform
-rw-r--r--    1 0        0            4096 Nov 13 01:34 uevent

./power:
-rw-r--r--    1 0        0            4096 Nov 13 01:34 wakeup
```

### RAM_CONSOLE

This allows saving the kernel printk messages to a buffer in RAM, so that after a kernel panic they can be viewed in the next kernel invocation, by accessing `/proc/last_kmsg`.

Would be good to get more details on how to set this up and use it here! I guess this is something like `pramfs`?

### other kernel changes

Here is a miscellaneous list of other kernel changes in the mistral Android kernel:

*   switch events - `drivers/switch/*` userspace support for monitoring GPIO via `sysfs/uevent` used by `vold` to detect USB

*   USB gadget driver for ADB - `drivers/usb/gadget/android.c`

*   yaffs2 flash filesystem

*   support in FAT filesystem for `FVAT_IOCTL_GET_VOLUME_ID`

*   and more...

## Kernel configuration options

The file [Documentation/android.txt](http://android.git.kernel.org/?p=kernel/common.git;a=blob_plain;f=Documentation/android.txt;hb=HEAD) has a list of required configuration options for a kernel to support an Android system.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Board Support highlights

> From: [eLinux.org](http://eLinux.org/Android_Board_Support "http://eLinux.org/Android_Board_Support")

# Android Board Support

Porting Android to a new platform can be a challenge. Here are some resources to start with that:

## Contents

*   1 Processor Support
    *   1.1 ARM
        *   1.1.1 OMAP
    *   1.2 Mips
    *   1.3 x86
*   2 Individual Platform Support
    *   2.1 For Nexus One
        *   2.1.1 Unlocking the phone
        *   2.1.2 Serial port access
*   3 System Requirements
    *   3.1 RAM (>256M if possible)

## Processor Support

### ARM

Most ports of Android are to ARM-based platforms.

#### OMAP

*   Mentor Graphics and Texas Instruments support Android on OMAP processors via the [project](http://code.google.com/p/rowboat/%7CRowboat)

*   See also [Android on OMAP](http://eLinux.org/Android_on_OMAP "Android on OMAP"), which has a very thorough listing of issues faced in initially porting Android to OMAP

### Mips

Mentor Graphics did a port of Android to MIPS.

See [`www.mipsandroid.org`](http://www.mipsandroid.org)

(Unfortunately, this site requires registration.)

*   MIPS now has support for SMP on Android - see [MIPS Supports Symmetric Multiprocessing on Android Platform](http://edageek.com/2010/06/01/smartphones-smp/) - Posted by Ken Cheung in IP Cores on Tuesday, June 1, 2010

### x86

There is a whole well-developed project for Android on x86.

See [`www.android-x86.org/`](http://www.android-x86.org/)

At least one major product (Sony Internet TV) is reported to be x86-based. Intel has a team of developers working on Android issues. See Mark Gross' presentation from ELC 2010 for some tips from them about using Android

*   [Experiences in Android Porting, Lessons Learned,Tips and Tricks](http://eLinux.org/images/e/ee/ELC2010-android-xp-tips-tricks.pdf "ELC2010-android-xp-tips-tricks.pdf") by Mark Gross, April 2010, Embedded Linux Conference 2010

*   Intel is working on "native" Android support. See [Intel prepping x86 port for Android 2.2](http://www.linuxfordevices.com/c/a/News/Intel-x86-port-and-Sprint-upgrade-plans/?kc=LNXDEVNL063010) By Eric Brown, lwn.net, 2010-06-28

## Individual Platform Support

### For Nexus One

#### Unlocking the phone

Bryan Swetland says: ([here](http://torvalds-family.blogspot.com/2010/02/happy-camper.html?showCom))

All Nexus One devices have an unlockable bootloader (`fastboot oem unlock`), which, once unlocked will allow you to reflash the boot partition (kernel + ramdisk), system partition, etc.

Full kernel sources are available here: [`android.git.kernel.org/?p=kernel/msm.git;a=shortlog;h=refs/heads/android-msm-2.6.29-nexusone`](http://android.git.kernel.org/?p=kernel/msm.git;a=shortlog;h=refs/heads/android-msm-2.6.29-nexusone) (make `mahimahi_defconfig` to configure just like the production kernel). We're in the process of rebasing up to .32, on our way to .33 and beyond.

#### Serial port access

There are some serial port pins available on the micro-USB connector, which you can access if you have the right hardware.

See this [discussion on xda-developers](http://forum.xda-developers.com/showthread.php?t=625434) for detailed information and links.

Brian Swetland says: TTL level (~3.3v?) serial is present on the D+/D- pins of the micro USB connector whenever VBUS (usb +5v power) is not present. This is physical UART1 (`ttyMSM0`). In standard builds the FIQ kernel debugger runs there. You'll have to disable the FIQ debugger and enable the serial device in your kernel config if you want to use it as a regular serial port.

## System Requirements

### RAM (>256M if possible)

Dianne Hackborn had this to say (in August, 2009) about RAM requirements for Android:



I would recommend at least 128MB available to the `kernel`. In many architectures, a big chunk of RAM will be dedicated to the radio, so you need to take that into account, and the 128MB recommendation does not cover that. Also if your architecture allocates graphics surfaces in user space, bump it up by 16MB or so (The Qualcomm devices I have experience do their allocations in RAM outside of that accessible to the kernel.) And of course this also depends on the size and density of your screen, camera megapixels, etc. If the screen has more pixels than 320x480 or the camera is more than 3 megapixels, bump the size up accordingly.

For reference, the myTouch has 192MB of RAM which on 1.6 only left 100MB left for the kernel and user space, and was `very` tight on RAM. Don't go that low. An update to the Qualcomm radio apparently frees up a bunch of space, adding over 10MB or so to user space... that should run even 2.2 okay. At this level, though, the amount of RAM is probably the most important aspect to how well the device will run. Don't skip on RAM, and you'll have a much better running device, with a lot fewer headaches as you try to get everything working well. That is from painful experience. :)

Another reference point -- the Droid has 256MB RAM, which runs the system well, but it also does its graphics allocations in user space and has a high density screen so you can still end up not keeping as many processes running as you'd like if loading large pages with the browser, running lots of background services, etc.

The Nexus One has 512MB of RAM and honestly that is really more than we know what to do with. It is great. :) I ended up putting some code into the activity manager to put a hard limit on the number of processes we would keep around, because there was so much memory we had often could keep way more processes than was useful. That was never an issue on Droid. ;)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

* [Android](http://eLinux.org/Category:Android "Category:Android")

# Android 系统信息

讨论 Android 系统部分，内容涵盖系统引导、电源管理、系统安全、Dalvik Java 虚拟机、包管理、网络、文件系统和日志系统。

# Booting

> From: [eLinux.org](http://eLinux.org/Android_Booting "http://eLinux.org/Android_Booting")

# Android Booting

The bootup of an Android system consists of several phases, which are outlined here.

## Contents

* 1 Key bootup components
  * 1.1 Bootloader
  * 1.2 `init`
    * 1.2.1 `init` resources
* 2 Sequence of boot steps on ADP1
  * 2.1 firmware
  * 2.2 kernel
  * 2.3 user space
* 3 Tools for analyzing Android Bootup
* 4 Notes on the Android startup procedure
  * 4.1 Overview
  * 4.2 `strace`
  * 4.3 Interaction of different processes on application initialization
  * 4.4 Improving Bootup Time presentation
* 5 News
  * 5.1 1-second boot of Android

## Key bootup components

### Bootloader

The first program which runs on any Android system is the bootloader. Technically, the bootloader is outside the realm of Android itself, and is used to do very low-level system initialization, before loading the Linux kernel. The kernel then does the bulk of hardware, driver and file system initialization, before starting up the user-space programs and applications that make up Android.

Often, the first-stage bootloader will provide support for loading recovery images to the system flash, or performing other recovery, update, or debugging tasks.

The bootloader on the ADP1 detects certain keypresses, which can be used to make it load a `recovery` image (second instance of the kernel and system), or put the phone into a mode where the developer can perform development tasks (`fastboot` mode), such as re-writing flash images, directly downloading and executing an alternate kernel image, etc.

### `init`

A key component of the Android bootup sequence is the program `init`, which is a specialized program for initializing elements of the Android system. Unlike other Linux systems (embedded or otherwise), Android uses its own initialization program. (Linux desktop systems have historically used some combination of `/etc/inittab` and sysV init levels - e.g. `/etc/rc.d/init.d` with symlinks in `/etc/rc.d/rc.[2345]`). Some embedded Linux systems use simplified forms of these -- such as the init program included in busybox, which processes a limited form of `/etc/inittab`, or a direct invocation of a shell script or small program to do fixed initialization steps.

The Android `init` program processes two files, executing the commands it finds in them, called `init.rc` and `init.<machine_name>.rc`, where `<machine_name>` is the name of the hardware that Android is running on. (Usually, this is a code word. The name of the HTC1 hardware for the ADP1 is `trout`, and the name of the emulator is `goldfish`.)

The `init.rc` file is intended to provide the generic initialization instructions, while the `init.<machine_name>.rc` file is intended to provide the machine-specific initialization instructions.

#### `init` resources

The syntax for these `.rc` files is documented in a readme file in the source tree. See the [Android init language reference](https://android.googlesource.com/platform/system/core/+/master/init/readme.txt)

Or, see also: [kandroid copy of old Android PDK](http://www.kandroid.org/online-pdk/guide/bring_up.html)

* Note that the old PDK has been retracted from where it used to found below [`source.android.com/porting`](http://source.android.com/porting)
  * You may be able to reconstruct it though:
    * You need a local copy of the AOSP sourcetree, and run the usual `build/envsetup.sh` preparation
    * Use `repo init -b` to check out the AOSP sourcetree with a tag around 2.3, then `make sdk sdk_all`
    * This worked for me, though I used some tag around 4.0.4. Some links had to be fixed in the resulting html output

See also [`www.androidenea.com/2009/08/init-process-and-initrc.html`](http://www.androidenea.com/2009/08/init-process-and-initrc.html)

## Sequence of boot steps on ADP1

### firmware

* first-stage bootloader runs
  * it detects if a special key is held, and can launch the recovery image, or the `fastboot` bootloader
* eventually, a kernel is loaded into RAM (usually with an initrd)
  * normally, this will be the kernel from the `boot` flash partition.

### kernel

* the kernel boots
  * core kernel initialization
    * memory and I/O areas are initialized
    * interrupts are started, and the process table is initialized
  * driver initialization
  * kernel daemons (threads) are started
  * root file system is mounted
  * the first user-space process is started
    * usually `/init` (note that other Linux systems usually start `/sbin/init`)

### user space

* the kernel runs `/init`
  * `/init` processes `/init.rc` and `/init.<machine_name>.rc`
  * dalvik VM is started (`zygote`). See [Android Zygote Startup](http://eLinux.org/Android_Zygote_Startup "Android Zygote Startup")
  * several daemons are started:
    * `rild` - radio interface link daemon
    * `vold` - volume daemon (media volumes, as in file systems - nothing to do with audio volume)
* the `system_server` starts, and initializes several core services
  * See [`www.androidenea.com/2009/07/system-server-in-android.html`](http://www.androidenea.com/2009/07/system-server-in-android.html)
  * initialization is done in 2 steps:
    * 1) a library is loaded to initialize interfaces to native services, then



2. Java-based core services are initialized in `ServerThread::run()` in [SystemServer.java](http://android.git.kernel.org/?p=platform/frameworks/base.git;a=blob;f=services/java/com/android/server/SystemServer.java).

- The activity manager starts core applications, which are themselves Dalvik applications:
  - `com.android.phone` — phone application
  - `android.process.acore` — home (desktop) and a few core apps

- Other processes are also started by `/init`, somewhere in there:
  - `adb`
  - `mediaserver`
  - `dbus-daemon`
  - `akmd`

## Tools for Analyzing Android Bootup

- `logcat` — see Android Logging System
  - Try this command:

```bash
adb logcat -d -b events | grep "boot"
```

```text
01-01 00:00:08.396 I/boot_progress_start(  754): 12559
01-01 00:00:13.716 I/boot_progress_preload_start(  754): 17879
01-01 00:00:24.380 I/boot_progress_preload_end(  754): 28546
01-01 00:00:25.068 I/boot_progress_system_run(  768): 29230
01-01 00:00:25.536 I/boot_progress_pms_start(  768): 29697
01-01 00:00:25.958 I/boot_progress_pms_system_scan_start(  768): 30117
01-01 00:00:40.005 I/boot_progress_pms_data_scan_start(  768): 44171
01-01 00:00:45.841 I/boot_progress_pms_scan_end(  768): 50006
01-01 00:00:46.341 I/boot_progress_pms_ready(  768): 50505
01-01 00:00:49.005 I/boot_progress_ams_ready(  768): 53166
01-01 00:00:52.630 I/boot_progress_enable_screen(  768): 56793
```

- Or this:

```bash
adb logcat -d | grep preload
```

```text
10-15 00:00:17.748 I/Zygote  (  535): ...preloaded 1873 classes in 2438ms.
10-15 00:00:17.764 I/Zygote  (  535): ...preloaded 0 resources in 0ms.
10-15 00:00:17.772 I/Zygote  (  535): ...preloaded 15 resources in 7ms.
```

- [Bootchart](http://eLinux.org/Using_Bootchart_on_Android "Using Bootchart on Android") — see Using Bootchart on Android.
- `strace` is pretty handy also, to see the timings for system calls from a process as it runs.
  - You can use `strace` as a wrapper for a program in `init.rc`, and save the results to a file.
  - Use `-f` to follow subprocesses.
  - Use `-tt` to get detailed timestamps for syscalls.
  - Use `-o` to output the data to a file.

Here is an example of using `strace` to follow the startup of zygote and the apps that are forked from it.

Replace:

```text
service zygote /system/bin/app_process -Xzygote /system/bin --zygote --start-system-server
```

with:

```text
service zygote /system/xbin/strace -f -tt -o /cache/debug/boot.strace /system/bin/app_process -Xzygote /system/bin --zygote --start-system-server
```

Here is some sample data:

```text
$ head boot.strace
571   00:00:11.389939 execve("/system/bin/app_process", ["/system/bin/app_process", "-Xzygote", "/system/bin", "--zygote", "--start-system-server"], [/* 15 vars */]) = 0
571   00:00:11.658878 brk(0)            = 0x804b000
571   00:00:11.659048 mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x77f9a000
571   00:00:11.659169 readlink("/proc/self/exe", "/system/bin/app_process", 4096) = 23
571   00:00:11.659339 access("/etc/ld.so.preload", R_OK) = 0
571   00:00:11.659440 open("/etc/ld.so.preload", O_RDONLY) = 3
571   00:00:11.659548 fstat64(0x3, 0x7fa76650) = 0
571   00:00:11.659887 mmap2(NULL, 36, PROT_READ|PROT_WRITE, MAP_PRIVATE, 3, 0) = 0x77f99000
571   00:00:11.659970 close(3)          = 0
571   00:00:11.660071 open("/lib/libc_sse.so", O_RDONLY) = 3
```

Please note that writing the `strace` data takes extra time. For long sequences of very fast syscalls, such as when the timezone file is being read, the overhead of `strace` itself exaggerates the timings in the trace. Use the timing information with caution.

## Notes on the Android Startup Procedure

### Overview

See "Android Initialization Process" at [`blog.chinaunix.net/u2/85805/showart_1421736.html`](http://blog.chinaunix.net/u2/85805/showart_1421736.html) (this address is not working), using [`blog.chinaunix.net/space.php?uid=7788581&do=blog&id=2558375`](http://blog.chinaunix.net/space.php?uid=7788581&do=blog&id=2558375) instead.

### `strace`

[`benno.id.au/blog/2007/11/18/android-runtime-strace`](http://benno.id.au/blog/2007/11/18/android-runtime-strace)

### Interaction of Different Processes on Application Initialization

Talking about Android Process — [`blog.csdn.net/mawl2002/archive/2009/06/24/4295905.aspx`](http://blog.csdn.net/mawl2002/archive/2009/06/24/4295905.aspx)

### Improving Bootup Time Presentation

See [Improving Android Boot Time](http://eLinux.org/Improving_Android_Boot_Time "Improving Android Boot Time") — notes and material for a talk at LinuxCon North America, 2010, by Tim Bird.

## News

### 1-Second Boot of Android

Ubiquitous Corporation has announced boot of an ARM-based Android system in 1 second. Actually, it's more like a suspend and resume than a boot. See [`www.linuxfordevices.com/c/a/News/Ubiquitous-QuickBoot/?kc=LNXDEVNL032410`](http://www.linuxfordevices.com/c/a/News/Ubiquitous-QuickBoot/?kc=LNXDEVNL032410) [March, 2010].

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Power Management

> From: [eLinux.org](http://eLinux.org/Android_Power_Management "http://eLinux.org/Android_Power_Management")

# Android Power Management

Notes on Power Management in Android.

## Contents

- 1. Wakelocks
  - 1.1. Creating a wakelock
  - 1.2. Using a wakelock inside the kernel
  - 1.3. Using a wakelock from user space
  - 1.4. Sample `cat /proc/wakelocks` output
- 2. Patch submission controversy
- 3. Wakelock documentation (from patch)
- 4. Motorola quickwakeup feature
- 5. Earlysuspend
- 6. May 2010 patch submission — "Suspend blockers"

## Wakelocks

The first version of Android utilized a system called "wakelocks", which was a set of patches to the Linux kernel to allow a caller to prevent the system from going to low power state.

Each wakelock is defined with a name and type. The type is one of:

- `WAKE_LOCK_IDLE`
- `WAKE_LOCK_SUSPEND`

The name is an arbitrary ASCII string.

When a wake lock of type "IDLE" is in effect, the system will not enter idle (low power) state, and this should make the device more responsive. That is, it does not have to wake up from idle to respond to interrupts or events. When a wake lock of type "SUSPEND" is held, then the system will not suspend, which takes even longer to resume from.

You can, from user space, see the currently defined wakelocks and a bunch of information about their status, using `cat /proc/wakelocks`.

Below is an example of output from that command.

To see the code for this, see the file:

```text
drivers/android/power.c
```

NOTE: See the [Discussion](http://eLinux.org/Talk:Android_Power_Management "Talk:Android Power Management") page for a note on this file.

### Creating a Wakelock

Kernel code can define a wakelock, and get a handle to it, by calling:

```c
#include <linux/wakelock.h>
wake_lock_init(struct wakelock *lock, int type, const char *name);
```

From user space, a process can write a name to:

```text
/sys/power/wake_lock
```

to create and lock a suspend lock with that name.

### Using a Wakelock Inside the Kernel

Kernel code can acquire and release the lock with one of the following:

```c
void wake_lock(struct wake_lock *lock);
void wake_unlock(struct wake_lock *lock);
```

Kernel code can also set a timeout to specify automatic release of the wakelock after a specific period, with:

```c
void wake_lock_timeout(struct wake_lock *lock, long timeout);
```

The wakelock does not need to be held prior to calling this; it will automatically lock the wakelock and register the timeout.

### Using a Wakelock from User Space

To release a suspend wake lock from user space, a process can write the lock name to:

```text
/sys/power/wake_unlock
```

### Sample `cat /proc/wakelocks` Output

Here are some wakelocks from my ADP1 phone, running Donut (I think):

*Note: I widened the columns and adjusted the title row to make the columns line up better.*



```text
$ cat /proc/wakelocks
name                    count   expire_count  active_since
                                        wake_count          total_time      sleep_time      max_time        last_change
"PowerManagerService"   3580    0       0     0             1706674438454   1354421173104   62626251221     31701936996687
"mddi_link_active_idle_lock" 4641 0     0     0             26749877925     0               253234863       31701903732527
"msmfb_idle_lock"       2549    0       0     0             28889923076     0               266601563       31701902633894
"SMD_RPCCALL"           8913    0       34    0             9038391159      6843658471      176025391       31690316543807
"audio_pcm_idle"        12      0       0     0             68230224609     0               27459259033     31690315567244
"audio_pcm"             12      0       0     0             68230285646     12423248292     27459289551     31690315567244
"rpc_read"              60      0       0     0             3112792         823974          91553           31690315048445
"adsp"                  12      0       0     0             67035552978     11988464355     27387664794     31690282791365
"rpc_read"              12      0       0     0             671387          213624          91553           31686582229842
"usb_mass_storage"      0       0       0     0             0               0               0               0
"rpc_read"              137     0       0     0             8972160         6744383         122070          31685788467635
"rpc_server"            277     0       0     0             406372060       320922839       41412354        31685787887801
"rpc_read"              277     0       0     0             117919940       111480725       94848633        31685787826766
"alarm"                 1220    0       0     0             27851074219     25716247547     382141114       31669270950545
"rpc_read"              4909    0       0     0             375915506       347930899       16021729        31376427078475
"gpio_input"            0       0       0     0             0               0               0               0
"mddi_idle_lock"        54      0       0     0             8752532958      0               249603271       31154190719832
"SMD_DATA5"             862     862     377   0             620518382572    567607416986    6926910400      31153421737899
"alarm_rtc"             177     10      0     0             47826019299     47825439463     1801544190      31152471695175
"KeyEvents"             13271   0       0     0             11482665934     343322752       503204346       30525886245957
"evdev"                 4437    0       0     0             4980529833      98724365        506927490       30525884811631
"evdev"                 188     0       6     0             3093719493      2680358890      393676758       30522918777697
"rpc_read"              18      0       0     0             1464840         0               335693          30520425552599
"gpio_kp"               68      0       14    0             14835723878     2092010498      933135987       30445059005968
"evdev"                 52      0       0     0             98999026        0               24139405        30438128067247
"rpc_read"              596     0       0     0             745910654       211212166       491180420       30046209060900
"rpc_read"              1331    0       0     0             286651593       169342025       112518310       30046203598253
"rpc_read"              10      0       0     0             1495361         427247          274658          3596980453801
"qmi0"                  2       2       0     0             996235351       0               501717529       173250290527
"qmi2"                  1       1       0     0             490385742       0               490385742       173250290527
"qmi1"                  1       1       0     0             493193359       0               493193359       173250290527
"evdev"                 0       0       0     0             0               0               0               0
"evdev"                 0       0       0     0             0               0               0               0
"rpc_read"              2       0       0     0             427247          0               274659          7461350097
"mt9t013"               0       0       0     0             0               0               0               0
"gpio_input"            0       0       0     0             0               0               0               0
"gpio_input"            0       0       0     0             0               0               0               0
"SMD_DATA7"             0       0       0     0             0               0               0               0
"SMD_DATA6"             0       0       0     0             0               0               0               0
"msm_serial_hs_rx"      0       0       0     0             0               0               0               0
"unknown_wakeups"       0       0       0     0             0               0               0               0
"deleted_wake_locks"    36      0       0     0             2593991         518798          1068114         0
"radio-interface"       329     0       0     549499512     437556091307    299558441157    2895507812      31701540695418
"vbus_present"          3       2       0     16399444580   26400295008545  25248585083008  25852771240234  31685690780867
"main"                  27      0       0     547991455078  4674244259033   0               627599700928    31154098800887
"mmc_delayed_work"      796     796     172   0             405246968975    396150246568    689067383       31153556991805
"SMD_DS"                682     681     192   558929443     486005943591    268692961407    2368892822      31701531357039
```

## Patch submission controversy

Arve Hjønnevå (of Google) sent patches to the linux-pm mailing list in of 2009, but they were rejected. See [this thread](https://lists.linux-foundation.org/pipermail/linux-pm/2009-February/019750.html) for the submission and resulting discussion. This was the third version of the patches submitted for review by the kernel community.

The reasons for the rejection are described in the LWN.NET article [Wakelocks and the embedded problem](http://lwn.net/Articles/318611/).

## Wakelock documentation (from patch)

The 3rd version of the wakelock patch included the following `/Documentation/power/wakelock.txt` file.



# Wakelocks

A locked wakelock, depending on its type, prevents the system from entering suspend or other low-power states. When creating a wakelock, you can select if it prevents suspend or low-power idle states. If the type is set to `WAKE_LOCK_SUSPEND`, the wakelock prevents a full system suspend. If the type is `WAKE_LOCK_IDLE`, low-power states that cause large interrupt latencies, or that disable a set of interrupts, will not be entered from idle until the wakelocks are released. Unless the type is specified, this document refers to wakelocks with the type set to `WAKE_LOCK_SUSPEND`.

If the suspend operation has already started when locking a wakelock, it will abort the suspend operation as long it has not already reached the `suspend_late` stage. This means that locking a wakelock from an interrupt handler or a freezeable thread always works, but if you lock a wakelock from a `suspend_late` handler you must also return an error from that handler to abort suspend.

Wakelocks can be used to allow user-space to decide which keys should wake the full system up and turn the screen on. Use `set_irq_wake` or a platform specific api to make sure the keypad interrupt wakes up the cpu. Once the keypad driver has resumed, the sequence of events can look like this:

- The Keypad driver gets an interrupt. It then locks the `keypad-scan` wakelock and starts scanning the keypad matrix.
- The `keypad-scan` code detects a key change and reports it to the `input-event` driver.
- The `input-event` driver sees the key change, enqueues an event, and locks the `input-event-queue` wakelock.
- The `keypad-scan` code detects that no keys are held and unlocks the `keypad-scan` wakelock.
- The user-space `input-event` thread returns from `select`/`poll`, locks the `process-input-events` wakelock and then calls `read` in the `input-event` device.
- The `input-event` driver dequeues the key-event and, since the queue is now empty, it unlocks the `input-event-queue` wakelock.
- The user-space `input-event` thread returns from `read`. It determines that the key should not wake up the full system, releases the `process-input-events` wakelock and calls `select` or `poll`.

```
                 Key pressed   Key released
                     |             |
keypad-scan          ++++++++++++++++++
input-event-queue        +++          +++
process-input-events       +++          +++
```

## Driver API

A driver can use the wakelock api by adding a wakelock variable to its state and calling `wake_lock_init`. For instance:

```
struct state {
    struct wakelock wakelock;
}

init() {
    wake_lock_init(&state->wakelock, WAKE_LOCK_SUSPEND, "wakelockname");
}
```

Before freeing the memory, `wake_lock_destroy` must be called:

```
uninit() {
    wake_lock_destroy(&state->wakelock);
}
```

When the driver determines that it needs to run (usually in an interrupt handler) it calls `wake_lock`:

```
wake_lock(&state->wakelock);
```

When it no longer needs to run it calls `wake_unlock`:

```
wake_unlock(&state->wakelock);
```

It can also call `wake_lock_timeout` to release the wakelock after a delay:

```
wake_lock_timeout(&state->wakelock, HZ);
```

This works whether the wakelock is already held or not. It is useful if the driver woke up other parts of the system that do not use wakelocks but till need to run. Avoid this when possible, since it will waste power if the timeout is long or may fail to finish needed work if the timeout is short.

## Motorola quickwakeup feature

Jocelyn Falempe of Motorola proposed (in November, 2009) a quickwakeup feature to make it possible to reduce the time for a periodic job to resume, do a small amount of work, and suspend again.

[`patchwork.kernel.org/patch/58064/`](http://patchwork.kernel.org/patch/58064/)

From the patch:

```
The purpose of this feature is to drastically reduce the suspend/resume
time for device driver which needs to do periodic job.
In our use case (android smartphone), the system is most of the time in
suspend to RAM, and needs to send a low level command every 30s. With
current framework it takes about 500ms on omap3430 to resume the full
system, and then suspend again. With quickwakup feature, in the resume
process after resuming sysdev and re-enabling irq, the driver handler is
executed, and then it suspends again.
This new path takes 20ms for us, which leads to good power-saving. 
```

## Earlysuspend

Arve's patches also included something referred to as "earlysuspend", but I haven't reviewed this yet to see what it is.

## May 2010 patch submission - "Suspend blockers"

Arve refactored the patches and did a name change, and submitted them again in April and May of 2010. There was a LOT of discussion on the `linux-pm` mailing list, which many developers participated in. The discussion raised lots of questions, and lots of responses were given. People interested in Android power management may get more enlightenment by reading the thread.

[`groups.google.com/group/linux.kernel/browse_frm/thread/b6fed7e38365c259/c92d8b4a41f87902?hl=en&tvc=1&q=linux.kernel+suspend+block+api+(version+6)#c92d8b4a41f87902`](http://groups.google.com/group/linux.kernel/browse_frm/thread/b6fed7e38365c259/c92d8b4a41f87902?hl=en&tvc=1&q=linux.kernel+suspend+block+api+(version+6)#c92d8b4a41f87902)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Security

> From: [eLinux.org](http://eLinux.org/Android_Security "http://eLinux.org/Android_Security")

# Android Security

## Contents

- 1 Overview
- 2 Kernel-level security
  - 2.1 Users and groups
    - 2.1.1 Sample File Permissions
    - 2.1.2 Sample Process List
  - 2.2 Paranoid network-ing
- 3 Application-level security
- 4 Tutorial
- 5 Security Analysis
- 6 Security Investigations
  - 6.1 TOMOYO Linux investigation
    - 6.1.1 Presentation
    - 6.1.2 Code
    - 6.1.3 Contact
- 7 Security Tricks
  - 7.1 Changing application security permissions after installation

## Overview

The overall architecture of Android security is described at: [`developer.android.com/guide/topics/security/security.html`](http://developer.android.com/guide/topics/security/security.html)

Each application is given its own Linux user id (UID) and group ID

## Kernel-level security

### Users and groups

Each application is assigned a uid and gid at install time. Application data files are stored in `/data/data/\<app-nameu0005c class="calibre16">/...`, and are read-writable only by that application process.

#### Sample File Permissions

Here is an example from my ADP1 phone (lots of lines omitted to reduce noise):

(Oh, and yes, I'm using busybox - `find`, `xargs`, and `sort` are not available otherwise)



```
# find /data/data -type f | xargs ls -l | sort -k3 -n
-rw-------    1 1000     1000         1954 Nov 12 01:10 /data/data/com.android.providers.subscribedfeeds/files/sslcache/android.clients.google.com.443
-rw-r--r--    1 1000     1000       147608 Apr  6  2009 /data/data/com.google.tts/lib/libspeechsynthesis.so
-rw-rw----    1 1000     1000           65 Nov  5 02:01 /data/data/com.google.android.systemupdater/shared_prefs/system_update_helper.xml
-rw-rw----    1 1000     1000          679 Nov 11 23:18 /data/data/com.android.settings/shared_prefs/com.android.settings_preferences.xml
-rw-rw----    1 1000     1000         2000 May 14 20:07 /data/data/com.google.android.location/files/DATA_Preferences
-rw-rw----    1 1000     1000         6144 Dec 19  2008 /data/data/com.android.settings/databases/webviewCache.db
-rw-rw----    1 1000     1000        11264 Nov 12 01:10 /data/data/com.android.providers.subscribedfeeds/databases/subscribedfeeds.db
-rw-rw----    1 1000     1000        14336 Dec 19  2008 /data/data/com.android.settings/databases/webview.db
-rw-rw----    1 1000     1000        36864 Nov 12 18:23 /data/data/com.android.providers.settings/databases/settings.db
-rw-rw----    1 1000     1000       129024 Nov 12 18:45 /data/data/com.google.android.server.checkin/databases/checkin.db
-rw-rw-r--    1 1000     1000          120 Nov 12 01:09 /data/data/com.android.providers.subscribedfeeds/shared_prefs/subscribedFeeds.xml
-rwxrwx---    1 1000     1000        54052 Dec 20  2008 /data/data/com.android.settings/files/wallpaper
-rw-------    1 1001     1001            4 Oct 31 21:09 /data/data/com.android.providers.telephony/app_parts/PART_1257023388570
-rw-------    1 1001     1001            4 Oct 31 21:10 /data/data/com.android.providers.telephony/app_parts/PART_1257023445796

...
-rw-rw----    1 1001     1001          103 May 13  2009 /data/data/com.android.providers.telephony/shared_prefs/preferred-apn.xml
-rw-rw----    1 1001     1001          122 Oct 28 17:37 /data/data/com.android.phone/shared_prefs/com.android.phone_preferences.xml
-rw-rw----    1 1001     1001          126 Sep  3  2008 /data/data/com.android.phone/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 1001     1001         7168 Nov  5 02:01 /data/data/com.android.providers.telephony/databases/telephony.db
-rw-rw----    1 1001     1001        69632 Nov  6 01:58 /data/data/com.android.providers.telephony/databases/mmssms.db
-rw-rw----    1 10000    10000         114 Apr 20  2009 /data/data/com.android.alarmclock/shared_prefs/AlarmClock.xml
-rw-rw----    1 10000    10000        4096 Dec 19  2008 /data/data/com.android.alarmclock/databases/alarms.db
-rw-rw----    1 10001    10001        7168 Nov 12 18:43 /data/data/org.koxx.forecast_weather.v2/databases/forecasts.db
-rw-rw----    1 10002    10002         489 Nov 11 23:19 /data/data/com.android.calculator2/files/calculator.data
-rw-rw----    1 10003    10003         683 Jun 10 19:27 /data/data/com.android.camera/shared_prefs/com.android.camera_preferences.xml
-rw-rw----    1 10003    10003        5120 Dec 20  2008 /data/data/com.android.providers.drm/databases/drm.db
-rw-rw----    1 10003    10003       10240 Nov  1 16:24 /data/data/com.android.providers.downloads/databases/downloads.db
-rw-rw----    1 10003    10003       37888 May 13  2009 /data/data/com.android.providers.media/databases/internal.db
-rw-rw----    1 10003    10003       37888 Sep  4 23:25 /data/data/com.android.camera/databases/launcher.db
-rw-rw----    1 10003    10003       60416 Nov 12 19:01 /data/data/com.android.providers.media/databases/external-39636438.db
-rw-r--r--    1 10004    10004           0 Jun 12 01:13 /data/data/com.android.providers.im/databases/im.db-mj76B91FF8
-rw-r--r--    1 10004    10004           0 Jun 12 04:05 /data/data/com.android.providers.im/databases/im.db-mj0AB1E39C
...
-rw-rw----    1 10004    10004         105 Dec 18  2008 /data/data/com.android.providers.contacts/shared_prefs/owner-info.xml
-rw-rw----    1 10004    10004         125 Nov 11 16:37 /data/data/com.android.contacts/shared_prefs/dialtacts.xml
-rw-rw----    1 10004    10004         126 Dec 19  2008 /data/data/com.android.contacts/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 10004    10004         146 Aug 28 16:02 /data/data/com.android.contacts/shared_prefs/com.android.contacts_preferences.xml
-rw-rw----    1 10004    10004         169 Nov  5 02:01 /data/data/com.android.launcher/shared_prefs/launcher.xml
-rw-rw----    1 10004    10004        4096 Jan 30  2009 /data/data/com.android.providers.userdictionary/databases/user_dict.db
-rw-rw----    1 10004    10004       20480 Oct 31 21:12 /data/data/com.android.launcher/databases/launcher.db
-rw-rw----    1 10004    10004       21504 Nov 12 18:45 /data/data/com.android.providers.im/databases/im.db
-rw-rw----    1 10004    10004      110592 Nov 12 02:08 /data/data/com.android.providers.contacts/databases/contacts.db
-rw-------    1 10005    10005         270 Jun 13 03:36 /data/data/com.android.email/databases/0c180cf8-fb7b-4d3e-b994-4282611af63a.db_att/32
-rw-r--r--    1 10005    10005     1418240 Nov  5 02:01 /data/data/com.android.email/databases/0c180cf8-fb7b-4d3e-b994-4282611af63a.db
-rw-rw----    1 10005    10005        1866 Dec 20  2008 /data/data/com.android.email/shared_prefs/AndroidMail.Main.xml
-rw-rw----    1 10005    10005        6144 Sep  8 01:35 /data/data/com.android.email/databases/webviewCache.db
-rw-rw----    1 10005    10005       14336 May 14 17:58 /data/data/com.android.email/databases/webview.db
-rw-rw----    1 10006    10006         126 Dec 18  2008 /data/data/com.google.android.gm/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 10006    10006         199 Jan 22  2009 /data/data/com.google.android.gm/shared_prefs/Gmail.xml
-rw-rw----    1 10006    10006        6144 Dec 19  2008 /data/data/com.google.android.gm/databases/gmail.db
-rw-rw----    1 10006    10006        6144 Dec 23  2008 /data/data/com.google.android.gm/databases/webviewCache.db
-rw-rw----    1 10006    10006       14336 Dec 23  2008 /data/data/com.google.android.gm/databases/webview.db
-rw-------    1 10007    10007        1888 Nov 12 17:09 /data/data/com.google.android.apps.gtalkservice/files/sslcache/mtalk.google.com.5228
-rw-------    1 10007    10007        1954 Nov 12 18:43 /data/data/com.google.android.providers.gmail/files/sslcache/android.clients.google.com.443
-rw-rw----    1 10007    10007        6144 Oct 23 22:43 /data/data/com.google.android.googleapps/databases/webviewCache.db
-rw-rw----    1 10007    10007        7168 May 13  2009 /data/data/com.google.android.providers.settings/databases/googlesettings.db
-rw-rw----    1 10007    10007       13312 Nov 11 20:37 /data/data/com.google.android.googleapps/databases/accounts.db
-rw-rw----    1 10007    10007       14336 May 13  2009 /data/data/com.google.android.googleapps/databases/webview.db
-rw-rw----    1 10007    10007      502784 Nov 12 18:45 /data/data/com.google.android.providers.gmail/databases/mailstore.tbird20d@gmail.com.db
-rw-rw----    1 10009    10009         126 Sep  3  2008 /data/data/com.android.mms/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 10009    10009         585 Sep  3  2008 /data/data/com.android.mms/shared_prefs/com.android.mms_preferences.xml
-rw-rw-rw-    1 10010    10010         310 Sep 18 01:12 /data/data/com.android.music/shared_prefs/Music.xml
-rw-rw----    1 10015    10015         126 Apr 29  2009 /data/data/com.google.android.street/shared_prefs/com.google.android.street.StreetView.xml
-rw-------    1 10017    10017          35 Nov 12 16:49 /data/data/com.android.browser/cache/webviewCache/c24b0576
-rw-------    1 10017    10017          43 Nov 12 16:47 /data/data/com.android.browser/cache/webviewCache/5446c8f2
...
-rw-------    1 10017    10017     1204872 May 13  2009 /data/data/com.android.browser/app_plugins/gears.so
-rw-r--r--    1 10017    10017         512 Nov 12 19:18 /data/data/com.android.browser/databases/webviewCache.db-journal
-rw-r--r--    1 10017    10017        8192 May 14 19:15 /data/data/com.android.browser/gears/geolocation.db
-rw-r--r--    1 10017    10017       18432 Dec 19  2008 /data/data/com.android.browser/gears/localserver.db
-rw-r--r--    1 10017    10017       20480 Dec 19  2008 /data/data/com.android.browser/gears/permissions.db
-rw-r--r--    1 10017    10017       48128 Nov 12 19:01 /data/data/com.android.browser/app_icons/WebpageIcons.db
-rw-rw----    1 10017    10017         851 May 29 13:53 /data/data/com.android.browser/shared_prefs/com.android.browser_preferences.xml
-rw-rw----    1 10017    10017       32768 Nov 12 16:49 /data/data/com.android.browser/databases/webviewCache.db
-rw-rw----    1 10017    10017       68608 Nov 12 16:49 /data/data/com.android.browser/databases/browser.db
-rw-rw----    1 10017    10017      257024 Nov 12 17:09 /data/data/com.android.browser/databases/webview.db
-rw-rw-rw-    1 10017    10017           0 Nov 12 16:48 /data/data/com.android.browser/app_plugins/gears-0.5.17.0/gearstimestamp
-rw-rw----    1 10018    10018         126 Sep  3  2008 /data/data/com.android.calendar/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 10018    10018         539 Nov 11 23:19 /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml
-rw-rw----    1 10018    10018      375808 Nov 12 09:58 /data/data/com.android.providers.calendar/databases/calendar.db
-rw-rw----    1 10019    10019          48 Nov  7 06:11 /data/data/com.google.android.apps.maps/files/DATA_Tiles
-rw-rw----    1 10019    10019         483 Nov 11 03:58 /data/data/com.google.android.apps.maps/shared_prefs/com.google.android.maps.MapsActivity.xml
-rw-rw----    1 10019    10019         708 Nov 12 17:09 /data/data/com.google.android.apps.maps/shared_prefs/friend_finder.xml
-rw-rw----    1 10019    10019        2000 Nov 11 03:58 /data/data/com.google.android.apps.maps/files/DATA_Preferences
-rw-rw----    1 10019    10019        6144 May 13  2009 /data/data/com.google.android.apps.maps/databases/webviewCache.db
-rw-rw----    1 10019    10019        6144 Nov  1 21:28 /data/data/com.google.android.apps.maps/databases/search_history.db
-rw-rw----    1 10019    10019        8192 Nov 11 03:52 /data/data/com.google.android.apps.maps/databases/friends.db
-rw-rw----    1 10019    10019       14336 May 13  2009 /data/data/com.google.android.apps.maps/databases/webview.db
-rw-rw----    1 10019    10019       16048 Nov  7 06:11 /data/data/com.google.android.apps.maps/files/DATA_Tiles_1
-rw-rw-rw-    1 10019    10019          65 Nov 11 03:52 /data/data/com.google.android.apps.maps/shared_prefs/extra-features.xml
-rw-rw----    1 10021    10021         435 Oct 30 17:09 /data/data/com.android.vending/shared_prefs/vending_preferences.xml
-rw-rw----    1 10021    10021        5120 Oct  6 19:38 /data/data/com.android.vending/databases/suggestions.db
-rw-rw----    1 10021    10021        6144 May 14 17:17 /data/data/com.android.vending/databases/webviewCache.db
-rw-rw----    1 10021    10021       14336 May 14 17:21 /data/data/com.android.vending/databases/webview.db
-rw-rw----    1 10021    10021       17408 Oct  6 19:39 /data/data/com.android.vending/databases/assets.db
-rw-------    1 10022    10022       50077 Nov 12 05:34 /data/data/com.google.android.youtube/cache/videos?vq=peter+sellers+inspector&format=2&restriction=us&start-index=18&max-results=8
-rw-------    1 10022    10022       53110 Nov 12 05:33 /data/data/com.google.android.youtube/cache/videos?vq=peter+sellers+inspector&format=2&restriction=us&start-index=10&max-results=8
-rw-------    1 10022    10022       57403 Nov 12 05:33 /data/data/com.google.android.youtube/cache/videos?vq=peter+sellers+inspector&format=2&restriction=us&start-index=1&max-results=9
-rw-------    1 10022    10022       63761 Nov 12 05:32 /data/data/com.google.android.youtube/cache/recently_featured?format=2&start-index=1&max-results=9
-rw-rw----    1 10022    10022         739 Nov 12 16:45 /data/data/com.google.android.youtube/shared_prefs/youtube.xml
-rw-rw----    1 10022    10022        5120 Nov 12 05:34 /data/data/com.google.android.youtube/databases/suggestions.db
-rw-rw----    1 10025    10025         114 May 13  2009 /data/data/com.google.android.voicesearch/shared_prefs/com.google.android.voicesearch_preferences.xml
-rw-rw----    1 10025    10025         126 May 13  2009 /data/data/com.google.android.voicesearch/shared_prefs/_has_set_default_values.xml
-rw-rw----    1 10025    10025        2000 May 13  2009 /data/data/com.google.android.voicesearch/files/DATA_Preferences
-rw-rw----    1 10025    10025        8192 Jun 10 03:25 /data/data/com.google.android.voicesearch/databases/webviewCache.db
-rw-rw----    1 10025    10025       14336 May 13  2009 /data/data/com.google.android.voicesearch/databases/webview.db
-rw-rw----    1 10026    10026         688 Jan 10  2009 /data/data/com.quirkconsulting/shared_prefs/TouchTipv2.xml
-rw-rw----    1 10026    10026        6144 Dec 19  2008 /data/data/com.quirkconsulting/databases/webviewCache.db
-rw-rw----    1 10026    10026       14336 Dec 19  2008 /data/data/com.quirkconsulting/databases/webview.db
-rw-------    1 10027    10027        4326 Aug  8 01:03 /data/data/com.a0soft.gphone.aCurrency/app_db/currency.db
-rw-rw----    1 10027    10027         170 Aug  8 01:04 /data/data/com.a0soft.gphone.aCurrency/shared_prefs/com.a0soft.gphone.aCurrency_preferences.xml
-rw-rw----    1 10027    10027         740 Dec 20  2008 /data/data/com.a0soft.gphone.aCurrency/shared_prefs/pref2.xml
-rw-rw----    1 10027    10027         801 Aug  8 01:05 /data/data/com.a0soft.gphone.aCurrency/shared_prefs/pref3.xml
-rw-rw----    1 10027    10027        6144 Aug  8 01:03 /data/data/com.a0soft.gphone.aCurrency/databases/webviewCache.db
-rw-rw----    1 10027    10027       14336 Aug  8 01:03 /data/data/com.a0soft.gphone.aCurrency/databases/webview.db
-rw-rw----    1 10028    10028       14336 Sep 19 22:17 /data/data/com.stylem.movies/databases/webview.db
-rw-rw----    1 10028    10028       53248 Sep 19 22:18 /data/data/com.stylem.movies/databases/webviewCache.db
-rw-rw----    1 10029    10029         241 Jan 10  2009 /data/data/com.capaci.android.flashlight/shared_prefs/SettingsFile.xml
-rw-rw----    1 10030    10030         233 Jun 15 15:02 /data/data/com.weather.Weather/files/tile-Radar-023010230-200906151450-twc.png
-rw-rw----    1 10030    10030         233 Jun 15 15:02 /data/data/com.weather.Weather/files/tile-Radar-023010231-200906151450-twc.png
-rw-rw----    1 10030    10030         233 Jun 15 15:02 /data/data/com.weather.Weather/files/tile-Radar-023010232-200906151450-twc.png
-rw-rw----    1 10030    10030         233 Mar 18  2009 /data/data/com.weather.Weather/files/tile-Radar-023010221-200903181940-twc.png
-rw-rw----    1 10030    10030         233 Mar 18  2009 /data/data/com.weather.Weather/files/tile-Radar-023010223-200903181940-twc.png
-rw-rw----    1 10030    10030         233 Mar 18  2009 /data/data/com.weather.Weather/files/tile-Radar-023010230-200903181940-twc.png
-rw-rw----    1 10030    10030         233 Mar 18  2009 /data/data/com.weather.Weather/files/tile-Radar-023010232-200903181940-twc.png 
```



当 Dalvik（实际上是 `zygote` 进程）加载应用程序时，它会切换到该应用程序的 `uid` 和 `gid`，以便进程在正确的安全上下文中运行。

#### 示例进程列表

如果将下面的 `Uid` 与上面的列表进行比较，您会看到分配的 `UID` 与正在运行的进程之间的对应关系。（例如，`10017` 是浏览器）。

```
# ps
  PID  Uid        VSZ Stat Command
    1 0           288 S   /init
[kernel threads omitted...]
   30 1000        808 S   /system/bin/servicemanager
   31 0           848 S   /system/bin/vold
   32 0           668 S   /system/bin/debuggerd
   33 1001       7888 S   /system/bin/rild
   34 0         70548 S   zygote /bin/app_process -Xzygote /system/bin --zygote
   35 1013      30032 S   /system/bin/mediaserver
   36 1002       1172 S   /system/bin/dbus-daemon --system --nofork
   37 0           816 S   /system/bin/installd
   39 0           744 S   /system/bin/sh /runme.sh
   40 1008       1304 S   /system/bin/akmd
   41 0          3340 S   /sbin/adbd
   64 1000     171284 S   system_server
  108 1001     122172 S   com.android.phone
  110 10004    129936 S   android.process.acore
  387 10004    101668 S   com.android.inputmethod.latin
 6721 10017    158272 S   com.android.browser
 6901 10019     96340 S   com.google.android.apps.maps
 7166 0           740 S   /system/bin/sh -
 7635 10007    123776 S   com.google.process.gapps
 7727 10000     91284 S   com.android.alarmclock
 7753 0           872 S   sleep 3
 7754 0          2104 R   ps 
```

### 偏执网络（Paranoid networking）

Android 在 Linux 内核中添加了一个“偏执网络”选项，该选项根据调用进程的组限制对某些网络功能的访问。

允许访问网络功能的组列表位于内核源文件中：`/include/linux/android_aids.h`

以下是该列表：

| #define | GID | Capability |
|---------|-----|------------|
| AID_NET_BT_ADMIN | 3001 | 可以创建 RFCOMM、SCO 或 L2CAPP 蓝牙套接字 |
| AID_NET_BT | 3002 | 可以创建蓝牙套接字 |
| AID_INET | 3003 | 可以创建 IPv4 或 IPv6 套接字 |
| AID_NET_RAW | 3004 | 可以创建某些类型的 IPv4 套接字？？ |
| AID_NET_ADMIN* | 3005 | 允许进程具有 CAP_NET_ADMIN 权限 |

注意：* 在 Donut 中添加（不在原始 Android 1.0 中）

## 应用级安全

Android 还使用用户空间级别的安全系统来规范应用程序和系统组件之间的通信和交互。相关描述见：[`developer.android.com/guide/topics/security/security.html`](http://developer.android.com/guide/topics/security/security.html)

## 教程

参见 [`siis.cse.psu.edu/android-tutorial.html`](http://siis.cse.psu.edu/android-tutorial.html)

（精简版见：[`siis.cse.psu.edu/android_sec_tutorial.html`](http://siis.cse.psu.edu/android_sec_tutorial.html)）

## 安全分析

参见对 Android 安全性的深入分析：[`www.isecpartners.com/files/iSEC_Android_Exploratory_Blackhat_2009.pdf`](http://www.isecpartners.com/files/iSEC_Android_Exploratory_Blackhat_2009.pdf)

## 安全调查

### [TOMOYO Linux](http://elinux.org/TomoyoLinux) 调查

#### 演示文稿

*   [“使用 TOMOYO Linux 学习、分析和保护 Android (JLS2009)”](http://www.slideshare.net/haradats/learning-analyzing-and-protecting-android-with-tomoyo-linux-jls2009)（日本 Linux 研讨会 2009，2009 年 10 月）

*   [“TOMOYO Linux on Android”](http://www.slideshare.net/haradats/taipei2009)（[2009 年台北智能本/上网本/移动应用会议](http://www.slideshare.net/haradats/taipei2009)，2009 年 10 月）

*   [“TOMOYO Linux on Android”](http://www.slideshare.net/haradats/tomoyo-linux-on-android)（CELF 日本技术 Jamboree 28，2009 年 6 月）

*   [slideshare 上关于 TOMOYO Linux 的其他英文幻灯片](http://www.slideshare.net/haradats/presentations?order=popular)

*   [TOMOYO Linux 的所有英文幻灯片 PDF](http://sourceforge.jp/projects/tomoyo/docs/?category_id=532&language_id=1)

#### 代码

*   [tomoyo-android-jp - Google Code 上的项目托管](http://code.google.com/p/tomoyo-android-jp/)

#### 联系方式

haradats@gmail.com

## 安全技巧

### 安装后更改应用程序安全权限

某些应用程序请求的权限超出了实际需要。您可以通过编辑`/data/system/pacakges.xml`来更改授予应用程序的权限集。

`lbcoder` 在 android-platform 邮件列表中写道：

```
进入 /data/system/packages.xml，您可以删除权限行。
保存 packages.xml 后立即重启手机（否则
该文件将被系统再次覆盖）。新减少的
权限将在启动时被读取。
```

[类别](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# 内存使用

> 来源：[eLinux.org](http://eLinux.org/Android_Memory_Usage "http://eLinux.org/Android_Memory_Usage")

# Android 内存使用

Android 系统的内存由多个不同的分配器在多个不同的池中管理。

## 目录

*   1 系统内存
*   2 进程内存
    *   2.1 procrank
    *   2.2 smem 工具
*   3 Dalvik 堆
*   4 调试 Android 应用程序内存使用
    *   4.1 如何调试本机进程内存分配
    *   4.2 libc.debug.malloc
*   5 参考

## 系统内存

您可以通过检查`/proc/meminfo`来查看系统对机器内存的视图。

如果您使用 `ddms`，您可以看到系统以及不同执行进程在机器上使用的内存摘要。单击 `SysInfo` 选项卡，然后在窗格左上角的框中选择“内存使用”。

以下是截图：

![Android 内存使用情况（OMAP EVM 平台，运行 eclair，由 ddms 显示）](http://eLinux.org/File:Ddms-memory-usage1.png "Android 内存使用情况（OMAP EVM 平台，运行 eclair，由 ddms 显示）")

请注意，您可以通过将鼠标悬停在特定的饼图切片上来获取每个进程的数字。数字以 K 和百分比显示。

## 进程内存

您可以通过检查`/proc/<pid>/status`来查看单个进程的内存使用情况。

有关内存使用的详细信息位于：

*   `/proc/<pid>/statm`
*   `/proc/<pid>/maps`
*   `/proc/<pid>/smaps`

`top` 命令将显示 `VSS` 和 `RSS`。

另外，请参阅上面的 `ddms` 信息。

### procrank

`procrank` 将显示进程内存利用率的快速摘要。默认情况下，它显示 `Vss`、`Rss`、`Pss` 和 `Uss`，并按 `Vss` 排序。但是，您可以控制排序顺序。

`procrank` 源代码包含在 `system/extras/procrank` 中，二进制文件位于 Android 设备上的`/system/xbin`中。

*   `Vss` = 虚拟集大小
*   `Rss` = 驻留集大小
*   `Pss` = 比例集大小
*   `Uss` = 唯一集大小

一般来说，您需要关注的两个数字是 `Pss` 和 `Uss`（`Vss` 和 `Rss` 通常没有价值，因为它们不能准确反映进程对与其他进程共享的页面的使用情况。）

*   `Uss` 是进程独有的页面集。这是应用程序立即终止时释放的内存量。
*   `Pss` 是与其它进程共享的内存量，其计算方式是在共享它的进程之间平均分配。如果进程终止，这部分内存不会被释放，但它表示该进程对整体内存负载的“贡献”量。

您还可以使用 `procrank` 查看每个进程的工作集大小，并重置工作集大小计数器。

以下是 `procrank` 的用法：



以下为格式化后的内容：

```text
# procrank -h
Usage: procrank [ -W ] [ -v | -r | -p | -u | -h ]
    -v  Sort by VSS.
    -r  Sort by RSS.
    -p  Sort by PSS.
    -u  Sort by USS.
        (Default sort order is PSS.)
    -R  Reverse sort order (default is descending).
    -w  Display statistics for working set only.
    -W  Reset working set of all processes.
    -h  Display this help screen. 
```

以下是一些示例输出：

```text
# procrank
  PID      Vss      Rss      Pss      Uss  cmdline
 1217   36848K   35648K   17983K   13956K  system_server
 1276   32200K   32200K   14048K   10116K  android.process.acore
 1189   26920K   26920K    9293K    5500K  zygote
 1321   20328K   20328K    4743K    2344K  android.process.media
 1356   20360K   20360K    4621K    2148K  com.android.email
 1303   20184K   20184K    4381K    1724K  com.android.settings
 1271   19888K   19888K    4297K    1764K  com.android.inputmethod.latin
 1332   19560K   19560K    3993K    1620K  com.android.alarmclock
 1187    5068K    5068K    2119K    1476K  /system/bin/mediaserver
 1384     436K     436K     248K     236K  procrank
    1     212K     212K     200K     200K  /init
  753     572K     572K     171K     136K  /system/bin/rild
  748     340K     340K     163K     152K  /system/bin/sh
  751     388K     388K     156K     140K  /system/bin/vold
 1215     148K     148K     136K     136K  /sbin/adbd
  757     352K     352K     117K      92K  /system/bin/dbus-daemon
  760     404K     404K     104K      80K  /system/bin/keystore
  759     312K     312K     102K      88K  /system/bin/installd
  749     288K     288K      96K      84K  /system/bin/servicemanager
  752     244K     244K      71K      60K  /system/bin/debuggerd 
```

在这个示例中，它显示了本地守护进程和程序比基于 Dalvik 的服务和程序小一个数量级。此外，即使是最小的 Dalvik 程序也需要大约 1.5 兆字节（`Uss`）才能运行。

### `smem` 工具

你可以使用 `smem` 查看非常详细的按进程或系统范围的内存信息。

参见 [使用 smem on Android](http://eLinux.org/Using_smem_on_Android "Using smem on Android")

## Dalvik 堆

Dalvik 堆由 `zygote` 预加载类和数据（截至 Android 2.2 版本，预加载了超过 1900 个类）。当 `zygote` 分叉启动一个 Android 应用程序时，新应用程序会获得此堆的写时复制映射。正如 Dan Borstein 在下面所说，这有助于减少内存占用以及加快应用程序启动时间。

与其他许多语言的虚拟机一样，Dalvik 在堆上执行垃圾回收。每个 VM 进程中似乎有一个单独的线程（称为 `HeapWorker`）执行垃圾回收操作。（参见 `toolbox ps -t`）[需要更多关于垃圾回收的说明]

Dan Borstein 对堆共享的说明^([[1]](#cite_note-1))：

它用于 Android，将大量与常见库类相关的、有效只读（技术上可写但实际上很少写入）的数据的 RAM 占用，在所有的活动 VM 进程中进行摊销。系统启动时会预加载 1000 多个类，每个类至少会消耗一点堆空间，并且通常会指向一系列其他对象。由预加载过程创建的堆会与每个派生的 VM 进程共享写时复制（但实际上在实践上很少被写入）。这为每个进程节省了数百 KB 的脏不可分页 RAM，同时也有助于加快进程启动速度。

[需要信息：如何显示 dalvik 堆信息？]

## 调试 Android 应用程序内存使用

参见 Dianne Hackborn 的一篇优秀文章：[`stackoverflow.com/questions/2298208/how-to-discover-memory-usage-of-my-application-in-android/2299813#2299813`](http://stackoverflow.com/questions/2298208/how-to-discover-memory-usage-of-my-application-in-android/2299813#2299813)

### 如何调试本地进程内存分配

```text
setprop dalvik.vm.checkjni true
setprop libc.debug.malloc 10
setprop setprop dalvik.vm.jniopts forcecopy
start
stop 
```

### `libc.debug.malloc`

系统中的 C 库（bionic）支持在运行时使用不同的调试版本 `malloc` 代码的能力。

如果系统属性 `libc.debug.malloc` 的值不是 0，那么当进程被实例化时，C 库会为该进程使用分配和释放内存的函数。

（请注意，还有其他方式会导致调试共享库的 `malloc` 代码最终被使用。也就是说，如果你在模拟器中运行，且系统属性 `ro.kernel.memcheck` 的值不为 '0'，那么你会获得调试级别 20。请注意，调试级别 20 只能在模拟器中使用。）

默认情况下，使用标准的 `malloc`/`free`/`calloc`/`realloc`/`memalign` 例程。通过设置 `libc.debug.malloc`，会使用不同的例程，来检查某些类型的内存错误（如泄漏和越界）。这是通过加载一个包含这些不同例程的单独的共享库（`.so`）来实现的。

共享库的名称为：`/system/lib/libc_malloc_debug_leak.so` 和 `/system/lib/libc_malloc_debug_qemu.so`

（信息来源于查看 `<android-source-root>/bionic/libc/bionic/malloc_debug_common.c`）

`libc.debug.malloc` 支持的值（调试级别）有：

*   1 - 执行泄漏检测

*   5 - 填充已分配内存以检测越界

*   10 - 填充内存并添加哨兵以检测越界

*   20 - 为模拟器使用经过特殊检测的 `malloc`/`free` 例程

我不确定这些共享库是否会在生产设备中提供。

## 参考文献

1.  ↑ Dan Borstein 的评论，2009 年 1 月，对博客文章 [Dalvik vs. Mono](http://www.koushikdutta.com/2009/01/dalvik-vs-mono.html) 的评论

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Dalvik 虚拟机

> 来源：[eLinux.org](http://eLinux.org/Android_Dalvik_VM "http://eLinux.org/Android_Dalvik_VM")

# Android Dalvik VM

Dalvik 是 Android 应用程序运行的虚拟机的名称。此 VM 执行 Dalvik 字节码，该字节码是从用 Java 语言编写的程序编译而来的。注意，Dalvik VM 不是 Java VM（`JVM`）。

每个 Android 应用程序都在自己的进程中运行，并带有自己的 Dalvik 虚拟机实例。

在启动时，会创建一个名为 `zygote` 的单个虚拟机，它会预加载一长串类。（截至 Android 2.1（eclair）版本，`zygote` 预加载的类列表有 1,942 个条目）。所有其他“java”程序或服务都从这个进程分叉出来，并在各自的地址空间中作为自己的进程（和线程）运行。Android 框架中的应用程序和系统服务都是用“java”实现的。

编写 Dalvik 是为了让设备能够高效地运行多个 VM。Dalvik VM 执行 Dalvik 可执行文件（`.dex`）格式的代码，该格式针对最小内存占用进行了优化。VM 是基于寄存器的，运行由 Java 语言编译器编译的类，这些类已通过附带的“dx”工具转换为 `.dex` 格式。

大多数 Android 应用程序以包（`.apks`）的形式交付并存储在系统中，其中包含 dex 字节码（类和方法的代码）和资源。在首次启动时，系统会在 `/data/dalvik-cache` 中创建 dex 类的缓存。

## 目录

*   1 文档

*   2 问答

*   3 JIT

*   4 与 Java 的关系

*   5 其他平台上的 Dalvik

*   6 调试 VM

    *   6.1 获取堆栈跟踪

    *   6.2 使用 checkJNI

*   7 资源

## 文档

在源代码中的 `dalvik/docs` 目录下有一些关于 Dalvik 的文档。参见 [Android dalvik 文档 git 仓库](http://android.git.kernel.org/?p=platform/dalvik.git;a=tree;f=docs;)。



源代码中有一些相当长的注释，包括在`Thread.c`和`Exception.c`的顶部附近。`mterp`目录中有一些笔记描述了解释器的结构。

## Q&A

来自`fadden`在`android-platform`列表上的提问：

- 谁负责读取`dex`文件并调用`Dalvik`？
  - VM由框架通过`JNI`调用接口启动。参见`frameworks/base`中的`AndroidRuntime.cpp`。

- 是否有教程教如何通过`adb`终端启动应用：字节码文件 > `dex`文件 > 在`Dalvik`中启动应用 => 并在`adb`中查看结果？
  - 参见`dalvik/docs`目录中的“hello-world.html”（上面有链接）。

- `Dalvik`内部是否有分析器，能让我们跟踪`dalvik`执行的每一步？
  - 你可以开启`LOG_INSTR`来查看每条指令的执行过程。这会产生大量的日志。如果你尝试在设备上这样做，会很快超出64KB的`kernel`日志缓冲区并丢失大量信息，因此它只适用于“桌面”版本（例如`sim-eng`）。
  - 另外，`Dalvik`确实包含用于跟踪和性能分析的插桩。参见[`elinux.org/Android_Tools#traceview`](http://elinux.org/Android_Tools#traceview)。

## JIT

从2.2版本（*Froyo*）开始，`Dalvik`包含了一个即时编译器（JIT）。

- 参见[适用于Android Dalvik VM的JIT编译器](http://code.google.com/events/io/2010/sessions/jit-compiler-androids-dalvik-vm.html)
  - `Ben Cheng`和`Bill Buzbee`在`Google IO 2010`上的演示视频
  - [幻灯片，PDF格式](http://dl.google.com/googleio/2010/android-jit-compiler-androids-dalvik-vm.pdf)

从2.2版本开始，`Dalvik JIT`是一个“基于代码片段的JIT”，这意味着它只编译在运行时发现为“热点”的单个代码片段。（也就是说，它不会编译整个方法。）`Dalvik`字节码解释器会持续分析它正在执行的代码，当某段代码被确定为执行频繁时，它会被传递给编译器转换为本地代码。在这个过程中可能会执行多种优化。之后，在执行该软件的这一部分时，会执行这段本地代码，而不是原来的字节码。

据报道，JIT的内存开销为每个应用程序100K至200K。在一个示例中（参见演示文稿的幻灯片22），本地指令与`DEX`字节码的大小比为7.7比1。也就是说，执行相同操作，本地指令占用的空间大约是`DEX`字节码的8倍。

## 与Java的关系

由于`Dalvik`不被称为Java虚拟机，因此它不使用“Java”的品牌。此外，它不执行Java字节码。因此，`Google`可以忽略与`Sun`或`Oracle`的许可问题。

然而，创建`Dalvik`程序需要Java编译器和一组类库。

截至2010年3月，构建`Android`系统及其附加应用程序仅支持`Sun JDK`版本1.5。

## Dalvik在其他平台上的实现

- `Myriad Alien Dalvik` - 为其他平台实现的`Dalvik VM`（首次在`Meego`上演示）
  - [`www.linuxfordevices.com/c/a/News/Myriad-Group-Myriad-Alien-Dalvik/?kc=LNXDEVNL020911`](http://www.linuxfordevices.com/c/a/News/Myriad-Group-Myriad-Alien-Dalvik/?kc=LNXDEVNL020911)

## 调试VM

你可以设置许多属性来控制VM的操作，并允许调试系统的各个方面：

参见[`netmite.com/android/mydroid/dalvik/docs/embedded-vm-control.html`](http://netmite.com/android/mydroid/dalvik/docs/embedded-vm-control.html)

（注意，这在`<aosp-root>/dalvik/docs`中，还有其他许多包含`Dalvik`相关信息的文件。）

这提到了一些可以通过属性控制的功能，包括：

- `checkjni` - 使用`JNI`时执行各种检查
- `enableassertions` - 在VM代码中启用断言
- `verify-bytecode` - 是否执行字节码验证
- `execution-mode` - 解释器使用优化汇编代码还是可移植的C代码
- `stack-trace-file` - 收到`SIGQUIT`信号时堆栈跟踪数据的存放位置

### 获取堆栈跟踪

你可以通过发送`SIGQUIT`信号来强制VM转储所有线程的堆栈跟踪。这可以通过`kill -3 <pid>`实现，其中`pid`是主`dalvik`进程的ID。默认情况下，堆栈跟踪会发送到`android`日志，但你也可以将数据发送到文件（使用`dalvik.vm.stack-trace-file`属性）。

### 使用checkJNI

`CheckJNI`指的是`Dalvik VM`的一种特殊运行时模式，它强制VM执行某些检查，并在通过`JNI`调用的代码发生某些错误时报告问题。

参见[`android-developers.blogspot.com/2011/07/debugging-android-jni-with-checkjni.html`](http://android-developers.blogspot.com/2011/07/debugging-android-jni-with-checkjni.html)

## 资源

- [Dalvik维基百科条目](http://en.wikipedia.org/wiki/Dalvik_(software))
- [Dalvik VM内部机制](http://sites.google.com/site/io/dalvik-vm-internals) - `Dan Bornstein`在`Google IO 2008`上的演示视频
- [DEX文件格式](http://www.retrodev.com/android/dexformat.html)，由`Michael Pavone`逆向工程
- [Dalvik字节码](http://developer.android.com/reference/dalvik/bytecode/Opcodes.html)

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

- [Android](http://eLinux.org/Category:Android "Category:Android")

# 包、资产和资源

> 来源：[eLinux.org](http://eLinux.org/Android_Packages "http://eLinux.org/Android_Packages")

# Android包

## 目录

- 1 包
  - 1.1 `AndroidManifest.xml`
  - 1.2 包管理工具
- 2 资源
- 3 资产

## 包

`Android`应用程序以“包”的形式分发，它们是包含类文件、资源和元信息（`AndroidManifest.xml`文件和应用程序的安全证书）的压缩归档文件。

一个包的扩展名为`.apk`，它由一组目录和文件组成，并进行了`gzip`压缩归档。

一个包通常包含以下内容：

- `META-INF/MANIFEST.MF` - 包文件（`apk`）自身的清单文件。
- `META-INF/CERT.SF` - 安全证书
- `META-INF/CERT.RSA` - 另一个安全证书（应该区分这两个证书）
- `AndroidManifest.xml` - 此包中应用程序的清单文件
- `classes.dex` - 此包中应用程序的`dalvik`（[`eLinux.org/java`](http://eLinux.org/java)）类的实际代码
- `res/` - 包含资源文件的目录
- `resources.arsc` - ???

### AndroidManifest.xml

`AndroidManifest.xml`文件包含包中应用程序的信息。通常，一个包会包含一个应用程序。`AndroidManifest`文件描述了应用程序的名称、所需的库和安全权限、应用程序使用的消息、代表应用程序的图标等等。

详细内容参见[`developer.android.com/guide/topics/manifest/manifest-intro.html`](http://developer.android.com/guide/topics/manifest/manifest-intro.html)。

### 包管理工具

[aapt](http://eLinux.org/Android_aapt "Android aapt")工具用于创建、检查和修改`Android`包。

## 资源

应用程序资源的概述位于：[`developer.android.com/guide/topics/resources/index.html`](http://developer.android.com/guide/topics/resources/index.html)

可以将原始文件用作资源（而不被构建系统编译）。参见这篇关于[在Android中将原始文件用作资源](http://thedevelopersinfo.com/2009/11/27/using-files-as-raw-resources-in-android/)的的文章。

## 资产



`Assets` are like resources, except that they do not have a resource ID, and they are listed in the `assets` directory of a package, rather than the `res` directory.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Networking

> From: [eLinux.org](http://eLinux.org/Android_Networking "http://eLinux.org/Android_Networking")

# Android Networking

Here are some tips for getting networking working on your Android device.

## Setting the DNS server

In my experience, some times the device fails to get its DNS server correctly from DHCP. The DNS server address is retrieved from system properties.

You can set this manually by typing (on the target):

```
$ setprop net.eth0.dns1 xx.yy.zz.aa 
```

(replacing with the correct numeric values for your DNS server address)

I have also set the following:

```
$ setprop net.nds1 xx.yy.zz.aa 
```

This needs to be set each time the system boots. I'm sure there's a way to have `init` set this, or to put it into persistent properties, but I haven't done that yet.

## Configuring a web proxy

The browser looks at system settings stored in a provider database for the http proxy.

The value for `http_proxy` is set in the following sqlite database: `/data/data/com.android.providers.settings/databases/settings.db`

The setting goes in the `system` table in this database, with a key of `99`, a name of `http_proxy` and a value that is a string containing your proxy server and port. I don't know if you can use a server name rather than just an IP address. I haven't done that.

To set this, on target, do the following:

```
 # cd /data/data/com.android.providers.settings/databases
 # sqlite3 settings.db
SQLite version 3.5.9
Enter ".help" for instructions
sqlite> insert into system values(99,'http_proxy','192.168.1.1:80');
sqlite>.exit 
```

*Replace `192.168.1.1:80` with the appropriate address and port for your network configuration.*

Since it's only a single line, you can also do this from the command line. You can check that the value is stored properly by typing the following:

```
# sqlite3 settings.db "select * from system;" 
```

This should show output similar to the following (first part omitted):

```
...
38|volume_ring|4
39|volume_ring_last_audible|4
99|http_proxy|43.131.3.73:80 
```

This change is persistent, and you should only have to make it once.

## Setting up networking on bootup

Add the following lines in the `init.rc`:

```
service ethernet /eth0.sh 
```

Now create a file at the root (or anywhere else, probably in `/system/etc` but modify the above line accordingly) called `eth0.sh`, make it executable (`chmod +x eth0.sh`) and put the following lines in it:

```
#!/system/bin/sh

netcfg eth0 dhcp

setprop net.dns1 8.8.8.8
setprop net.dns2 8.8.4.4 
```

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# File Systems

> From: [eLinux.org](http://eLinux.org/Android_File_Systems "http://eLinux.org/Android_File_Systems")

# Android File Systems

## YAFFS

Android in most mobile phones up to version 2.2 (Froyo) use the YAFFS2 filesystem.

Here is some information about YAFFS2:

*   [File Systems#YAFFS2](http://eLinux.org/File_Systems#YAFFS2 "File Systems")

*   Wookey's presentation about YAFFS at ELC Europe 2007 [yaffs.pdf](http://eLinux.org/images/e/e3/Yaffs.pdf "Yaffs.pdf"), [video](http://free-electrons.com/pub/video/2007/elce/elce-2007-wookey-yaffs.ogg)

*   [YAFFS update for ELC Europe 2010](http://wookware.org/talks/yaffsupdate-ELCE-2010.pdf)

## EXT4

According to this report by Ted Tso, version 2.3 (Gingerbread) will be using ext4

[`www.linuxfoundation.org/news-media/blogs/browse/2010/12/android-will-be-using-ext4-starting-gingerbread`](http://www.linuxfoundation.org/news-media/blogs/browse/2010/12/android-will-be-using-ext4-starting-gingerbread)

With ext4, you may need to explicitly sync the data to the file system, in order to make sure not to lose information.

See [this blog entry by Tim Bray](http://android-developers.blogspot.com/2010/12/saving-data-safely.html) for information on this topic.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Logging System

> From: [eLinux.org](http://eLinux.org/Android_Logging_System "http://eLinux.org/Android_Logging_System")

# Android Logging System

This article describes the Android logging system

## Contents

*   1 Overview

*   2 Kernel driver

*   3 System and Application logging

    *   3.1 Application log

    *   3.2 Event log

    *   3.3 System log

*   4 `log` command line tool

*   5 Capturing stdout with `logwrapper`

*   6 `Logcat` command

    *   6.1 Trick to couple Android logging to Linux kernel logging

*   7 Resources

## Overview

The Android system has a logging facility that allows systemwide logging of information, from applications and system components. This is separate from the Linux kernel's own logging system, which is accessed using `dmesg` or `/proc/kmsg`. However, the logging system does store messages in kernel buffers.

![](http://eLinux.org/File:Android-logging-kmc-kobayashi.png)

image by Tetsuyuki Kobabayshi, of Kyoto Microcomputer Co.

The logging system consists of:

*   a kernel driver and kernel buffers for storing log messages

*   C, C++ and Java classes for making log entries and for accessing the log messages

*   a standalone program for viewing log messages (`logcat`)

*   ability to view and filter the log messages from the host machine (via `eclipse` or `ddms`)

There are four different log buffers in the Linux kernel, which provide logging for different parts of the system. Access to the different buffers is via device nodes in the file system, in `/dev/log`.

The four log buffers are:

*   `main` - the main application log

*   `events` - for system event information

*   `radio` - for radio and phone-related information

*   `system` - a log for low-level system messages and debugging

Up until 2010, only the first three logs existed. The system log was created to keep system messages in a separate buffer (outside of `/dev/log/main`) so that a single verbose application couldn't overrun system messages and cause them to be lost.

Each message in the log consists of a tag indicating the part of the system or application that the message came from, a timestamp, the message log level (or *priority* of the event represented by the message) and the log message itself.

All of the log buffers except for `event` use free-form text messages. The `event` buffer is a `binary` buffer, where the event messages (and event parameters) are stored in binary form. This form is more compact, but requires extra processing when the event is read from the buffer, as well as a message lookup database, to decode the event strings.

The logging system automatically routes messages with specific tags into the radio buffer. Other messages are placed into their respective buffers when the log class or library for that buffer is used.

## Kernel driver

The kernel driver for logging is called the `logger`. See [Android logger](http://eLinux.org/Android_logger "Android logger")

## System and Application logging

### Application log

An Android application includes the [android.util.Log class](http://developer.android.com/reference/android/util/Log.html), and uses methods of this class to write messages of different priority into the log.

Java classes declare their tag statically as a string, which they pass to the log method. The log method used indicates the message "severity" (or log level). Messages can be filtered by tag or priority when the logs are processed by retrieval tools (`logcat`).

### Event log



`EventLog` messages are created using the [android.util.EventLog class](http://developer.android.com/reference/android/util/EventLog.html), which creates binary-formatted log messages. Log entries consist of binary tag codes, followed by binary parameters. The message tag codes are stored on the system at `/system/etc/event-log-tags`. Each message has the string for the log message, as well as codes indicating the values associated with (stored with) that entry.

## System log

Many classes in the Android framework utilize the system log to keep their messages separate from possibly noisy application log messages. These programs use the `android.util.Slog` class, with its associated messages.

In all cases, eventually a formatted message is delivered through the C/C++ library down to the kernel driver, which stores the message in the appropriate buffer.

## `log` command-line tool

There is a `log` command-line tool that can be used to create log entries from any program. This is built into the `toolbox` multi-function program.

The usage for this is:

```
USAGE: log [-p priorityChar] [-t tag] message
       priorityChar should be one of:
               v,d,i,w,e
```

## Capturing stdout with `logwrapper`

It is sometimes useful to capture stdout from native applications into the log. There is a utility called `logwrapper` which can be used to run a program and redirect its stdout into log messages.

The `logwrapper` usage is:

```
Usage: logwrapper [-x] BINARY [ARGS ...]

Forks and executes BINARY ARGS, redirecting stdout and stderr to
the Android logging system. Tag is set to BINARY, priority is
always LOG_INFO.

-x: Causes logwrapper to SIGSEGV when BINARY terminates
    fault address is set to the status of wait()
```

Source for `logwrapper` is at: `system/core/logwrapper/logwrapper.c`

## `logcat` command

You can use the `logcat` command to read the log. This command is located in `/system/bin` in the local filesystem, or you can access the functionality using the `adb logcat` command.

Documentation on the use of this command is at: [`developer.android.com/guide/developing/tools/adb.html`](http://developer.android.com/guide/developing/tools/adb.html).

Some quick notes:

- Log messages each have a tag and priority.
- You can filter the messages by tag and log level, with a different level per tag.
- You can specify, using a system property, that various programs emit their stdout or stderr to the log.

### Trick to couple Android logging to Linux kernel logging

Note that the Android logging system is completely separate from the Linux kernel log system, which uses `printk` inside the kernel to save messages and `dmesg` to extract them. You can write to the kernel log from user space by writing to `/dev/kmsg`.

I've seen a reference to couple the two together, to redirect Android messages into the kernel log buffer, using the `logcat` program launched from `init`, like below:

```
service logcat /system/bin/logcat -f /dev/kmsg
      oneshot
```

(See [`groups.google.com/group/android-kernel/browse_thread/thread/87d929863ce7c29e/f8b0da9ed6376b2f?pli=1`](http://groups.google.com/group/android-kernel/browse_thread/thread/87d929863ce7c29e/f8b0da9ed6376b2f?pli=1).)

I'm not sure why you'd want to do this (maybe to put all messages into a single stream, with the same timestamp, if kernel message timestamping is on).

## Resources

- [Android Debug Bridge reference page](http://developer.android.com/guide/developing/tools/adb.html)
  - Has `adb logcat` usage information.
- [Logging System Of Android](http://blog.kmckk.com/archives/2936958.html): Presentation by Tetsuyuki Kobayashi, September 2010, at CELF's Japan Technical Jamboree 34.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Source Code Description

> From: [eLinux.org](http://eLinux.org/Android_Source_Code_Description "http://eLinux.org/Android_Source_Code_Description")

Android source code is massive and contains several projects, and this is humanly impossible to remember each and every single project available. This page has been brought to life to enable developers to understand the different parts of the source code. This page contains different versions of Android, and it outlines in detail what each directory contains. Following are the links to the different Android version source code information:

- [android-4.0.3_r1](http://eLinux.org/Android-4.0.3_r1 "Android-4.0.3 r1")
- [android-4.1.1_r4](http://eLinux.org/Android-4.1.1_r4 "Android-4.1.1 r4")
- [master-android](http://eLinux.org/Master-android "Master-android")
- [AOSP Contribution](http://eLinux.org/AOSP_Contribution "AOSP Contribution")

Written and maintained by: [Nanik Tolaram](https://plus.google.com/+NanikT/)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# 软件开发

## Android 软件开发

关于 Android 软件开发，内容涵盖 SDK、构建系统、工具、调试和测试。

## Software Development Kit

> From: [eLinux.org](http://eLinux.org/Android_SDK "http://eLinux.org/Android_SDK")

### Android SDK

[Android Developers Homepage](http://developer.android.com/index.html)

#### Application SDK

Used for creating high-level portable Java code.

1. [Android SDK](http://developer.android.com/sdk/index.html) (Required)
2. [Eclipse](http://www.eclipse.org/downloads/) Classic or greater (Not technically required)
3. [Eclipse ADT Plugin](http://developer.android.com/sdk/eclipse-adt.html) (Required if using Eclipse)
4. [NetBeans plugin](http://kenai.com/projects/nbandroid/) (No official support)
5. [Windows USB Driver](http://developer.android.com/sdk/win-usb.html) (Only needed if using Windows)

**Versions**: [Regularly Updated Dashboard](http://developer.android.com/resources/dashboard/platform-versions.html)

Top 3 SDKs in use by users as of 4/13/2010:

1. `1.5`
2. `1.6`
3. `2.0`

#### Native SDK

Used to create a portable shared object library file for your C/C++ or assembly code inside your Java application.

1. [Android NDK](http://developer.android.com/sdk/ndk/index.html)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Source Build System

> From: [eLinux.org](http://eLinux.org/Android_Build_System "http://eLinux.org/Android_Build_System")

## Android Build System

Basics of the Android build system were described at (down as of 9/2011): [`source.android.com/porting/build_system.html`](http://source.android.com/porting/build_system.html).

*Note that `partner-setup` should be replaced with `choosecombo` or even `lunch` in that description.*

*This information seems to be duplicated at:* [`pdk.android.com/online-pdk/guide/build_system.html`](http://pdk.android.com/online-pdk/guide/build_system.html). I'm going to assume that the source.android site is the most up-to-date, but I haven't checked.

More information about the Android build system, and some of the rationale for it, is described at: [`android.git.kernel.org/?p=platform/build.git;a=blob_plain;f=core/build-system.html`](http://android.git.kernel.org/?p=platform/build.git;a=blob_plain;f=core/build-system.html).

You use `build/envsetup.sh` to set up a “convenience environment” for working on the Android source code. This file should be sourced into your current shell environment. After doing so, you can type `help` or `hmm` for a list of defined functions that are helpful for interacting with the source.

## Contents

1. Overview
2. Some Details
   1. What tools are used
   2. Telling the system where the Java toolchain is
   3. Specifying what to build
   4. Actually building the system
3. Build tricks
   1. Seeing the actual commands used to build the software
   2. Make targets
   3. Helper macros and functions



- 3.4 Speeding up the build
- 3.5 Building only an individual program or module
- 3.6 Setting module-specific build parameters
- 4 Makefile tricks
  - 4.1 Build helper functions
  - 4.2 Add a file directly to the output area
- 5 Adding a new program to build
  - 5.1 Steps for adding a new program to the Android source tree
- 6 Building the kernel

## Overview

The build system uses some pre-set environment variables and a series of `make` files in order to build an Android system and prepare it for deployment to a platform.

Android make files end in the extension `.mk` by convention, with the main make file in any particular source directory being named `Android.mk`.

There is only one official file named `Makefile`, at the top of the source tree for the whole repository. You set some environment variables, then type `make` to build stuff. You can add some options to the `make` command line (other targets) to turn on verbose output, or perform different actions.

The build output is placed in `out/host` and `out/target`. Stuff under `out/host` are things compiled for your host platform (your desktop machine). Stuff under `out/target/product/<platform-name>` eventually makes its way to a target device (or emulator).

The directory `out/target/product/<platform-name>/obj` is used for staging "object" files, which are intermediate binary images used for building the final programs. Stuff that actually lands in the file system of the target is stored in the directories `root`, `system`, and `data`, under `out/target/product/<platform-name>`. Usually, these are bundled up into image files called `system.img`, `ramdisk.img`, and `userdata.img`.

This matches the separate file system partitions used on most Android devices.

## Some Details

### What tools are used

During the build you will be using `make` to control the build steps themselves. A host toolchain (compiler, linker and other tools) and libraries will be used to build programs and tools that will run on the host. A different toolchain is used to compile the C and C++ code that will wind up on the target (which is an embedded board, device or the emulator). This is usually a "cross" toolchain that runs on an X86 platform, but produces code for some other platform (most commonly ARM). The kernel is compiled as a standalone binary (it does not use a program loader or link to any outside libraries). Other items, like native programs (e.g. `init` or `toolbox`), daemons or libraries will link against bionic or other system libraries.

You will be using a Java compiler and a bunch of java-related tools to build most of the application framework, system services and Android applications themselves. Finally, tools are used to package the applications and resource files, and to create the filesystem images that can be installed on a device or used with the simulator.

### Telling the system where the Java toolchain is

Before you build anything, you have to tell the Android build system where your Java SDK is. (Installing a Java SDK is a pre-requisite for building).

Do this by setting a `JAVA_HOME` environment variable.

### Specifying what to build

In order to decide what to build, and how to build it, the build system requires that some variables be set. Different products, with different packages and options can be built from the same source tree. The variables to control this can be set via a file with declarations of `make` variables, or can be specified in the environment.

A device vendor can create definition files that describe what is to be included on a particular board or for a particular product. The definition file is called `buildspec.mk`, and it is located in the top-level source directory. You can edit this manually to hardcode your selections.

If you have a `buildspec.mk` file, it sets all the make variables needed for a build, and you don't have to mess with options.

Another method of specifying options is to set environment variables. The build system has a rather ornate method of managing these options for you.

To set up your build environment, you need to load the variables and functions in `build/envsetup.sh`. Do this by "source-ing" the file into your shell environment, like this:

```sh
$ source build/envsetup.sh
```

or

```sh
$ . build/envsetup.sh
```

You can type `help` (or `hmm`) at this point to see some utility functions that are available to make it easier to work with the source.

To select the set of things you want to build, and what items to build for, you use either the `choosecombo` function or the `lunch` function. `choosecombo` will walk you through the different items you have to select, one-by-one, while `lunch` allows you select some pre-set combinations.

The items that have to be defined for a build are:

- the product (`generic` or some specific board or platform name)
- the build variant (`user`, `userdebug`, or `eng`)
- whether you're running on a simulator (`true` or `false`)
- the build type (`release` or `debug`)

Descriptions of these different build variants are at [`source.android.com/porting/build_system.html#androidBuildVariants`](http://source.android.com/porting/build_system.html#androidBuildVariants).

The build process from a user perspective is described pretty well in this blog post: [First Android platform build](http://blog.codepainters.com/2009/12/18/first-android-platform-build/) by CodePainters, December 2009.

### Actually building the system

Once you have things set up, you actually build the system with the `make` command.

To build the whole thing, run `make` in the top directory. The build will take a long time if you are building everything (for example, the first time you do it).

## Build tricks

### Seeing the actual commands used to build the software

Use the `showcommands` target on your `make` line:

```sh
$ make -j4 showcommands
```

This can be used in conjunction with another make target, to see the commands for that build. That is, `showcommands` is not a target itself, but just a modifier for the specified build.

In the example above, the `-j4` is unrelated to the `showcommands` option, and is used to execute 4 make sessions that run in parallel.

### Make targets

Here is a list of different make targets you can use to build different parts of the system:

- `make sdk` - build the tools that are part of an SDK (`adb`, `fastboot`, etc.)
- `make snod` - build the system image from the current software binaries
- `make services`
- `make runtime`
- `make droid` - `make droid` is the normal build.
- `make all` - make everything, whether it is included in the product definition or not
- `make clean` - remove all built files (prepare for a new build). Same as `rm -rf out/<configuration>/`
- `make modules` - shows a list of submodules that can be built (List of all `LOCAL_MODULE` definitions)
- `make <local_module>` - make a specific module (note that this is not the same as directory name. It is the `LOCAL_MODULE` definition in the `Android.mk` file)
- `make clean-<local_module>` - clean a specific module
- `make bootimage TARGET_PREBUILT_KERNEL=/path/to/bzImage` - create a new boot image with custom `bzImage`

### Helper macros and functions

There are some helper macros and functions that are installed when you source `envsetup.sh`. They are documented at the top of `envsetup.sh`, but here is information about a few of them:

- `croot` - change directory to the top of the tree
- `m` - execute `make` from the top of the tree (even if your current directory is somewhere else)
- `mm` - builds all of the modules in the current directory



`mmm \ <dir1u0005c class="calibre16">...` - 构建所提供目录中的所有模块

`cgrep \ <patternu0005c class="calibre16">` - 在本地所有 C/C++ 文件中执行 `grep` 操作

`jgrep \ <patternu0005c class="calibre16">` - 在本地所有 Java 文件中执行 `grep` 操作

`resgrep \ <patternu0005c class="calibre16">` - 在本地所有 `res/*.xml` 文件中执行 `grep` 操作

`godir \ <filenameu0005c class="calibre16">` - 进入包含某个文件的目录

### 加速构建

你可以在 `make` 命令中使用 `-j` 选项，以并发启动多个 `make` 执行的线程。

根据我的经验，你应该指定大约比你机器上的处理器数量多 2 个的线程。如果你有 2 个处理器，使用 `make -j4`；如果它们支持超线程（意味着你有 4 个虚拟处理器），尝试使用 `make -j6`。

你还可以指定使用 `ccache` 编译器缓存，这将会在你首次构建完成后加速后续的构建过程。要做到这一点，请在 shell 命令行中指定 `export USE_CCACHE=1`。（请注意，`ccache` 已包含在仓库的 prebuilt 部分中，无需在宿主机上单独安装。）

### 仅构建单个程序或模块

如果你使用 `build/envsetup.sh`，你可以使用一些已定义的函数来仅构建树的一部分。使用 `mm` 或 `mmm` 命令来实现这一点。

`mm` 命令会在当前目录（我认为也包括其子目录）中进行构建。使用 `mmm` 命令时，你可以指定一个目录或目录列表，它会构建这些目录。

要安装你的更改，请从树的顶层执行 `make snod`。`make snod` 会从当前二进制文件构建一个新的系统镜像。

### 设置模块特定的构建参数

Android 系统中的某些代码可以在构建方式上进行自定义（独立于构建变体以及发布/调试选项）。你可以通过设置变量来控制单个构建选项，既可以将其设置在环境中，也可以直接传递给 `make`（或调用 `make` 的 `m...` 函数）。

例如，通过设置 `INIT_BOOTCHART` 变量，`init` 程序可以构建为支持 bootchart 日志记录。（有关为何要这样做，请参阅 [在 Android 上使用 Bootchart](http://eLinux.org/Using_Bootchart_on_Android "Using Bootchart on Android")。）

你可以通过以下任一方式实现：

```
$ touch system/init/init.c
$ export INIT_BOOTCHART=true
$ make 
```

或

```
$ touch system/init/init.c
$ m INIT_BOOTCHART=true 
```

## Makefile 技巧

以下是一些可以在你自己的 `Android.mk` 文件中使用的提示。

### 构建辅助函数

在文件 `build/core/definitions.mk` 中定义了一整套构建辅助函数。

尝试使用 `grep define build/core/definitions.mk` 获取完整的列表。

以下是一些可能有趣的函数：

*   `print-vars` - 打印所有 Makefile 变量，用于调试

*   `emit-line` - 在构建过程中输出一行内容到文件中

*   `dump-words-to-file` - 将一个词列表输出到文件中

*   `copy-one-file` - 将文件从一个位置复制到另一个位置（目标位置在目标机上？）

### 直接将文件添加到输出区域

你可以使用 `add-prebuilt-files` 函数，将文件直接复制到输出区域，而无需构建任何内容。

以下行摘自 `prebuilt/android-arm/gdbserver/Android.mk`，将一组文件复制到输出区域的 `EXECUTABLES` 目录中：

```
$(call add-prebuilt-files, EXECUTABLES, $(prebuilt_files)) 
```

## 添加新程序进行构建

### 将新程序添加到 Android 源码树的步骤

*   在 `external` 下创建一个目录
    *   例如，`ANDROID/external/myprogram`

*   创建你的 C/C++ 文件。

*   创建 `Android.mk`，作为 `external/ping/Android.mk` 的克隆。

*   将 `ping.c` 和 `ping` 的名称改为与你自己的 C/C++ 文件和程序名相匹配。

*   在 `ANDROID/build/core/main.mk` 中，在 `external/zlib` 之后添加目录名称 `external/myprogram`。

*   从源码树的根目录执行 `make`。

*   你的文件将出现在构建输出区域以及系统镜像中。
    *   如果你想要单独复制文件到目标设备（而非执行完整安装），可以从构建输出区域中的 `out/target/product/...` 下复制你的文件。

有关更多详细信息，请参见 [`www.aton.com/android-native-development-using-the-android-open-source-project/`](http://www.aton.com/android-native-development-using-the-android-open-source-project/)。

## 构建内核

内核位于常规 Android 构建系统之外（事实上，内核默认并未包含在 Android 开源项目中）。然而，AOSP 中存在用于构建内核的工具。如果你要构建内核，请从以下页面开始：[`source.android.com/source/building-kernels.html`](http://source.android.com/source/building-kernels.html)

如果你要为模拟器构建内核，你可能还需要查看：[`stackoverflow.com/questions/1809774/android-kernel-compile-and-test-with-android-emulator`](http://stackoverflow.com/questions/1809774/android-kernel-compile-and-test-with-android-emulator)

此外，Ron M 在 2012 年 5 月 21 日于 android-kernel 邮件列表上写道：

这篇帖子非常老旧了——但就 AOSP 而言，没有任何变化，所以如果有人在为 QEMU 构建时遇到这个问题，或许会感兴趣：

实际上，AOSP 提供了一种更好、更短的构建适用于你的 QEMU 目标内核的方法：

1.  切换到你的内核源码目录（仅 `goldfish 2.6.29` 版本可为模拟器开箱即用）

2.  `${ANDROID_BUILD_TOP}/external/qemu/distrib/build-kernel.sh -j=64 --arch=x86 --out=$YourOutDir`

3.  `emulator -kernel ${YourOutDir}/kernel-qemu`  # 运行模拟器：

第 2 步调用了 `toolbox.sh` 包装脚本，该脚本绕过了禁用 SSE 的 gcc 警告——这种情况发生在 GCC \< 4.5 版本（例如 AOSP 预构建的 X86 工具链）中。

该脚本在 X86 架构下会添加 ` -mfpmath=387 -fno-pic` 参数，从而消除上述编译错误。

要对构建过程进行更精细的控制，你可以使用 `toolbox.sh` 包装脚本，并在不修改脚本文件的情况下设置其他一些配置。

以下是一个构建相同模拟器的示例：

```
# 设置架构
export ARCH=x86
# 让 make 在构建 android x86 时引用 QEMU 包装脚本
（消除上方列出的错误）
export
CROSS_COMPILE=${ANDROID_BUILD_TOP}/external/qemu/distrib/kernel-toolchain/android-kernel-toolchain-
# 在此处放置你的交叉编译器。在此示例中，我使用的是 AOSP 预构建的编译器
export
REAL_CROSS_COMPILE=${ANDROID_BUILD_TOP}/prebuilt/linux-x86/toolchain/i686-android-linux-4.4.3/bin/i686-android-linux-
# 配置你的内核 - 此处我使用默认的 goldfish_defconfig
make goldfish_defconfig
# 构建
make -j64
# 运行模拟器：
emulator -kernel arch/x86/boot/bzImage -show-kernel 
```

此方法适用于 2.6.29 goldfish 分支。如果有人在模拟器上使用 3+ 版本的内核，我很乐意听取相关经验。

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# 应用开发资源

> 来源：[eLinux.org](http://eLinux.org/Android_Application_Development "http://eLinux.org/Android_Application_Development")

# Android 应用开发

关于 Android 应用开发最可靠的参考，请浏览：

## [`developer.android.com/guide/index.html`](http://developer.android.com/guide/index.html)

这包括所有类、包和其他变量的 Java 文档，并且是最新更新的网站。

虽然最常见的做法是从 Eclipse 开始，这是最标准的，但你也自由使用 Netbeans，不过 Netbeans 的 Android SDK 插件更新并不十分活跃，而且据我所知，它是由一个名为 Kenai 的单一项目开发和维护的。

你还应该知道，没有核心 Java 编程的基础，就无法踏入 Android 应用开发领域。是的，这是先决条件，否则会有点困难。



So then, welcome, get ready to jump into the droid community and get going.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Scripting

> From: [eLinux.org](http://eLinux.org/Android_Scripting "http://eLinux.org/Android_Scripting")

`SL4A` (Scripting Layer for Android) allows you to edit and execute scripts and interactive interpreters directly on the Android device. Many parts of the Android API are available directly from the scripting language.

Scripts can be run interactively in a terminal or associated with an icon and launched like regular apps.

Home page: [`code.google.com/p/android-scripting/`](http://code.google.com/p/android-scripting/)

The [SL4A User's Guide](http://code.google.com/p/android-scripting/wiki/UserGuide) is a good place to start.

`SL4A` supports the following languages:

- Python
- Perl
- JRuby
- Lua
- BeanShell
- JavaScript
- Tcl
- Shell scripts

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Debugging

> From: [eLinux.org](http://eLinux.org/Android_Debugging "http://eLinux.org/Android_Debugging")

Debugging methods for Android.

## Contents

- 1. Debuggers
  - 1.1 Kernel and User co-debug with `GDB` on Android
- 2. Loggers
  - 2.1 Kernel message log
    - 2.1.1 Init logging
  - 2.2 Android logging system
- 3. Tracers
  - 3.1 `strace`
  - 3.2 Dalvik Method Tracer
- 4. Additional Resources

## Debuggers

### Kernel and User Co-Debug with GDB on Android

This presentation covers lots of Android debug resources provided by Linaro, presented by Zach Pfeffer in Spring 2012. Included is information about how to debug the kernel and user simultaneously with `gdb`.

See [Media:Zach Pfeffer Next Gen Android 2012.pdf](http://eLinux.org/images/4/4e/Zach_Pfeffer_Next_Gen_Android_2012.pdf "Zach Pfeffer Next Gen Android 2012.pdf").

## Loggers

### Kernel Message Log

The Linux kernel has a message log in an internal ring buffer. You can access the contents of this log using the [`dmesg`](http://en.wikipedia.org/wiki/Dmesg) command.

You can add timing information to the `printk` messages by adding `"time"` to the Linux kernel command line.

#### Init Logging

The Android `init` program outputs some messages to the kernel log as it starts the system. You can increase the verbosity of `init` using the `"loglevel"` command in the `/init.rc` file.

The default `loglevel` is `3`, but you can change it to `8`—the highest level—by changing the following line in the `/init.rc` file.

Change:

```
loglevel 3
```

to:

```
loglevel 8
```

### Android Logging System

The Android application framework has a built-in logging system, which goes through a special driver in the kernel. It is described at [`developer.android.com/guide/developing/tools/adb.html#logcat`](http://developer.android.com/guide/developing/tools/adb.html#logcat).

Note that although the log dumper (`logcat`) is described on the Android developer site on the `adb` page, there is a native `logcat` command included in the Android distribution. It is available on the target file system and can be run locally.

## Tracers

### `strace`

You can use [`strace`](http://en.wikipedia.org/wiki/Strace) on Android. It is included in the Android Open Source Project, at least as of Android 2.1, and appears to be automatically installed in engineering builds of the software.

To use `strace` during early initialization, you can put it in the `/init.rc` file. For example, to trace `zygote` initialization, change the following line in `/init.rc`:

```
service zygote /system/bin/app_process -Xzygote /system/bin --zygote --start-system-server
```

It should be changed to:

```
service zygote /system/xbin/strace -tt -o/data/boot.strace /system/bin/app_process -Xzygote /system/bin --zygote --start system-server
```

### Dalvik Method Tracer

See [`developer.android.com/guide/developing/tools/traceview.html`](http://developer.android.com/guide/developing/tools/traceview.html).

## Additional Resources

- [Google I/O 2009 - Debugging Arts of the Ninja Masters (video)](http://www.youtube.com/watch?v=Dgnx0E7m1GQ&feature=related) by Justin Mattson

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Testing

> From: [eLinux.org](http://eLinux.org/Android_Testing "http://eLinux.org/Android_Testing")

This page has information about various tests you can perform on Android.

Google provides a number of resources for testing applications, including `monkey`, the logger, and the Compliance Test Suite (`CTS`).

For an overview of Android application testing and resources provided by Google, see [`developer.android.com/guide/topics/testing/index.html`](http://developer.android.com/guide/topics/testing/index.html).

## Contents

- 1. Android Test Framework
- 2. Application testing resources
- 3. Benchmarks
- 4. Compliance Test Suite

## Android Test Framework

Google provides an integrated test framework for testing Android applications, based on the `JUnit` test framework from Java.

See [Android Testing Fundamentals](http://developer.android.com/guide/topics/testing/testing_android.html).

## Application Testing Resources

- [`monkeyrunner`](http://developer.android.com/guide/developing/tools/monkeyrunner_concepts.html)
  - The `monkeyrunner` tool provides an API for writing programs that control an Android device or emulator from outside of Android code. It allows you to write a program that runs on your host machine and interacts with an application running in the emulator or on a target device.
  - With `monkeyrunner`, you can write a Python program that installs an Android application or test package, runs it, sends keystrokes to it, takes screenshots of its user interface, and stores screenshots on the host.

- [`Monkey`](http://developer.android.com/guide/developing/tools/monkey.html) is a user interface and application tester for Android applications.
  - It is a command-line tool that sends pseudo-random streams of keystrokes, touches, and gestures to a device.
  - This tool is unrelated to the `monkeyrunner` tool mentioned above. It runs on the target, while `monkeyrunner`-based programs run on the development host machine.

- [Robotium](http://code.google.com/p/robotium/) test framework
  - Robotium is a test framework created to make it easy to write powerful and robust automatic black-box test cases for Android applications. With the support of Robotium, test case developers can write function, system, and acceptance test scenarios spanning multiple Android activities.
  - Robotium has full support for Activities, Dialogs, Toasts, Menus, and Context Menus.

- [Roboelectric](http://pivotal.github.com/robolectric) test framework
  - Roboelectric allows you to test-drive the development of your Android app inside the JVM on your workstation in seconds, instead of in the emulator or on a device, which can be slow.
  - Robolectric allows you to test most Android functionality, including layouts and GUI behavior, services, and networking code. It has more flexibility than Google's testing framework in some areas.

- [Ranorex](http://www.ranorex.com/mobile-automation-testing/android-test-automation.html) test framework
  - Ranorex provides a .NET-based test automation framework that allows you to record test scenarios directly on real mobile devices as well as on desktop machines.
  - Ranorex easily instruments the APK and deploys the instrumented APK directly on the devices, starts the application automatically, performs all recorded actions—keystrokes, touch events, device button events, and validations—and closes the application automatically.

## Benchmarks



There are a number of benchmarks you can use to test operating system, hardware and graphics performance.

For information about performance testing and benchmarks, see: [Android Benchmarks](http://eLinux.org/Android_Benchmarks "Android Benchmarks")

## Compliance Test Suite

Google provides a suite of tests to validate that a device complies with the Android standard.

See [Android Compliance Test Suite](http://eLinux.org/Android_Compliance_Test_Suite "Android Compliance Test Suite") for more informaton.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# 基于 Android 的系统

介绍与 Android 产品相关的信息，内容涵盖 Android 移植、如何获得系统 Root 权限、Android 应用开发、各类派生 ROM、Android 模拟器以及相关开发和测试等。

# Products (announced & shipped)

> From: [eLinux.org](http://eLinux.org/Android_Hardware "http://eLinux.org/Android_Hardware")

# Android Hardware

## Contents

- 1 Android Devices
- 2 Mobile Phones
  - 2.1 That have shipped
  - 2.2 Under development
- 3 Non-phone devices
  - 3.1 That have shipped
  - 3.2 Under development
- 4 Development board

## Android Devices

It looks like there's a page on this on Wikipedia: [`wikipedia.org/wiki/List_of_Android_devices`](http://wikipedia.org/wiki/List_of_Android_devices)

[Hello Android](http://www.helloandroid.com/devices) has a comprehensive database as well, along with an Android app to view the database on your phone.

## Mobile Phones

See [`www.androphones.com/`](http://www.androphones.com/)

### That have shipped

- HTC Dream
  - Branded as the G1 by T-Mobile
  - Google: Android Developer Phone 1 (ADP1) - same hardware as G1, but unlocked.
- HTC G1 V2
- HTC G2, aka HTC Magic
  - Google Android dev phone 2 - same hardware as Magic, but unlocked
- HTC Hero
  - branded as T-Mobile G2
- HTC Hero for CDMA
  - available from Sprint on Oct 11, 2009
- HTC Tatoo - Europe, Oct 2009
  - SPECS: 528MHz Qualcomm processor, 512MB ROM and 256MB RAM, 240x320 px (QVGA) 2.8-inch touchscreen, GPS, WiFi, compass and accelerometer.
  - HTC's Sense UI in TATTOO: [`www.akihabaranews.com/en/news-18854-TATTOO%2C+HTC%E2%80%99s+Latest+Android+Phone+with+Sense+UI.html`](http://www.akihabaranews.com/en/news-18854-TATTOO%2C+HTC%E2%80%99s+Latest+Android+Phone+with+Sense+UI.html)
- Samsung Galaxy (in Europe)
- Samsung Behold II
  - Samsung's TouchWiz 3D Interface: [`www.akihabaranews.com/en/news-19025-Samsung+Behold+II%2C+TouchWiz+Wonder+for+T-Mobile.html`](http://www.akihabaranews.com/en/news-19025-Samsung+Behold+II%2C+TouchWiz+Wonder+for+T-Mobile.html)
- Motorola Droid (on Verizon)
  - branded as Motorola Milestone in Europe
- Motorola Cliq
  - Has "MotoBlur" interface for interacting with social network sites
  - [Wired Article Sep 2009](http://www.wired.com/gadgetlab/2009/09/motorola-android/)
- Motorola Sholes ?
- Sony Ericsson XPERIA 10
  - [`gizmodo.com/5395712/sony-ericsson-xperia-x10-announced-sonys-first-android-device`](http://gizmodo.com/5395712/sony-ericsson-xperia-x10-announced-sonys-first-android-device)
- Sony Ericsson X10 Mini
  - [`www.sonyericsson.com/cws/companyandpress/aboutus/awards/award/x10miniaward?cc=gb&lc=en`](http://www.sonyericsson.com/cws/companyandpress/aboutus/awards/award/x10miniaward?cc=gb&lc=en)

### Under development

- Acer Liquid
  - [`www.linuxfordevices.com/c/a/News/Acer-Liquid/`](http://www.linuxfordevices.com/c/a/News/Acer-Liquid/)
  - [`www.akihabaranews.com/en/news-19112-Acer+Finally+Announces+Their+Android+Liquid+Smartphone.html`](http://www.akihabaranews.com/en/news-19112-Acer+Finally+Announces+Their+Android+Liquid+Smartphone.html)
- HTC Fiesta ?
- LG GW620
  - [Engadget Article Sep 2009](http://www.engadget.com/2009/09/14/lg-officially-announces-gw620-its-first-android-phone/)
  - [Wired article Sep 2009](http://www.wired.com/gadgetlab/2009/09/lg-android-phone/)
  - LG's slide out QWERTY: [`www.akihabaranews.com/en/news-18892-LG-GW620%2C+LG%E2%80%99s+First+Android+Smartphone.html`](http://www.akihabaranews.com/en/news-18892-LG-GW620%2C+LG%E2%80%99s+First+Android+Smartphone.html)

## Non-phone devices

### That have shipped

- [OpenSourceMID.org](http://www.opensourcemid.org) K7 OMAP3530 MID tablet Opensourcemid
- Archos Internet tablets
  - Archos 5 and Archos 7 Internet tablets - [Android tablet plays 720p video](http://www.linuxfordevices.com/c/a/News/Archos-5-Internet-Tablet/?kc=LNXDEVNL091609) Linux For Devices Article, Sep 2009
- Android handheld game device with Cortex-A8 833Mhz powerful SoC
  - ODROID - [Hackable Android handheld game device](http://www.linuxfordevices.com/c/a/News/HardKernel-Odroid/) Linux For Devices Article, Dec 2009
- S3C6410 microcontroller
  - [Android on S3C6410](http://elinux.org/Android_on_S3C6410)

### Under development

- [Continental AG car navigation system](http://phandroid.com/2009/06/05/android-in-your-car-autolinq-by-continental-ag/)
- [Marvel pad with targeted $100 price](http://www.linuxfordevices.com/c/a/News/Marvell-Moby/?kc=LNXDEVNL032410)
- Google TV

## Development board

- [Devkit8500D](http://www.armkits.com/Product/devkit8500d.asp) TI DM3730 based board
- [Devkit7000](http://www.armkits.com/Product/devkit7000.asp) Samsung S5PV210 based board
- [Mini6410](http://www.minidevs.com/minidevs/Mini6410%20Board.html) [Android_on_S3C6410](http://eLinux.org/Android_on_S3C6410 "Android on S3C6410")
- [MYD-AM335X](http://www.myirtech.com/list.asp?id=466) TI AM335x Development Board

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Porting efforts and issues

> From: [eLinux.org](http://eLinux.org/Android_Porting "http://eLinux.org/Android_Porting")

# Android Porting

This page describes various effort to port Android to new boards and new processors.

## Contents

- 1 Porting Overview
- 2 Porting Tutorials
- 3 Porting Issues
  - 3.1 Android Hardware Abstraction Layer
- 4 Porting to New Processors
- 5 Virtualization environments

## Porting Overview

This overview of porting steps was seen on the android-porting list: See [`www.mail-archive.com/android-porting@googlegroups.com/msg06721.html`](http://www.mail-archive.com/android-porting@googlegroups.com/msg06721.html)

This glosses over all the kernel work for a new board, and the Android-specific kernel patches, but has some good discussion about the flash partitioning and file system bringup process.



## 在 Linux 环境下为设备移植 Android 系统的操作指南

如果 Linux 内核已经启动并运行，且所有驱动程序（特别是触摸屏和显示驱动）都已加载，那么情况应该不会太糟糕。

在我看来，让你尽快运行起来的最简单方法是将内核中构建的初始 `ramfs` 与 Android 构建的根文件系统（`system`）、用户数据分区（挂载为 `/data`）合并为一个单一的根文件系统。

然后你可以将该根文件系统打包为一个 `tarball` 文件。

修改内核的 `NAND` 分区设置，为整个 Android `rootfs` 预留空间，然后重新编译内核。（请确保内核中包含 `yaffs` 支持。）此时不再需要 `ramfs`，只需让内核直接挂载 `mtd2` 作为其根文件系统，该分区将使用 `jffs2` 文件系统。

同时为自己创建一个 `busybox` 根文件系统，并将其制作为 `jffs2` 镜像。

因此，你的 `NAND` 分区结构应类似于以下布局（具体大小需自行决定）：
- `mtd0`：bootloader
- `mtd1`：kernel
- `mtd2`：rootfs (`jffs2`)
- `mtd3`：Android rootfs

擦除 `NAND` 上的所有内容。将标准的 Chumby bootloader 烧写到 `mtd0`，将新内核烧写到 `mtd1`，将 `jffs2` rootfs 镜像烧写到 `mtd2`。

启动设备。希望你能进入命令行提示符。

进入提示符后，将 `mtd3` 以 `yaffs2` 分区格式挂载到 `/mnt/android`。将 Android rootfs 解压到 `/mnt/android` 目录。将 `/mnt/android` 下所有文件的所有者和所属组更改为 `root`（使用 `chown` 和 `chgrp` 命令）。最后，通过 `chroot /mnt/android /init` 切换根目录。

此时，你应该能看到 Android 系统尝试启动。

我知道这需要一定的消化过程，但这更多是你要做的事情的概要。当然，这一过程假设你有能力擦除整个 `NAND` 并写入镜像等，但它应该能帮助你理清在设备上运行 Android 所需的一些要求。

关于你的 bootloader 问题，我建议继续使用现有的。只有当你想让所有东西与恢复系统兼容时（这完全是另一个讨论话题），你才需要修改它。

---

## 移植教程

- [将 Android 移植到新设备](http://www.linuxfordevices.com/c/a/Linux-For-Devices-Articles/Porting-Android-to-a-new-device/)
  - 一篇关于将 Android 移植到 Nokia N810 的出色且详尽的论文。
  - 包含详细的内核更改列表和带注释的差异（diffs）。
- [`wiki.kldp.org/wiki.php/AndroidPortingOnRealTarget`](http://wiki.kldp.org/wiki.php/AndroidPortingOnRealTarget)
- [Android on OMAP](http://eLinux.org/Android_on_OMAP "Android on OMAP") - 出色的教程，涵盖了将 Android 移植到基于 TI OMAP（ARM）处理器的平台时遇到的各种不同问题。
- 一些关于移植到 PXA 开发板的粗略笔记可在以下网址找到：[`letsgoustc.spaces.live.com/blog/cns!89AD27DFB5E249BA!320.entry`](http://letsgoustc.spaces.live.com/blog/cns!89AD27DFB5E249BA!320.entry)
- 添加新设备或更改现有设备配置的指南：[Android Device](http://eLinux.org/Android_Device "Android Device")

## 移植过程中遇到的问题

- Matt Porter（Mentor Graphics 公司）在 [ELC Europe 2009](http://www.embeddedlinuxconference.com/elc_europe09/index.html) 上做了关于将 Android 移植到 MIPS 和 PPC 处理器时遇到的困难的演讲。他的演讲题为“Mythbusters: Android”，包含了很多有价值的信息。
  - 参见 [Mythbusters_Android.pdf](http://eLinux.org/images/2/2d/Mythbusters_Android.pdf "Mythbusters Android.pdf")
- [Dalvik 移植指南](http://android.git.kernel.org/?p=platform/dalvik.git;a=blob_plain;f=docs/porting-guide.html;hb=HEAD)
- Matthias Brugger 在 ELC Europe 2012 上分享了他个人关于移植 Android 的“实战经验”。可在 slideshare 上查看他的[幻灯片](http://www.slideshare.net/MatthiasBrugger/porting-android-40toacustomboard)。

### Android 硬件抽象层 (HAL)

Android 通过其硬件抽象层与标准设备进行通信，该抽象层覆盖了设备的内核接口（例如设备节点、Linux 系统调用等）。要添加对自家硬件的支持，或者特别是为 Android 添加对新型硬件的支持，你需要理解这一抽象层。

Karim Yaghmour 有一篇很好的博客文章描述了 Android HAL 层：[`www.opersys.com/blog/extending-android-hal`](http://www.opersys.com/blog/extending-android-hal)

## 移植到新处理器

- Mentor Graphics 已将 Android 移植到 MIPS 和 PPC 架构。
- Power.Org 支持了将 Android 移植到 PPC 的工作。
  - Nina Wilner 在 ELC Europe 2009 上介绍了这项工作，并进行了演示。
  - 参见 [Android_On_Power.pdf](http://eLinux.org/images/0/07/Android_On_Power.pdf "Android On Power.pdf")

## 虚拟化环境

目前有一些虚拟化环境允许 Android 应用程序（或整个系统）在其他基于 Linux 的系统（如 MeeGo 或 Ubuntu）上运行。

以下是已知存在的不同系统的相关信息：

- OpenMobile ACL（应用程序兼容层）
  - LinuxDevices 文章：[`www.linuxfordevices.com/c/a/News/OpenMobile-ACL-for-MeeGo/?kc=LNXDEVNL092811`](http://www.linuxfordevices.com/c/a/News/OpenMobile-ACL-for-MeeGo/?kc=LNXDEVNL092811)
  - OpenMobile 产品页面：[`openmobile.co/products.php`](http://openmobile.co/products.php)
- Myriad Alien Dalvik
  - LinuxDevices 文章：[`www.linuxfordevices.com/c/a/News/Myriad-Group-Myriad-Alien-Dalvik/`](http://www.linuxfordevices.com/c/a/News/Myriad-Group-Myriad-Alien-Dalvik/)
  - Myriad Group 页面：[`www.myriadgroup.com/Device-Manufacturers/Android-solutions/~/media/D42B513FB5114FF2B4CA13A2D8CE313E.ashx`](http://www.myriadgroup.com/Device-Manufacturers/Android-solutions/~/media/D42B513FB5114FF2B4CA13A2D8CE313E.ashx)
- [FIXTHIS - 应在此处添加关于在 Ubuntu 上运行 Android 的 tetsuyuki 演讲]

[分类](http://eLinux.org/Special:Categories "Special:Categories")：
- [Android](http://eLinux.org/Category:Android "Category:Android")

---

# 获取 Root 权限（越狱）

> 来源：[wikipedia.org](https://en.wikipedia.org/wiki/Rooting_(Android_OS))

## 获取 Root 权限（越狱）

> Rooting 是一个过程，允许智能手机、平板电脑等运行 Android 移动操作系统的用户获得对 Android 各个子系统的特权控制（即 root 访问权限）。由于 Android 使用 Linux 内核，对 Android 设备进行 rooting 类似于在 Linux 或任何其他类似 Unix 的操作系统（如 FreeBSD 或 OS X）上获得管理员权限。

> 

> 进行 rooting 通常是为了克服运营商和硬件制造商对某些设备施加的限制。因此，rooting 使用户能够（或有权）更改或替换系统应用程序和设置，运行需要管理员级别权限的专用应用程序，或执行普通 Android 用户无法进行的其他操作。在 Android 上，rooting 还可以帮助完全移除和替换设备的操作系统，通常是升级到当前操作系统的较新版本。

> 

> Root 访问权限有时与破解运行苹果 iOS 操作系统的设备（越狱）相提并论。然而，这两个概念有所不同。越狱描述的是绕过苹果对最终用户的几种限制：修改操作系统（通过“锁定 bootloader”强制实施）、通过侧载安装非官方批准的应用程序，以及授予用户提升的管理员级权限。只有少数 Android 设备会锁定其 bootloader，许多厂商（如 HTC、Sony、Asus 和 Google）明确提供解锁设备甚至完全替换操作系统的能力。[1][2][3] 类似地，在 Android 设备上，侧载应用程序的能力通常无需 root 权限即可实现。因此，iOS 越狱中与 Android rooting 最直接对应的主要是第三方面，即授予用户超级用户管理权限。

---

# 各种硬件修复



> From: [eLinux.org](http://eLinux.org/Android_Hardware_Fixes "http://eLinux.org/Android_Hardware_Fixes")

# Android Hardware Fixes

## Fixing Android Hardware

### G1 hardware fixes

#### Acceleromters stopped working

If your acceleromters stop working, try the following:

*   Try removing the file `akmd_set.txt` can wake it back up. Word is:
    *   Remove `/data/misc/akmd_set.txt` and reboot your phone (or kill `akmd` process)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Android x86

> From: [eLinux.org](http://eLinux.org/Android_x86 "http://eLinux.org/Android_x86")

# Android x86

Android x86 is a software port to normal **PC**s. [Android x86 Homepage](http://www.android-x86.org/)

The current stable release is [`www.android-x86.org/releases/releasenote-3-2-rc2`](http://www.android-x86.org/releases/releasenote-3-2-rc2) Android-x86 3.2-r2], based upon Honeycomb.

## Contents

*   1 ICS 4.0.3
    *   1.1 Build on ubuntu 11.10
    *   1.2 Hardware
*   2 DONUT 1.6 r2
*   3 short steps to get a running system
    *   3.1 Running the system from boot medium CD or USB-Stick
    *   3.2 run the system from harddisk
*   4 details for a running system
    *   4.1 SD-card
    *   4.2 navigation
    *   4.3 sound
    *   4.4 video
    *   4.5 application errors
*   5 Development
    *   5.1 improvements/request for changes
    *   5.2 errors
    *   5.3 shell
    *   5.4 navigation/keyboard
    *   5.5 File Infos
    *   5.6 hand made changes on an usb-Stick Android 1.6 r2
    *   5.7 sound
    *   5.8 yaffs2 - filesystem
    *   5.9 Links

## ICS 4.0.3

### Build on ubuntu 11.10

see [Building Android 4.0 on Ubuntu 11.10](http://www.android-dev.ro/2011/12/13/building-android-4-0-on-ubuntu-11-10/)

install old version of `gcc` 4.4 with : `sudo apt-get install gcc-4.4 g++-4.4 g++-4.4-multilib gcc-4.4-multilib`

run `make` with : `make CC=gcc-4.4 CXX=g++-4.4 -j4 iso_img TARGET_PRODUCT=generic_x86`

### Hardware

Fritz!Wlan

AVM GmbH AVM Fritz!WLAN N [Atheros AR9001U]

## DONUT 1.6 r2

## short steps to get a running system

### Running the system from boot medium CD or USB-Stick

*   download CD-Image [android-x86-1.6-r2.iso](http://www.android-x86.org/download) or USB-Image [android-x86-1.6-r2_usb.img.gz](http://www.android-x86.org/download)
*   burn cd image or for the usb-image use the following commands on a linux box `gunzip [`www.android-x86.org/download`](http://www.android-x86.org/download)` and `dd if=android-x86-1.6-r2_usb.img of=/dev/sda` (`of=/dev/sda` is depending on where your linux mounted your usb-stick)
*   boot from created medium and choose the first menu entry "Live USB - Run Android-x86 without Installation"
*   in android goto settings/sound & display/screen timeout and set to "never timeout"

### run the system from harddisk

s. as well the [installation section on android-x86.org](http://www.android-x86.org/)

*   boot from CD or USB-Stick android x86 boot menu choose the fourth option "Installation - Install Android-x86 1.6-r2 to harddisk"
*   select "Create/Modify partitions" and create a bootable partition with `cfdisk`
*   select created partition e.g. `sda1` and format with e.g. `ext3`
*   install GRUB by selecting 'yes'
*   reboot system and boot from harddisk and select the default menu entry "Android-x86 1.6-r2"
*   in android goto settings/sound & display/screen timeout and set to "never timeout"

## details for a running system

### SD-card

for mounting an sd card see [[1]](http://www.android-x86.org/documents/sdcardhowto)

### sound

**Keys on ASUS EeePC**

```
Fn-F7, F8, F9,
some models are
Fn-F10, F11, F12 
```

**Notebooks**

```
Some notebooks also have volume adjustment hotkeys 
```

**raise sound volume in shell**

```
* change screen to console 1, press Alt+F1
* enter
  "alsa_amixer cset numid=1 31" for 'Front Playback Volume' and/or
  "alsa_amixer cset numid=20 31" for 'Master Playback Volume'  and/or
  "alsa_amixer cset numid=3 31" for 'Speaker Playback Volume'
* go back to graphic screen,  press Alt+F7 
```

**x86 PCs with normal keyboard**

rear panel audio jack and front panel audio jack depend on the setting of 'Front Playback Volume' `alsa_amixer` sound setting

### video

### application errors

*   menu /settings/about phone/System tutorial -> Sorry! The application settings (process `com.android.settings`) has stopped unexpectedly. Please try again.

## Development

### improvements/request for changes

*   set "settings/sound & display/screen timeout" to "never timeout" as for an x86 system there is no need to timeout an new users don't know what happens.

### errors

### shell

### navigation/keyboard

keyboard layouts see `/system/usr/keylayout/`

command to get events: `getevent`

[Keymaps and Keyboard Input, a detailed description](http://www.kandroid.org/android_pdk/keymaps_keyboard_input.html)

### File Infos

1.  `system.sfs` - squash filesystem
2.  `system.img` - ext2 file Image
3.  `ramdisk.img` - gzip cpio file - extract in an empty folder with `gzip -d \< ramdisk.img |cpio -id`
4.  `initrd.img` - gzip cpio file - extract in an empty folder with `gzip -d \< initrd.img |cpio -id`

### hand made changes on an usb-Stick Android 1.6 r2

**File content of an usb-stick**

```
├── android-system
│   ├── initrd.img
│   ├── install.img
│   ├── kernel
│   ├── ramdisk.img
│   └── system.sfs
├── android-x86.xpm.gz
├── cmdline
├── grub4dos
├── kernel -> grub4dos
├── lost+found
├── menu.lst
└── ramdisk
.
2 directories, 11 files 
```

steps to change files in `system.sfs` (`system.img`)

```
* Ubuntu 10.4 box
* change to shell, press strg+alt+F1
* sudo -i
* aptitude and install squashfs-tools
* modprobe squashfs
* cd /home/administrator
* copy system.sfs (squash file system) to harddisk, in /home/administrator
* mkdir systemsfs
* mount ./system.sfs ./systemsfs -t squashfs -o loop
* copy ./systemsfs/system.img /home/administrator/
* mkdir systemimg
* mount ./system.img ./systemimg -t ext2 -o loop 
```

now cd to `systemimg` directory and make the changes

eg. change `*.kl` files for sound F7 (scanncode=65) = mute; F8 (scanncode=66) = volume_down; F9 (scanncode=67) = volume_up

```
* cd usr/keylayout
* vi *.kl
* change lines
  key 113   VOLUME_MUTE
  key 114   VOLUME_DOWN
  key 115   VOLUME_UP

  key 65   VOLUME_MUTE
  key 66   VOLUME_DOWN
  key 67   VOLUME_UP 
```

### sound

s.

1.  [`wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture`](http://wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture)
2.  [`www.alsa-project.org/main/index.php/Main_Page`](http://www.alsa-project.org/main/index.php/Main_Page)

### yaffs2 - filesystem

```
* download unyaffs2 http://code.google.com/p/yaffs2utils/downloads/list s. description http://code.google.com/p/yaffs2utils/ ; extract to yaffs2util
* download snapshot as described in http://yaffs.net/node/346, extract the source file to directory yaffs2
* change ~/yaffs2util/Makefile with vi and set "KERNELDIR   = /usr/src/linux-headers-2.6.32-21" ; depending on the location of your header files
* execute make
* goto subfolder ~/yaffs2util/src and copy mkyaffs2 and unyaffs2 to /home/administrator/bin
* execute: PATH=$PATH:/home/administrator/bin
* 
```

### Links

[`androidoniphone.blogspot.com/2010/04/install-android-on-iphone-guide.html`](http://androidoniphone.blogspot.com/2010/04/install-android-on-iphone-guide.html) [`android-dls.com/wiki/index.php?title=Main_Page`](http://android-dls.com/wiki/index.php?title=Main_Page)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Applications and Services

> From: [eLinux.org](http://eLinux.org/Android_Applications "http://eLinux.org/Android_Applications")

# Android Applications

This page has some miscellaneous applications and services which may be of interest to developers:

## DLNA



一个快速成长的开源 Android 技术栈是：

*   Cling - [`www.teleal.org/projects/cling/`](http://www.teleal.org/projects/cling/)

或者，你也可以考虑：

*   [`www.cybergarage.org/twiki/bin/view/Main/CyberLinkForJava`](http://www.cybergarage.org/twiki/bin/view/Main/CyberLinkForJava)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Android Derivatives

> 来源：[eLinux.org](http://eLinux.org/Android_Derivatives "http://eLinux.org/Android_Derivatives")

本页面包含有关源自 Android 的系统的信息。

## 为什么选择非 Google Android

*   [`www.reliableembeddedsystems.com/pdfs/2012-07-03-penguin-and-droid.pdf`](http://www.reliableembeddedsystems.com/pdfs/2012-07-03-penguin-and-droid.pdf)

    *   Robert Berger 的演示文稿，讨论非 Google Android 市场

## Cyborgstack

该项目旨在将 Android 系统应用于其他产品类别，包括深度嵌入式领域：

*   网站：[`www.cyborgstack.org`](http://www.cyborgstack.org)

*   Wiki：[`wiki.cyborgstack.org`](http://wiki.cyborgstack.org)

*   GitHub：[`github.com/cyborgstack`](http://github.com/cyborgstack)

*   Twitter：@cyborgstack

*   邮件列表：[`lists.cyborgstack.org/listinfo/dev`](http://lists.cyborgstack.org/listinfo/dev)

### 无头 Android

来源：[`lkml.org/lkml/2012/2/15/443`](https://lkml.org/lkml/2012/2/15/443)

作为参考信息，我认为你们中有些人可能会感兴趣：Android 的用户空间可以被修改以运行在无头系统（即没有帧缓冲）上。也就是说，你可以完全配置掉帧缓冲相关功能，或者使用一个还没有帧缓冲（还？）的内核端口，同时仍然运行 Android 的用户空间。

我已经将其作为 Cyborgstack 项目的一部分放到了这里：

```
$ repo init -u git://github.com/cyborgstack/android.git -b headless
$ repo sync
$ ... 
```

相关的演示文稿来自 Android Builders Summit，可在此处获取：[cyborgstack-120213.pdf](http://eLinux.org/images/6/6f/Cyborgstack-120213.pdf "Cyborgstack-120213.pdf")

本质上，无头 Android 是 AOSP，但**不包含**：

*   `SurfaceFlinger`

*   `WindowManager`

*   `WallpaperService`

*   `InputMethodManager`

它为你提供的是所有 Android 框架，但适用于无 UI 系统（无帧缓冲）。这意味着，除了 `Activities` 之外，你可以使用标准的 Android 开发工具（Eclipse、SDK/NDK 等）来创建使用以下功能的应用程序：

*   `ContentProviders`

*   `Services`

*   `BroadcastReceivers`

为什么你会想要这个而不是使用“嵌入式 Linux”呢？老实说，当一些开发者第一次向我提到他们对此感兴趣时，我非常怀疑。事实上，我非常不以为然。但我不断收到越来越多的关于此事的询问。所以我决定咬紧牙关试一试。

现在我已经试过了，我认为使用这个而不是“嵌入式 Linux”有两个明显的好处：1）你可以获得一个统一平台用于所有设备开发，无论它是否有 UI；2）你的设备可以由任何熟悉 Android API 的开发者进行编程（而且你可能知道，这类开发者的数量正在增长。）

话虽如此，我所做的很大程度上是一个概念验证。实际上，在这一点上它还是一个粗糙的拼凑。请暂时不要发布这个。它需要更多的审查，当然也需要更多的工作。但是，它足以让你尝到可能性的滋味，并允许你进行试验。

干杯，

-- Karim Yaghmour

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# Android 的 Linux 模拟器

> 来源：[eLinux.org](http://eLinux.org/Linux_emulators_for_Android "http://eLinux.org/Linux_emulators_for_Android")

## 另请参阅

*   [KBOX Linux 模拟器用于 Android](http://eLinux.org/KBOX_Linux_emulator_for_Android "KBOX Linux emulator for Android")

# Android 社区

Android 社区相关的新闻、事件、邮件列表、参与者以及面向 Android 开发人员的各类组织。

# News

> 来源：[eLinux.org](http://eLinux.org/Android_News "http://eLinux.org/Android_News")

本页面包含有关 Android 平台的新闻链接。

## 目录

*   1 Android 新闻门户

*   2 访谈

*   3 行业/联盟新闻

    *   3.1 Mentor Graphics 收购 Embedded Alley

    *   3.2 OESF

*   4 软件

    *   4.1 发布

    *   4.2 移植

    *   4.3 视频

*   5 特色

    *   5.1 接口

    *   5.2 应用程序

*   6 手机新闻

*   7 上网本和 MID

## Android 新闻门户

*   [`androidguys.com/`](http://androidguys.com/) - 一般新闻

*   [`androinica.com/`](http://androinica.com/) - Android 博客

## 访谈

*   [Google 的 Rubin：Android “一场革命”](http://news.cnet.com/8301-1023_3-10245994-93.html) - CNet News, 2009年5月

*“Android，谷歌的移动操作系统，并没有为公司带来直接收入，而且可能永远不会——至少直接从系统本身不会。但谷歌移动平台总监 Andy Rubin 认为，谷歌和世界将从任何旨在让更多人接入互联网的设备中受益，并且他不避讳解释为什么为 Android 选择的开源方法最有希望实现这一目标。”*

## 行业/联盟新闻

### Mentor Graphics 收购 Embedded Alley

大型 EDA 公司 Mentor Graphics 于 2009 年 7 月收购了嵌入式 Linux 咨询公司 Embedded Alley。

*   参见 [`www.linuxfordevices.com/c/a/News/Mentor-Graphics-acquires-Embedded-Alley/`](http://www.linuxfordevices.com/c/a/News/Mentor-Graphics-acquires-Embedded-Alley/)

### OESF

开放嵌入式软件基金会（OESF）是一个于 2009 年 2 月在日本成立的 Android 联盟。成立之初包括 23 家公司，并得到了 Google 的支持。

*   参见 [`techon.nikkeibp.co.jp/english/NEWS_EN/20090325/167661/`](http://techon.nikkeibp.co.jp/english/NEWS_EN/20090325/167661/)

## 软件

### 发布

*   [Android SDK 3.0 版本](http://developer.android.com/sdk/android-3.0.html)（Honeycomb）

*   [Android SDK 2.3.3 版本](http://developer.android.com/sdk/android-2.3.3.html)

*   [Android SDK 2.3 版本](http://developer.android.com/sdk/android-2.3.html)（Gingerbread）

*   [Android SDK 2.2 版本](http://developer.android.com/sdk/android-2.2.html)（Froyo）

*   [Android SDK 2.1 版本](http://developer.android.com/sdk/android-2.1.html)（Eclair 2.1）发布（2010年1月12日）

    *   [`www.techtree.com/India/News/Android_21_SDK_Released/551-108663-580.html`](http://www.techtree.com/India/News/Android_21_SDK_Released/551-108663-580.html)

*   [Android 1.6 版本](http://developer.android.com/sdk/android-1.6.html)（Donut）发布（4 版本于 2009 年 12 月发布）

    *   [`developer.android.com/index.html`](http://developer.android.com/index.html)

    *   [`android-developers.blogspot.com/search/label/Android%201.6`](http://android-developers.blogspot.com/search/label/Android%201.6)

    *   [`developer.android.com/sdk/android-1.6-highlights.html`](http://developer.android.com/sdk/android-1.6-highlights.html)

*   [Android 1.5 版本](http://developer.android.com/sdk/android-1.5.html)（Cupcake）发布（2009年4月）

    *   [Android 1.5 “Cupcake” 开始在 G1 上推出](http://www.computerworld.com/action/article.do?command=viewArticleBasic&taxonomyName=mobile_devices&articleId=9132387&taxonomyId=75&intsrc=kc_top) ComputerWorld, 2009年4月30日

    *   [Android 1.5 固件可用](http://lwn.net/Articles/330377/) LWN.net, 2009年4月27日

        *   HTC（Android 开发手机的制造商）已经为 ADP1 发布了一套 Android 1.5 镜像。还有相当简单的说明，介绍如何将这些镜像刷入手机。

### 移植

*   [Android 移植到 MIPS](http://www.linuxdevices.com/news/NS2957041907.html) Linuxdevices, 2009年4月

    *   Embedded Alley 已将 Android 移植到 Alchemy MIPS 处理器。



[Android ported to various ARM processors](http://eLinux.org/Android_on_OMAP#Real_hardware "Android on OMAP")（基于ARM9、ARM11和Cortex-A8）。包括例如`OSK`板、Nokia N800、Nokia N810、[BeagleBoard](http://eLinux.org/BeagleBoard "BeagleBoard")、[Devkit8000](http://eLinux.org/Devkit8000 "Devkit8000")和Gumstix Overo板。

[Devkit7000](http://www.armkits.com/product/devkit7000.asp)基于Samsung S5PV210的板子。

[Devkit8500D](http://www.armkits.com/product/devkit8500d.asp)基于TI DM3730的板子。

### 视频

[基于DM3730运行Android的WLAN和蓝牙演示，详见YouTube](http://www.youtube.com/watch?v=kkhUqVVOpco)

[基于DM3730运行Android的演示，详见YouTube](http://www.youtube.com/watch?v=QnP5f_jfqfE)

[基于Mistral的TMDSEVM3530运行Android的演示，详见YouTube](http://www.youtube.com/watch?v=3MKg8UAxgTE)

[基于Mistral的TMDXEVM3503运行Android的演示，详见YouTube](http://www.youtube.com/watch?v=IuO0YQfjflY)

## 特性

### 界面

*   SenseUI（HTC）
*   MotoBlur（Motorola）
*   TouchWiz（Samsung）
*   Rachael（Sony Ericsson）

### 应用

*   Google Maps（带转弯导航功能）
*   Google Goggles - 通过相机以图搜图
    *   [`www.pcmag.com/article2/0,2817,2356786,00.asp`](http://www.pcmag.com/article2/0,2817,2356786,00.asp)
        *   对Google Goggles的实际体验
*   DoCoMo增强现实概念在Android上运行：[`www.akihabaranews.com/en/news-18527-DoCoMo+Augmented+Reality+Concept+at+Wireless+Japan+09.html`](http://www.akihabaranews.com/en/news-18527-DoCoMo+Augmented+Reality+Concept+at+Wireless+Japan+09.html)

## 手机资讯

*   Samsung手机
    *   [三星的Android手机将在德国上市](http://www.linuxdevices.com/news/NS6111935151.html)，Linuxdevices，2009年4月
*   T-mobile出货超过100万部G1手机
    *   [T-Mobile售出100万部Android手机](http://www.linuxdevices.com/news/NS9441485944.html)，Linuxdevices，2009年4月

## 上网本与MID

*   [据报道，基于ARM的MID运行Android](http://www.linuxdevices.com/news/NS2738659174.html)，Linuxdevices，2009年4月27日
*   [首款Android上网本露面](http://www.linuxdevices.com/news/NS2416044211.html)，Linuxdevices，2009年4月
    *   由Skytone宣布推出基于ARM的上网本

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")

# 活动

> 来源：[eLinux.org](http://eLinux.org/Android_Events "http://eLinux.org/Android_Events")

# Android活动

据我所知（截至2010年1月），涉及Android内容的活动有：

## 目录

*   1 谷歌活动
*   2 Android构建者峰会
*   3 其他非谷歌活动
*   4 Linux活动
*   5 区域活动
*   6 相关会议
*   7 往届活动
    *   7.1 区域活动

## 谷歌活动

*   Google I/O - 参见[Google I/O维基百科词条](http://en.wikipedia.org/wiki/Google_I/O)
    *   2011年的Google I/O于5月10日至11日在旧金山举行
        *   参见[Tims GoogleIO 2011笔记](http://eLinux.org/Tims_GoogleIO_2011_Notes "Tims GoogleIO 2011 Notes")
*   [Google开发者日](http://www.google.com/events/developerday)
    *   有谷歌开发者参与的区域性活动

## Android构建者峰会

这是一个（2011年）面向Android系统开发者的新活动。参与者包括将Android移植到新硬件、从事Android内核或底层基础设施工作，或者以其他方式从事Android本身（而非Android应用程序开发）的开发者。

*   [ABS主页](http://events.linuxfoundation.org/events/android-builders-summit/)
    *   [演讲幻灯片](http://events.linuxfoundation.org/events/android-builders-summit/slides)

## 其他非谷歌活动

*   [Android开放大会](http://androidopen.com/android2011/public/content/about)
    *   10月9日至11日，旧金山
    *   这是O'Reilly主办的活动，似乎旨在覆盖整个Android生态系统。
*   [AnDevCon II](http://www.andevcon.com/AnDevCon_II/index.html) - 11月6日至9日，旧金山
    *   主要涵盖应用程序开发，但也有其他分会场。

## Linux活动

*   [`events.linuxfoundation.org/events/embedded-linux-conference/`](http://events.linuxfoundation.org/events/embedded-linux-conference/) 嵌入式Linux大会
    *   参见[`embeddedlinuxconference.com`](http://embeddedlinuxconference.com)了解多年概览
        *   特别是在ELC Europe 2009和2010期间有Android相关的演讲
        *   参见Matt Porter和Nina Wilner在ELC Europe 2009演讲中的发言
        *   参见Tim Bird的演讲以及ELC Europe 2010演讲中的Android教程
*   部分CELF Japan Jamboree活动包含与Android相关的技术内容
    *   以下活动包含Android演讲：Japan Technical Jamboree 31，Japan Technical Jamboree 34

## 区域活动

即将举行...？

*   [Droidcon London 2010](http://www.droidcon.co.uk/) - 2010年10月28日至29日，伦敦
*   [Droidcon Belgium](http://droidcon.be/) - 下一期为2011年1月21日，布鲁塞尔
*   [`www.android-group.jp/abc2011w/`](http://www.android-group.jp/abc2011w/) Android Bazaar and Conference - 2011年1月9日，东京

## 相关会议

*   [游戏开发者大会](http://www.gdconf.com/)开始出现Android参与
    *   参见[`android-developers.blogspot.com/2010/01/android-at-2010-game-developers.html`](http://android-developers.blogspot.com/2010/01/android-at-2010-game-developers.html)

## 往届活动

*   [Android开发者大会](http://www.andevcon.com/) - 2011年3月7日至9日
    *   这似乎是首个完整的Android开发者活动，主要涵盖应用程序开发，但也有一些系统演讲
    *   在线档案位于???

### 区域活动

*   [`www.android-group.jp/abc2011w/`](http://www.android-group.jp/abc2011w/) Android Bazaar and Conference - 2011年1月9日，东京
*   [Droidcon Belgium](http://droidcon.be/) - 下一期为2011年1月21日，布鲁塞尔
*   [Droidcon London 2010](http://www.droidcon.co.uk/) - 2010年10月28日至29日，伦敦

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Android](http://eLinux.org/Category:Android "Category:Android")
*   [活动](http://eLinux.org/Category:Events "Category:Events")

# 网络/邮件列表目录

> 来源：[eLinux.org](http://eLinux.org/Android_Web_Resources "http://eLinux.org/Android_Web_Resources")

# Android网络资源

## 目录

*   1 网站
    *   1.1 谷歌网站
    *   1.2 社区网站
    *   1.3 其他网站
*   2 邮件列表
    *   2.1 其他列表

## 网站

### 谷歌网站

*   [`developer.android.com/`](http://developer.android.com/) - 主要面向应用程序开发者的网站
    *   [面向应用程序开发者的邮件列表](http://source.android.com/discuss#TOC-Android-application-developer-maili)
*   [`source.android.com/`](http://source.android.com/) - 专用于源代码管理的网站
    *   [用于源码/平台讨论的邮件列表](http://source.android.com/discuss#TOC-Open-source-mailing-lists)

### 社区网站

*   [Android-DLs](http://android-dls.com/)
    *   [Android-DLs wiki](http://android-dls.com/wiki/)
    *   [Android-DLs论坛](http://android-dls.com/forum/)
*   xda-developers
    *   [XDA Developers Dream Android开发论坛](http://forum.xda-developers.com/forumdisplay.php?f=448) - 关于ROM和Android系统开发的大量优质讨论
*   [AndroidCommunity.com](http://androidcommunity.com/)
*   Stack Overflow（[android标签问题](http://stackoverflow.com/questions/tagged/android)）
*   [Android Freeware Lovers](http://www.freewarelovers.com/android) - 社区驱动的开源和免费应用仓库
*   [Android Freeware](http://freeapk.com) Android免费应用或促销应用

### 其他网站



## Android™ on OMAP

- [Android™ on OMAP](http://www.mistralsolutions.com/android)
- [Android Demo on Mistral's TMDSEVM3530 featured on You Tube](http://www.youtube.com/watch?v=3MKg8UAxgTE)
- [Android Demo on Mistral's TMDXEVM3503 featured on You Tube](http://www.youtube.com/watch?v=IuO0YQfjflY)

## Mailing Lists

See [`developer.android.com/community/index.html`](http://developer.android.com/community/index.html) for a list of official Android mailing lists, and instructions for joining these lists.

- [android-platform](http://groups.google.com/group/android-platform)
  - Discussion of user-space Android code, including system libraries, service, public APIs or built-in applications.
- [android-porting](http://groups.google.com/group/android-porting)
  - Toolchains, device-specific customizations, board bring-up and optimizations
- [android-kernel](http://groups.google.com/group/android-kernel)
  - Discussions of Linux kernel and Android-related changes
- [repo-discuss](http://groups.google.com/group/repo-discuss) - Repo and Gerrit discussion
- [android-beginners](http://groups.google.com/group/android-beginners)
  - Beginning users of SDK and getting started with Android development
- [android-developers](http://groups.google.com/group/android-developers)
  - Experienced developers - implementation help, optimizations, etc.
- [android-discuss](http://groups.google.com/group/android-discuss)
  - General discussion of the platform, usage, ideas for new features, etc.
- [android-security-discuss](http://groups.google.com/group/android-security-discuss)
  - Security issues. Please don't disclose vulnerabilities directly on this list.
- [android-security-announce](http://groups.google.com/group/android-security-announce)
  - Low-volume list for security announcements by the Android Security Team.
- [Android Market Help Forum](http://www.google.com/support/forum/p/Android+Market?hl=en)
  - A web-based discussion forum for Android Market questions.

### Other lists

- [android-ndk](http://groups.google.com/group/android-ndk) - Android Native Development Kit (NDK) mailing list
  - List for people working on native code. This list is targeted by Google at supporting developers who are writing native shared libraries to use via JNI from their Java-based applications. You won't get any help using `agcc` or other community-developed native development tools there.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# People

> From: [eLinux.org](http://eLinux.org/Android_People "http://eLinux.org/Android_People")

# Android People

Here are some of the key Android developers you may encounter on mailing lists or at events:

## Google People

See [Google's listing of the Android core technical team](http://source.android.com/project/core-technical-team)

- [Dianne Hackborn](http://www.angryredplanet.com/~hackbod/) - platform programmer, worked on original OpenBinder
- Brian Swetland - lead kernel developer
  - See [`lkml.org/lkml/2009/6/10/397`](http://lkml.org/lkml/2009/6/10/397)
- Arve Hjønnevåg - kernel developer (original submitter of wakelock patches)
- Mike Chan - Droid developer
- Dan Bornstein - Dalvik creator
- Chris DiBona - Open Source Programs Manager at Google

## Non-google People

- Karim Yaghmour - President of [Opersys](http://www.opersys.com), long-time Embedded Linux and Android expert, author and trainer
- Greg Kroah-Hartman - long-time kernel developer, sometimes responds on android-kernel mailing list
- [Tim Riker](http://rikers.org/) [linked-in account](http://www.linkedin.com/in/timriker) - CTO at [Saygus](http://saygus.com/), maker of an Android-based video phone
- Tetsuyuki Kobayashi - Developer at Kyoto MicroComputer. Has an excellent blog with several great articles about Android. [`kobablog.wordpress.com/`](http://kobablog.wordpress.com/)
  - presentation: [Android is not just Java on Linux](http://kobablog.wordpress.com/2011/05/22/android-is-not-just-java-on-linux/)
    - an excellent overview of Android
  - page of presentations by Kobayashi-san: [`www.slideshare.net/tetsu.koba/presentations`](http://www.slideshare.net/tetsu.koba/presentations)

### Hacker community

- Steve Kondik (also known as Cyanogen) - creator and maintainer of the [cyanogenmod](http://www.cyanogenmod.com/) custom images
- Benno - has a blog, provides busybox binary (V.P. of Engineering at Open Kernel Labs)
  - [Android Framework Startup](http://benno.id.au/blog/2007/11/18/android-framework-startup) tutorial on framework startup (and how to change a `ramdisk.img`)
  - [Android - under the hood](http://benno.id.au/blog/2007/11/13/android-under-the-hood) analysis of system startup
  - [list of android articles by Benno](http://benno.id.au/blog/?tag=android)
  - [busybox binary](http://benno.id.au/blog/2007/11/14/android-busybox)
- JesusFreke - Used to make custom system images. Author of `smali`/`baksmali` (dex assembler/disassembler)
  - [JesusFreke's Blog](http://jf.andblogs.net/) (with release anouncements)
  - [smali project page](http://smali.googlecode.com)
- Haykuro - makes custom system images
  - [Haykuro's site](http://haykuro.theiphoneproject.org/) (blog, info)
- Brian Gupta (aka Brandorr) - author of FAQ at Android-DLs
- TheDudeOfLife - makes custom system images
  - [announcement of 1.5 (cupcake) build](http://forum.xda-developers.com/showthread.php?t=507151)
- Others on xda-developers: xmoo, Stericson, dapro, marcusmaximus, manup456

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")

# Organizations

> From: [eLinux.org](http://eLinux.org/Android_Organizations "http://eLinux.org/Android_Organizations")

# Android Organizations

Here are some Android organizations

- [Open Handset Alliance](http://www.openhandsetalliance.com/) - the original group of companies organized by Google to collaborate on Android technologies and delivery

## Regional

- [Korean Android Platform Group](http://www.kapg.org/)
  - Have published (or are endorsing) a book: [Inside Android](http://www.kapg.org/E_Inside_Android)
- [Android Association of Japan](http://www.android-group.jp/) (or Japan Android Group)
- [`www.yokohama.android-pf.org/`](http://www.yokohama.android-pf.org/) Yokohama Android Platform Club

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Android](http://eLinux.org/Category:Android "Category:Android")
