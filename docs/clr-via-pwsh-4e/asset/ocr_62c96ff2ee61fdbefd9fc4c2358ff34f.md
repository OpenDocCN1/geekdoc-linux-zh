密钥对，否则即使都生成了名为 OurLibrary 的程序集，公钥/私钥也不可能相同。

到此为止，程序集及其所有文件就可以打包和分发了。

如第 2 章所述，编译器在编译源代码时会检测引用的类型和成员，必须向编译器指定要引用的程序集——C#编译器是用/reference 编译器开关。编译器的一项工作是在最终的托管模块中生成 AssemblyRef 元数据表，其中每个记录项都指明被引用程序集的名称(无路径和扩展名)、版本号、语言文化和公钥信息。

![](bbox=[0.093, 0.24, 0.158, 0.277])

> **重要提示**　由于公钥是很大的数字，而一个程序集可能引用其他大量程序集，所以在最终生成的文件中，相当大一部分会被公钥信息占据。为了节省存储空间，Microsoft 对公钥进行哈希处理，并获取哈希值的最后 8 个字节。AssemblyRef 表实际存储的是这种简化的公钥值(称为“公钥标记”)。开发人员和最终用户一般看到的都是公钥标记，而不是完整公钥。
> 
> 但要注意，CLR 在做出安全或信任决策时，永远都不会使用公钥标记，因为几个公钥可能在哈希处理之后得到同一个公钥标记。

下面是一个简单类库 DLL 文件的 AssemblyRef 元数据信息(使用 ILDasm.exe 获得):

```
AssemblyRef #1 (23000001)
------------------------------------------------------------
Token: 0x23000001
Public Key or Token: b7 7a 5c 56 19 34 e0 89
Name: mscorlib
Version: 4.0.0.0
Major Version: 0x00000004
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
HashValue Blob:
Flags: [none] (00000000)
```

可以看出，这个 DLL 程序集引用了具有以下特性的一個程序集中的类型:

`"MSCorLib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"`

遗憾的是，ILDasm.exe 在本该使用术语“Culture”的地方使用了“Locale”。检查 DLL 程序集的 AssemblyDef 元数据表看到以下内容:

```
Assembly
------------------------------------------------------------
Token: 0x20000001
Name : SomeClassLibrary
Public Key :
Hash Algorithm : 0x00008004
Version: 3.0.0.0
Major Version: 0x00000003
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
Flags : [none] (00000000)
```