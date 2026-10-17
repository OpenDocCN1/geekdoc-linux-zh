
学者修正了上一个缺陷：使用了平滑过渡的灰度调色板；把整个图形输到了图形缓冲区（第19、20行）；使图像中心与屏幕中心重合（第30行）；绘图结束后等待键盘再次退出（第58~68行）。不过，整个程序大了一倍：它由54条指令构成，文件大小也增长到了105字节。该程序的绘图83.5所示。

![](img/a13a81a53f805f55074b2e5d2ec754b6_317_0.png)

图83.5 者的改进图

- [`Norton Guide`](https://en.wikipedia.org/wiki/Norton_Guide) 是在MS-DOS时代，一种驻内存的TSR程序，与编程语言的编译器提供文本。参考 [`Norton Guide`](https://en.wikipedia.org/wiki/Norton_Guide) 数据库，这种文件如图84所示。
- [`Mandelbrot set`](https://en.wikipedia.org/wiki/Mandelbrot_set) 英文原文是曼德博集合。
- [`Mandelbrot set`](https://en.wikipedia.org/wiki/Mandelbrot_set) 实际上是。
- [`Mandelbrot set`](https://en.wikipedia.org/wiki/Mandelbrot_set) 控制。
- [`Microsoft`](https://www.pouet.net/prod.php?id=5327) 微软全面介绍了数学方面和编码方面的细节，建议阅读：[`Microsoft`](https://msdn.microsoft.com/zh-cn/library/jj63753v=85)。
- [`Mandelbrot set`](https://en.wikipedia.org/wiki/Mandelbrot_set) 初始 `$z_0=0$`，因此前几步运算计算 `$z_1$`。
- [`Mandelbrot set`](https://en.wikipedia.org/wiki/Mandelbrot_set) 修改版下载地址：[`http://beginners.re/examples/mandelbrot/dump.exe`](http://beginners.re/examples/mandelbrot/dump.exe)。

## 84章 基于XOR

| Offset | Col | 0 |
|---|---|---|
| 0000170 | 00 00 00 00 |
| 0000180 | 02 1A 1A 1A 1A 1A 1A 1A |
| 0000190 | 1A 1A 1A 1F 1F 18 31 85 1E 19 |
| 00001A0 | 1A 1A 1A 77 1B 89 55 9A 1E 1A |
| 00001B0 | 1A 1A 1A 75 1A 1A 1A 1A 4A |
| 00001C0 | 1A 1A 1A 96 1A 1A 1A 1A 95 |
| 00001D0 | 1A 1A 1A 8D 1A 1A 1A 1A 1A 82 |
| 00001E0 | 1A 1A 1A 59 4A 4A 53 74 69 68 6E |
| 00001F0 | 73 54 79 6F 7E 48 77 70 73 69 |

为什么说是它是加密文件而非压缩文件呢？我们可以看到数值为`0x1A`的字节（右箭头字符）多次出现，而压缩文件则不会发生这种情况。我们还看到了大量拉丁字符的片段，只是这些字符串不可自然解释。

因为文件多次出现了`0x1A`，所以我们按照加密文件进行处理，并且假设该文件是经异或/`XOR`加密的密。我们可以在`Hiew`里清楚地看到，当使用`0x1A`对每个字节进行异或或运算时，文件里出现了亲切的英语文字。如图84.2所示。

### Hiew.X86.IMG EFU EDITMODE Hiew 8.02 (c) SEN

| X86.IMG | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|
| 0000170: | 00 00 00 00 00 00 00 00 02 49 06 07 00 |
| 0000180: | 18 00 00 00 05 00 4F 73 01 43 00 00 00 | |
| 0000190: | 00 00 00 E5 02 00 28-AF 02 02-F3 E8 02 00 | xd +n0 em |
| 0000200: | 73 60 0D 03 AF 71 03 4F 00 03 54 00 00 | smd rgb OAB T |
| 0000210: | 00 00 00 64 00 00 00 00 00 4E 6E 00 00 | d n |
| 0000220: | 00 00 00 82 00 00 00 00 00 00 00 00 00 | A P |
| 0000230: | 00 00 00 A0 00 00 00 48 00 00 00 00 00 | A I W |
| 0000240: | 00 00 00 43 53 50 49 65 73 74 72 73 74 | CPU Instruct |
| 0000250: | 69 6F 75 28 73 74 74 72 65 67 79 73 74 72 | ion set Register |
| 0000260: | 73 00 50 72 6F 74 65 63 79 6F 6E 20 70 | s Protection Reg, pr |
| 0000270: | 69 76 69 67 65 6C 65 45 73 65 70 74 69 | ivilege Exceptio |
| 0000280: | 63 73 00 41 64 6D 65 73 73 69 6E 20 | ns Addressing mo |
| 0000290: | 64 65 74 73 6F 64 65 73 00 00 00 02 40 | decodes B. K. |
| 0000300: | 00 00 00 00 00 00 00 00 00 00 00 00 00 | | | | |
| 0000310: | 00 00 00 00 00 00 3E 01 03 83 02 04 24 | | | |
| 0000320: | 26 00 00 00 00 00 34-40 00 00 00 00 44 | | | | |
| 0000330: | 00 00 00 00 00 00 48 53 50 75 73 74 72 | FPU Instr |
| 0000340: | 75 63 74 69 6F 6E 73 65 74 72 65 67 69 73 | uction set Regis |
| 0000350: | 74 65 72 73 2C 24 64 61 74 79 70 65 73 00 | ters, data types |
| 0000360: | 02 28 02 00 00 00 00 00 00 00 00 00 00 | ) ) | | | |
| 0000370: | 00 00 00 00 00 00 00 00 00 00-06 04 00 | B | | | |
| 0000380: | 40 5D 08 48 6E 73 74 72 75 63 79 6F 6E | MMX Instruction |
| 0000390: | 73 65 74 20 00 00 00 91 83 00 00 FF FF FF | set | | | |
| 0000400: | FF FF FF 08 00 00 00 00 00 00 00 00 12 | | | | |
| 0000410: | 03 30 16 08 34 73 78-71 00 57-03 D6 10 00 | 4B 42 We-D |
| 0000420: | 00 79 83 68-20 00 96-03 23-00 83 03 00 | ydm KOFS S |
| 0000430: | 29 00 8C 63 25 00 00 01 70 33-32 08 02 | Be- Stable |

84.2 对每个字符进行`XOR`运算是一种初级的加密方法。因为它简单就想不起这种方法，实际的工作中就会遇到这种技术。现在，我们大致理解了`0x1A`出现的原因。在进行异或后，数值为`0`的字符变为`0x1A`的密文。在解密时，我们应当尝试`0~255`之间的数字，再分析一下文件变成什么样子。有关的文件格式，请参见：`http://www.dave.org/orton-guides/file-format/`，加密领域（熵）属于重要的指标。它有一个特性：加密后的明文和密文，其熵不变。本节将介绍使用 `Wolfram Mathematica` 来计算熵。

```
In[1] = BinaryRead["X86.NG"]

Out[2]=52724

In[3]= decrypted = Map[BitXor#, input]

In[4]= Export["X86_decrypted", "Binary"]

Out[5]=52724
```
