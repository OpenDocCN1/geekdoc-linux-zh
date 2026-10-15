
关键在于，所有系统都将始终获得设备基本功能的单一 `INF`。`Extension INF(s)` 然后可以对驱动程序进行任何针对特定系统或平台的专门配置。假设你有需要为特定 `OEM` 应用的特殊品牌。或者，你想在支持的特定型号设备上启用某些增值功能。你可以从 `Extension INF` 中完成所有这些工作。你为每个想要支持的独特系统类型或变体编写一个 `Extension INF`。在安装过程中，`Windows` 会调用正确的 `INF` 来执行你的定制。好的一点是，`Base INF` 和 `Extension INF` 可以分别更新（并通过 `WU` 分发）。因此，亲爱的驱动程序编写者，你可以先让你的 `Base INF` 正常工作，而你的 `OEM` 客户可以在稍后某个时间点通过流程设置他们想要的 `Extension INF`。

组件化安装和 `Extension INF` 在 `MSDN` 上有关 `Extension INF` 的文档中有更详细的解释。

## And Then There Are... Hardware Support Apps

你听说过 `Windows 10 S` 吗？那是“锁定”版本的 `Windows`，只能运行来自商店的应用程序。这意味着只能运行 `UWP` —— 而不是 `Win32` —— 应用程序

![](img/feabf7ef0b3bb3419a0ef4d863642d48_13_0.png)

## Universal Drivers... (Cont.)

are supported. Regardless of what you think about this, Microsoft says they’re going to sell these systems. And, if I had to guess, there’ll be other systems in the future that will have the same restrictions.

Suppose you currently have a `Device Manager` property sheet, or `Control Panel Applet`, that’s used to manage your device. That’s not going to work very well on a system that doesn’t support the `Win32 API`, right? So, the final part of the Universal Driver picture is Hardware Support Apps that are written as `UWP` apps. Of course, that’s not nearly as simple as it might seem at first blush. `UWP` has some pretty significant limitations: No `IOCTLs`, no `WMI`, no `RPC`. About the only cool technology that you can use in a `UWP` app is `ETW`.

In place of device-specific `IOCTLs`, `UWP` offers something called `Custom Capabilities`. These are specific functions your driver authorizes to specific applications. And, in this way, everything is supposed to be kept safe.

I’m not convinced. I’m not a fan of the whole `UWP` programming model in general (I’m a device guy… I don’t like being told what I can and cannot do). But I admit it: I really haven’t spent much time investigating the whole issue of `Custom Capabilities` for `UWP` apps. Maybe it’s not as bad as I think. I’ll look into it, and write an article that describes what I find in a future issue of The NT Insider. In the meantime, you can read (and weep) more about `Custom Capabilities` for Hardware Support Apps in `MSDN`.

Note that there’s an interesting side-effect of making a support app a `UWP` app. That app can now be pulled-down during the install (and also during future updates) from the `Windows Store`. You can also, optionally, pre-populate the app onto a specific install image using `DISM`. But in either case, the app will no longer be part of what we think of today as the traditional installer package. This does sound to me like it might make servicing easier.

## Gimmie a D! Gimmie a C! Gimmie a H! Gimmie a U! What’s That Spell?

It spells “`DCHU`.” No, you can’t pronounce it. It stands for:

- Declarative – You use a Declarative `INF` file
- Componentized – You separate your `INF` into a `Base INF` and zero or more `Extension INFs`
- Hardware Support Apps – Written at a `UWP` app, of course
- Universal – Your driver (and `INF`) is restricted to the Universal feature set

![](img/feabf7ef0b3bb3419a0ef4d863642d48_14_0.png)

Together, Microsoft describes these as the Universal Driver Pillars. See the lovely artwork I stole from somebody’s WinHEC deck in Figure 3.

For your driver to be truly able to run on “any Windows platform” you need to embrace all four of the `DCHU` design principles.

## Universal DDIs – Only Part of the Story

Now, hopefully, you see that writing a driver that’s restricted to the Universal `DDIs` is straight forward, but it’s also only part of the story. If you truly want your driver to be installable on any Windows system (now and in the future) you’re going to have to become `DCHU` compliant. Of course, how important any of this is to you will depend greatly on the type of drivers you write and the types of hardware you support.

Be aware that there are rumblings that `DCHU` compliance will become required for certain classes of drivers in the not too distant future. While that remains to be seen, at least the direction that Microsoft wants us to move is clear.
