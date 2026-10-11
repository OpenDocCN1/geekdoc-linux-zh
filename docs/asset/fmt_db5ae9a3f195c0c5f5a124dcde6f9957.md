
`<XRoot>//bin/X86 SVGA`

`/etc/X86Config`

`<XRoot>/_lib/X11/X86Config`

`<XRoot>//lib/X11/doc/README.ark`

`<XRoot>//lib/X11/doc/README.ati`

```
SVGA 核心 X 服务器
服务器配置文件
服务器配置文件
ARK 驱动程序的额外文档
ATI weaggaon 驱动程序的额外文档
```

`<XRoot>/lib/doc/X11/README.cirrus`

`<XRoot>/lib/doc/X11/README.trident`

`<XRoot>/lib/doc/X11/README.tseng`

`<XRoot>/lib/doc/X11/README.Oak`

`<XRoot>/lib/doc/X11/README.Video7`

`<XRoot>/lib/doc/X11/README.Wdig`

```
Cirrus 驱动程序的额外文档
Trident 驱动程序的额外文档
ET4000 和 ET3000 驱动程序的额外文档
Oak 驱动程序的额外文档
Video7 驱动程序的额外文档
WD/PVGA 驱动程序的额外文档
```

注意：`<XRoot>` 指 X11 安装树的根目录。

## 参见

+   `X(1)`, `Xserver(1)`, `XFree86(1)`, `XFree86config(4/5)`, `xf86config(1)`, `xvxdt(1)`, `xdm(1)`, `xinit(1)`

## 缺陷

欢迎报告缺陷，应将电子邮件发送至下方地址列表。

# 联系信息

XFree86 源码从 FTP 服务器 XFree86.org 获取。
详情请发送电子邮件至 `XFree86@XFree86.org`。

## 作者

请参阅 `XFree86(1)` 手册。

XFree86 版本 3.1.2

# XF86_VGA16

`XF86_VGA16`—用于 x86 平台 UNIX 的 4 位非加速 X 窗口系统

## 概要

`XF86_VGA16 [:displaynumber] [ option ] ...`

## 描述

`XF86_VGA16` 是用于 VGA 卡的 4 位颜色服务器。此服务器的默认根视觉效果为 StaticColor。它还包含了 `XF86_Mono(1)` 手册中描述的非 VGA 单色卡。它可以在双头配置下运行。

## 配置

`XF86_VGA16` 服务器支持16色模式下的以下流行 VGA 芯片组。

```
18800, 18800-1, 28800-2, 28800-4, 28800-5, 28800-6, 68800CX, 68800LX, 88800CL, 88800GX

- ATI

- Tseng

- Trident

- Cirrus

- Oak

ET4000

TVGA800CS, TVGA800B, TVGA900C, TVGA900CL, CL641, CL642, CL640, OTI067, OTI77, OTI87
```
