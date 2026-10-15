

# 打印机驱动及其对 PDL 的处理

如果打印机只支持你需要处理的语言中的一部分怎么办？如果你从网上下载了一个 PostScript 文件，而你的打印机只理解 PCL5E，该怎么办？如果你的打印机不能直接解释 PDF，如何打印 PDF 文件？

一个选择是手工转换文件。你的系统自带了大量转换工具；几乎总有办法把你手头的文件转换成打印机可以打印的格式。浏览器可以将 HTML（或 XHTML）页面转换为 PostScript。OpenOffice 可以将 MS Word 文件转换为 PDF。Ghostscript 可以将 PDF 转换为 PostScript，而 PostScript 又可以转换为几乎任何格式，包括 PCL。

更简单的方法是让你的打印系统为你完成工作。某些系统，例如 CUPS，对需要进行哪些转换有一些内置知识，并且可以自动为你设置转换。

如果需要确定文件使用的是什么 PDL，并且无法从文件名判断（例如 foo.pdf），file 命令可以告诉你（除非文件以一段 PJL 指令开头，在这种情况下 file 只会说“HP Printer Job Language data”）。

将几个打印作业保存为文件而不是发送到打印机，你就可以看到这些语言中的程序是什么样子的。在文本编辑器中花一两分钟浏览每种类型的文件，就能很好地感受到它们之间的差异。（不要直接用 cat 将它们输出到屏幕，因为只有 PostScript 是 ASCII。随机二进制数据往往会让终端模拟器感到困惑。）

## PostScript:

```
%!PS-Adobe-3.0
%BoundingBox: 0 0 612 792
%%Pages: 1
%
% Draw a line around the polygons...
pop pop pop dup 0 setgray 0 0 moveto dup 0 lineto 0.707106781 mul dup
lineto closepath stroke
```

## PDF:

```
%PDF-1.3
%A?A?A?A*
81 0 obj
<<
/Linearized 1
/O 83
/H [ 915 494 ]
/T 125075
>>
endobj
xref
81 24
0000000016 00000 n
A^<8f>
```

## PCL5:

```
^E[&l1o0i10l6ED"&l1X"r0F"&v0n1O"p4300X"%1BDT,-1TR0TD1SP1FT10,50 CF3,1LB...%1A"%c100G"%V2T"&8a0P"[p0X"[p0Y"[10U"[s1p12vsb4148T"&i0 E"p0Y"[c7?920Y"[10U"[s1p12vsb4101T"&a0P"&l06b60E"[9"&a0P"[p0X" p0Y"[p474Y"[p14X"[10U"[s1p12vsb4101T"[p402Y"[p186X"%v0O"[c9 00a0b100g2P"[10U"[p250Y"%v0O"[c900a4b10g2P"[v10"%v0O"[c4a156b100g2 P"[v10"[p251Y"[p187X"%v0O"[c899a154b10g2P"[v10"[p346Y"[p256X
```

## PCL/XL:

```
A"X"B"X"BA"<89>A"@A"<86>A"CA"<8F>AA"@"<85>A"A"<82>HA"@A"@"@A? %AA?CA"A"P"@TimesNewRmnBDA?A?A?UUA?BA?A?Au?BA?A?o<85>A"A"CA" BA7LKA?"@?A?A?A"A"@
```

## 26.9 PPD 文件

当你调用 lpr 在彩色打印机 Pollux 上打印 book.ps 时，lpr 可能会返回并询问你想要打印在什么尺寸的纸上。但等等——系统是如何知道要告诉其客户端 lpr，Pollux 可以在 A4 纸上打印的？它如何知道 Pollux 可以处理 PostScript，如果不能，它应该怎么做？它从哪里找到 Pollux 是彩色打印机的信息？

如果你使用的是 CUPS，所有这些信息都保存在描述打印机属性和功能的 PostScript Printer Description（PPD）文件中。CUPS 守护进程读取其打印机的 PPD，并根据需要将有关它们的信息传递给客户端和过滤器。

PPD 最初是为 Mac 世界开发的，但很快也被 Windows 采用。Mac 和 Windows 打印机驱动程序使用 PPD 文件来确定如何将 PostScript 作业发送到打印机。例如，要求一台在美国销售的单面、黑白打印机打印在欧洲 B4 尺寸纸张上的双面彩色文档是没有意义的。

每台 PostScript 打印机都有厂商创建的自己的 PPD 文件，尽管该文件并不总是很容易找到。检查安装光盘和厂商的网站。

PPD 文件只是文本文件。在文本编辑器中查看一个，就可以看到它包含的类型的信息。在网络上，PPD 甚至可以是远程的——CUPS 客户端可以从相关的 CUPS 服务器获取所需的所有 PPD 信息。

CUPS 还使用 PPD 来描述缺乏 PostScript 解释器的打印机。一个额外的字段就能解决问题。看：

```
$ grep cupsFilter /usr/share/ppd/ghostscript/model/pxlmono.ppd
*cupsFilter: "application/vnd.cups-postscript 100 pstopsxl"
*cupsFilter: "application/vnd.cups-pdf 0 pstopsxl"
```
