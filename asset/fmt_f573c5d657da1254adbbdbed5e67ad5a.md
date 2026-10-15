
- 桌面管理系统：由于用户-计算机交互对话的主要仲裁者是桌面管理系统或窗口管理系统，我们随后定义并详细说明这类程序的功能。我们对一个通用窗口管理器 FVWM 进行了功能概述 —— 最常用于所谓的非集成安装中 —— 以让你体验到“原味”窗口管理器的外观和感觉及其功能。我们描述了在 PC-BSD 中使用的 KDE4 桌面管理系统的操作，并对我们基础 UNIX 系统中最重要的桌面管理器实现进行了描述。我们描述并概述了该桌面管理系统中默认的窗口管理器。

- X Window System 客户端应用程序编程：我们随后继续描述如何在更低的操作级别上使用 X Window System，通过给出如何为 X Window System 编写客户端应用程序的基本描述，然后展示使用一些促进此过程的编程工具包。我们给出了各种方法论的基本示例：使用 Xlib/XCB 编程以及使用 PC-BSD 中 KDE4 桌面管理器的 Qt 工具包库编程。

## 22.2.1 用户-应用程序软件交互模型

当你坐在电脑前使用应用程序程序完成特定任务时，你主要关心的是计算机提供的结果。你被屏蔽了计算机如何将你的手和手指的动作转化为这些结果的细节。计算机所经历的过程的一种看法如图 22.1 所示，在图中，你作为用户，利用软件组件的中间设施，无论是在同一工作站本地，还是在网络或互联网上全局，与应用程序一起工作。

本章的基本假设是，图形用户界面 GUI 可以最有效地控制单个用户与运行在独立或联网计算机上的应用程序之间的对话，使用 X Window System 和 UNIX 操作系统的中介。用户对话的组件

![](img/02e070097d401d3bf7de4bf1c470b267_1028_0.png)

with an application program can be simplified to the software component blocks shown in Figure 22.1.

For example, a user presses a mouse button to signify a graphical “pick” in an application window shown on screen. That choice, or event, is recognized by and acted upon by the window manager controlling that window. This event is passed along to the desktop manager, which uses the protocols of the X Window System to pass the request to UNIX. UNIX then passes the request to the application software program for further disposition. Another example is the reverse of the previous one. An application software program generates a request for graphical service, passes this request to UNIX, which in turn passes the request via the X Window System protocols to the desktop manager and window manager to display the graphical request on the screen of the user’s computer.

It is important to note that you can either use the facilities of a nonintegrated GUI system (i.e., one that only uses the functions of a window manager and the X Window System to work within the UNIX environment) or an integrated GUI system, which uses the desktop manager (and perhaps a session manager) as an intermediate software link in the chain shown in Figure 22.1. For example, if you install UNIX on your computer, you may wish to only install the X Window System and a default window manager, such as FVWM. This would constitute a nonintegrated GUI installation. The event generation chain of interactivity as seen in Figure 22.1 would start at the user and proceed through the window manager and then jump to the X Window System. An integrated approach would involve installation of a desktop manager such as KDE4. The event generation chain of interactivity as seen in Figure 22.1 would start at the user and proceed through the window manager, then desktop manager, and then to the X Window System. Most users will use the integrated installation. Section 22.2 deals exclusively with a nonintegrated installation. Section 22.3 deals with an integrated installation.

If you have done a nonintegrated installation of the X Window System and UNIX—for example, by installing TrueOS without a GUI and then built the X Window System from source code or package—and have not specified that the X Window System start automatically when your computer boots up, you must type `startx` at the UNIX command prompt in order for the X Window System and a default window manager to “take control” of your display.

We have done an integrated installation of UNIX, with PC-BSD and the KDE desktop environment. Be advised that when we show a nonintegrated installation example, we are really showing a “mock” installation example, because we started from an integrated environment to begin with!

We do not show the installation of an operating system like TrueOS (which, by default, has a CUI exclusively) with the X Window System and FVWM built on top of it.

## 22.2 BASICS OF THE X WINDOW SYSTEM

### 22.2.1 What is the X Window System Similar to and What Advantage(s) Does it Have?
