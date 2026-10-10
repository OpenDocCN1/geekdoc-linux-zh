
## 第18章 ♦ 设置打印服务器 595

### 选择打印机

如果您正在为 `OpenLinux` 系统选择一款新打印机，请选择兼容 `PostScript` 或 `HP LaserJet` 的型号，以便更有可能顺利使用。`PostScript` 语言是 `Linux` 和 `UNIX` 打印的首选格式，多年来一直如此。所有主要的文字产品在 `OpenLinux` 和 `UNIX` 系统上均支持 `PostScript` 打印。

如果您获得 `PostScript` 打印机，则在本地安装打印机时只需选择 `Generic PostScript` 打印机。无需特殊驱动程序。但是，您可能需要确认您的打印机是否支持 `Level 2` 或 `Level 3 PostScript`。虽然大多数当前打印机支持这些级别，但许多较旧的 `Apple` 打印机则不支持。

如果您没有 `PostScript` 打印机，仍有大量打印机定义可供选择，其中之一很可能适用于您。除了 `PostScript` 打印机外，`Ghostscript` 可以支持您的打印机；如果支持，您可以使用该工具进行打印。`Ghostscript`（位于 `http://www.wisc.edu/~ghost/`）是一个 `PostScript` 解释器程序。它可以将 `PostScript` 内容转换为可由多种打印机解释的输出。

## 使用 Webmin 添加打印机

由于 `OpenLinux`（受美国出口限制）未包含加密工具，`Webmin` 的连接不安全。

要在 `OpenLinux` 系统上启用 `Webmin`，您首先需要确保基于 Web 的管理已打开。从 `K` 菜单中，点击 `Settings` -> `COAS System` -> `Daemons`。向下滚动列表并点击 `Web-administration`（使其旁边出现勾选标记）。点击 `OK`。重新启动 `OpenLinux`，`Webmin` 即可使用。

要启动 `Webmin`，请在 Web 浏览器的“转到”或“位置”框中输入以下内容（例如 `Netscape Communicator`）：

```
http://localhost:1000
```

![](img/f0f494d795c6ea03cd25d687dd72914c_628_0.png)

更完整的列表在 `http://www.picante.com/~gtaylor/printer_list.cgi` 上维护。

## 第四部分 ♦ OpenLinux 网络和服务器设置

## 表 18-1

| 供应商 | 完全兼容 | 主要兼容 | 部分兼容 | 完全不兼容 |
| :--- | :--- | :--- | :--- | :--- |
| Brother | HL-10V, HL-660, HL-720, HL-760 | BJ-10e, BJ-20e, BJ-200, B-2500, B-C250, BJ-620, BJ-70, BJ-800, LBP-68i, LPF-311 | BJ-3000, BJ-4000, BJ-4100, BJ-4200, B-C350, BJ-4400, B-C400, B-7000, B-C704, Stylus Color 800, Stylus Color 350, Stylus Color 750 | BJC-4550, MULTIPASS, C2500, MULTIPASS, Stylus Color 740, Stylus Photo 750 | BJC-5000, LBP-460, LBP-660 |
