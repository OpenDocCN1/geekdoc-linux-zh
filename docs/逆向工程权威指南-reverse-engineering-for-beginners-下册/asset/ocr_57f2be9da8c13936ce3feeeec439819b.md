int x=10; //设置默认值

那么对应的代码表现为：

若在IDA里打开对x进行初始化的可执行文件，我们将看到数据段的开头部分看到初始化变量x。紧随其后的空间用于存储样本中的字符串。

用IDA打开7.2节那个没有初始化x的变量，将会看到什么内容？

```
.data:0040FA80          dd ? ; DATA XREF: _main10
.data:0040FA80                   ; _main+22
.data:0040FA84 dword_40FA84 dd ? ; DATA XREF: _memset+1E
.data:0040FA84                   ; unknown_libname_1+28
.data:0040FA88 dword_40FA88 dd ? ; DATA XREF:
.data:0040FA88                   ; _sbh_free_block+5
.data:0040FA8C LPVOID lpMem
.data:0040FA8C lpmB dd ? ; DATA XREF:
___sbh_find_block+B             _sbh_free_block+2BC
.data:0040FA8C                   ; _sbh_free_block+2CA
.data:0040FA90 dword_40FA90 dd ? ; DATA XREF:
.V6_HeapAlloc+13                 ; _calloc_impl+72
.data:0040FA94 dword_40FA94 dd ? ; DATA XREF:
___sbh_free_block+2FE
```

这段代码里有很多“？”标记的变量，这是未初始化的x变量的标记。这意着在程序加载到内存中之后，操作系统将为这些变量分配空间，并填入数字[2]。但是在可执行文件里，这些未初始化的变量不占用内存空间。为了方便使用结构型数据的大型数据，人们刻意做了这种设置。

# 7.2.2 MSVC: x86+0IllyDbg

我们可以在OlyDbg观察数据的数据段的变量。如图7.15所示。