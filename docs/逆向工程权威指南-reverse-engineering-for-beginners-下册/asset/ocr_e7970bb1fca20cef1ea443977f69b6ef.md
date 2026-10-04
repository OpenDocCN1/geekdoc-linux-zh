```
key= 9 value=LmgasLkvw&fgpgag~uvcrwl. 'mhj
key= 10 value= Olt'tdMwhx'efwbf!tubumn!anvk
key= 11 value= Security device station found
key= 12 value= In#rjvsznuz!(duhdd#r{'whho#gPtme
message #4
key= 14 value= Number of authorized users exceeded
key= 15 value= Ovlmdq!hg!'jukunuhydk!vrbsp!ydbefe
message #5
key= 17 value=`check security device station
key= 18 value=`ijbh'tdMwhx'efwbf!tubuNmm!`,
```

虽然出现了人类类语言的字符串，但是我们还是能够找到英语字符串。

另外，由于程序采用的解密算法是非常简单的XOR算法，所以它的加密函数就不会复杂的到哪去。如果有需要的话，我们甚至可以使用它的算法加密自己的字符串，然后把自制的的密文放在程序里面。

# 78.3 例3: MS-DOS

本例的研究的是一款1995年研发的MS-DOS程序，联络不上开发商。

在之前的那个守孚DOS的时代，所有的MS-DOS程序基本在16位的8086或者80286 CPU上运行。因此此程序是16位程序。这种程序的指令与本书介绍过的汇编指令相同，只是寄存器是16位寄存器，而且指令集略微小了。

MS-DOS系统没有系统启动程序，全部程序都可以访问硬件端口。所以程序中大量出现了OUT/IN指令。就当时的操作系统来说，基本上只有驱动程序才会使用这些指令，而且应用程序已经不能直接访问硬件端口了。

在当时的的技术条件下，访问密码的MS-DOS程序必须直接访问LPT打印机。那么我们就搜索这些端操作指令了：

```
seg030:0034
sent_pro+22p                     out_post proc far ; CODE XREF;
seg030:0034                               ; sent_pro+2Ap ...nseg030:0034
seg030:0034          arg_0          =byteptr 6
```