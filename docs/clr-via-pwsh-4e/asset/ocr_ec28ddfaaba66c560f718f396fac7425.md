Main 是公共静态方法，用 IL 代码实现(有的方法可能用本机 CPU 代码实现，比如 x86 代码)。Main 返回类型是 void，无参。构造器(名称始终是 .ctor)是公共方法，也用 IL 代码实现。构造器返回类型是 void，无参，有一个 this 指针(指向调用方法时构造对象的内存)。

强烈建议多试验一下 ILDasm。它提供了丰富的信息。你对自己看到的东西理解得越多，对 CLR 及其功能的理解就越好。本书后面会大量地用到 ILDasm。

为增加趣味性，来看看 Program.exe 程序集的统计信息。在 ILDasm 中选择“视图”|“统计”，会显示以下信息：

```
File size : 3584
  PE header size : 512 (496 used) (14.29%)
  PE additional info : 1411 (39.37%)
  Num.of PE sections : 3
  CLR header size : 72 ( 2.01%)
  CLR meta-data size : 612 (17.08%)
  CLR additional info : 0 ( 0.00%)
  CLR method headers : 2 ( 0.06%)
  Managed code : 20 ( 0.56%)
  Data : 2048 (57.14%)
  Unaccounted : -1093 (-30.50%)

Num.of PE sections : 3
  .text - 1024
  .rsrc - 1536
  .reloc - 512

CLR meta-data size : 612
  Module - 1 (10 bytes)
  TypeDef - 2 (28 bytes) 0 interfaces, 0 explicit layout
  TypeRef - 4 (24 bytes)
  MethodDef - 2 (28 bytes) 0 abstract, 0 native, 2 bodies
  MemberRef - 4 (24 bytes)
  CustomAttribute- 2 (12 bytes)
  Assembly - 1 (22 bytes)
  AssemblyRef - 1 (20 bytes)
  Strings - 184 bytes
  Blobs - 68 bytes
  UserStrings - 8 bytes
  Guids - 16 bytes
  Uncategorized - 168 bytes

CLR method headers : 2
  Num.of method bodies - 2
  Num.of fat headers - 0
  Num.of tiny headers - 2

Managed code : 20
  Ave method size - 10
```

从中可以看出文件大小(字节数)以及文件各部分大小(字节数和百分比)。对于这个如此小的 Program.exe 应用程序，PE 头和元数据占了相当大的比重。事实上，IL 代码只有区区 20 个字节。当然，随着应用程序规模的增大，它会重用大多数类型以及对其他类型和程序集的引用，元数据和头信息在整个文件中的比重越来越小。

> **注意** 顺便说一下，ILDasm.exe 的一个 bug 会影响显示的文件长度。尤其不要相信 Unaccounted 信息。