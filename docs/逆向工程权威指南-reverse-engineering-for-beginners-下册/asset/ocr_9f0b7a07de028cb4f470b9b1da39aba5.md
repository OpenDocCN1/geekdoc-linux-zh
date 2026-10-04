这个网站还开发了另一款曼德博集合的研究程序，感兴趣的读者可以访问：http://demonstrations.wolfram.com/IteratesForMandelbrotSet/

+   ○

# 83. 2.2 demo程序

本节将介绍的这个曼德博集合的demo程序，由30条指令、64个字节构成。虽然它的算法与前文的算法一致，但是它用到了很多编程技巧。

整个程序的源代码是公开的。为了让读者阅读，笔者添加了一些注释：

```
1 ; X is column on screen
2 ; Y is row on screen
3
4
5 ; X=0, Y=0                X=319, Y=0
6 ; +=-----------------------
7 ; |
8 ; |
9 ; |
10 ; |
11 ; |
12 ; |
13 ; V
14 ; X=0, Y=199             X=319, Y=199
15
16
17 ; switch to VGA 320*200*256 graphics mode
18 mov al,13h
19 int 10h
20 ; initial BX is 0
21 ; initial DI is 0xFFFE
22 ; DSBX (or DS:0) is pointing to Program Segment Prefix at this
moment
23 ; ... first 4 bytes of which are CD 20 FF 9F
24 les ax, [bx]
25 ; ES:AX=99FFF:20CD
26
27 FillLoop:
28 ; set DX to 0. CWD works as: DX:AX = sign_extend(AX).
29 ; AX here is 0x20CD (at startup) and then 320 (when getting back
after loop),
s30 ; so DX will always be 0.
31 cwd
32 mov ax,di
33 ; AX is current pointer within VGA buffer
```