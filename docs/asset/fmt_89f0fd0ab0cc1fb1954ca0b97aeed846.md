
### RemapCursorPad
此配置导致 X 服务器发送方向键的键码。这是对 X 协议的轻微违反，但它允许客户端区分这些键。

### SNFFormat `<number> <number> <number> <number>`
SNF（自然格式）字体。由于 SNF 字体没有标准，可以调整以下四个数字以读取大多数 SNF 字体。这四个参数代表以下值，通常在编译时构建到服务器中：

```
BITMAP_BIT_ORDER
IMAGE_BYTE_ORDER
```

例如，为了读取 SCO SNF 字体，在 `Xconfig` 文件中添加此行：

```
SnfFormat 1 0 1 1
```

或者，为了读取来自 Interactive Systems Corp 的兼容 X11 R4 的 SNF 字体，在 `Xconfig` 文件中添加此行：

```
SnfFormat 1 1 4 4
```

### Terminate
导致服务器在最后一个客户端断开连接时退出。通常 `xinit` 在最后一个客户端断开连接后、服务器重置之前杀死 X 服务器。

### Trace`<number>`
打印额外的调试信息。

### VideoRam`<number>`
以 1024 字节为单位指定显卡内存（1 MB 等于值 1024）。X 服务器检测显卡上的内存大小。

### VisualClass`<number>`
使用 `/usr/include/X11/X.h` 中的默认 `VisualClass`，并基于下表：

| VISUAL CLASS | NUMBER |
| --- | --- |
| StaticGray | 0 |
| GrayScale | 1 |
| StaticColor | 2 |
| PseudoColor | 3 |
| TrueColor | 4 |
| DirectColor | 5 |

图 G.2：Visual Classes

在单色显示器上，应在 `Xconfig` 文件中添加行

```
VisualClass 1
```

## G.2 Metro X 配置文件

### G.2.4 模式 (Modes)

`Xconfig` 文件的最后部分是模式数据库（modes）。它包含了各种分辨率的 VESA 计时规范。默认值适用于大多数显卡，可以对其进行微调以使图像居中并调整显示器上的尺寸。大多数 Metro-X 服务器使用此数据库来配置显卡。数字表示 `DisplayConfig` 文件中 `CLOCKS` 行所使用的时钟，并显示了水平和垂直计时值。具体而言，模式的一个示例为：

```
`1024x768*` 65 1024 1092 1220 1344 768 786 791 810
```

下表显示了上一个示例中每个模式数字的定义。

| VALUE | 含义 |
|---|---|
| 1024X768 | 像素屏幕分辨率 |
| 65 | 像素时钟 (MHz) |
| 1024 | 显示的像素 (水平) |
| 1092 | 同步开始 (水平) |
| 1220 | 同步结束 (水平) |
| 1344 | 总计 (水平) |
| 768 | 显示的像素 (垂直) |
| 786 | 同步开始 (垂直) |
| 791 | 同步结束 (垂直) |
| 810 | 总计 (垂直) |

图 G.3：模式定义

这些数字代表电子束在屏幕每垂直刷新一次时遍历的范围。它们决定了图像在屏幕上的位置以及刷新率。

## 调整图像位置

如果屏幕图像没有正确居中或填充显示器屏幕，你可以编辑模式数字。在拉伸或缩小图像之前，请确保图像已居中。你所做的任何调整将在重启 X 服务器后生效。

图像居中：显示的像素（Pixels Displayed）数字必须与所需的物理屏幕分辨率匹配。同步开始（Sync Start）和同步结束（Sync End）数字必须同时以相同的幅度增加或减少（向左或向右；向上或向下），并保持在显示（Displayed）和总计（Total）值的范围内。

- 图像太靠右：要调整太靠右的图像，请增加水平同步开始和水平同步结束的值。
- 图像太靠左：要调整太靠左的图像，请等量减少水平同步开始和水平同步结束的值。例如，要调整太靠左的图像，可以从向两个水平计时数字（同步开始和同步结束）增加 8 开始。确保同步结束数字不超过水平总计值。同样的这种技术也适用于定位：
- 图像太靠下：要调整太靠底部的图像，请减少垂直同步开始和垂直同步结束的值。
- 图像太靠上：要调整太靠顶部的图像，请增加垂直同步开始和垂直同步结束的值。例如，要调整太靠上的图像，可以从向两个垂直计时数字（同步开始和同步结束）增加 8 开始。确保同步结束数字不超过垂直总计值。

拉伸或缩小图像：显示的像素（Pixels Displayed）数字必须与所需的物理屏幕分辨率匹配。通过增加或减少总计（Total）值来拉伸或缩小图像。此外，为了保持中心位置，必须根据变化的总计值的一半等量地增加或减少同步开始（Sync Starts）和同步结束（Sync End）数字。例如，如果你向水平总计值增加了10，那么你也将向水平同步开始值增加5，并向水平同步结束值增加5。

- 图像水平方向太窄：要拉伸水平方向太窄的图像（左右出现额外空间），将水平总计增加 x，然后向水平同步开始和水平结束值都增加 x 的一半。
- 图像垂直方向太窄：要拉伸垂直方向太窄的图像（顶部和底部出现额外空间），将垂直总计增加数量 x，然后向垂直同步开始和垂直同步结束值都增加 x 的一半。
- Metro 水平方向太宽：要缩小水平方向太宽的图像（图像超出了左右），将水平总计减少数量 x，然后从水平开始和水平结束值中各减去 x 的一半。
- Metro 垂直太高：要缩小垂直方向太高的图像（图像超出了上下），将垂直总计减少数量 x，然后从垂直同步和同步结束值中各减去 x 的一半。

## 扩展 (Extensions)

扩展在 `/usr/lib/X11/config` 中配置。大多数扩展是动态加载的；如果需要，它们将自动加载而无需任何手动配置。标记为“ON”的扩展在启动时加载且永卸载。标记为“DYN”的扩展根据 XQuery 调用请求动态加载。这些扩展通过 `list` 或 `xdp` 显示。标记为“OFF”的扩展无法使用，也不会通过 `list` 或 `xdp` 显示。

## 备注

- 多缓冲（Multi-Buffering）和双缓冲（DOUBLE-BUFFER）可以动态加载。它们必须被设置为“ON”或“OFF”。
- GLX (OpenGL)可以动态加载，但 GLX 取决于 DOUBLE-BUFFER 是否“ON”。因此，要使用 GLX，请将 DOUBLE-BUFFER 设置为“ON”并将 GLX 设置为“DYN”。
- X3D (PEX)可以动态加载，但 X3D 取决于 Multi-Buffering 是否“ON”。因此，要使用 X3D，请将 Multi-Buffering 设置为“ON”。

268

Red Hat Linux 常见问题解答

| 镜像站点 | 路径 |
| :--- | :--- |
| ftp.iss.nus.sg | /pub/redhat |
| **南美** | |
| ftp.sunite.dcc.uchile.cl | /pub/OS/linux/redhat |
| **北美** | |
| ftp.kernel.org | /pub/mirrors/redhat |
| sunsite.unc.edu | /pub/linux/distributions/redhat/ |
| tsx-11.mit.edu | /pub/linux/distributions/redhat/ |
| ftp.redhat.com | /pub/linux/distributions/RedHat/ |
| peyote-asesino.nucleu.unam.mx | /linux/redhat-4.1 |
| red.ears.umich.edu | /pub/linux/distributions/redhat |
| linux.aiss.uiuc.edu | /pub/redhat |
| ftp.varearcharch.com | /pub/mirrors/redhat |
| ftp.xtn.net | /pub/linux/redhat |
| ftp-nog.rutgers.edu | /pub/linux/distributions/redhat |
| ftp.interpath.net | /pub/redhat |
| schitzer.case.wisc.edu | /pub/RedHat |
| ftp.engr.uark.edu | /pub/redhat |
| ftp.infomagic.com | /pub/mirrors/RedHat |
| ftp.wgs.com | /pub/linux/redhat |
| ftp.bster.com | /pub/redhat |
| ftp.pht.com | /pub/linux/redhat |
| linux.ucs.indiana.edu | /linux/redhat |
| ftp.ou.edu | /linux/redhat |
