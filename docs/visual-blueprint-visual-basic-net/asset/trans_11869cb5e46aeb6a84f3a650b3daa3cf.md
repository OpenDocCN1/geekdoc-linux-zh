

# 访问文件信息

可以使用 IO 命名空间中的 FileInfo 类来浏览文件和目录、删除和移动文件以及修改属性。

要将 FileInfo 类链接到文件，请使用 New 关键字创建该类的一个实例。构造函数接受一个参数，即要访问的路径和文件名。创建类实例后，即可开始访问属性。

DirectoryName 属性返回文件的完整路径。如果要访问该目录的属性，Directory 属性提供对 DirectoryInfo 对象的访问。有关 DirectoryInfo 的更多信息，请参阅“访问目录信息”部分。

Extension 属性返回文件的扩展名，即文件名中最后一个句点后的三字符或四字符扩展名。Name 属性指定不带路径的文件名。FullName 返回包含文件名的完整路径。Length 属性返回一个 Long 值，指定文件中的字节数。Attribute 属性使您能够检索或更改文件的属性。

CreationTime 属性使您能够使用 DateTime 变量检索或更改文件的创建日期和时间。LastAccessTime 属性使您能够检索或更改文件的最近访问时间。LastWriteTime 属性使您能够检索或更改文件的最近写入时间。

Delete 方法永久地从文件系统中删除文件，并且不需要参数。CopyTo 将文件复制到新位置。传递一个字符串作为参数，其中包含新位置的路径。您可以提供要复制到的路径，或复制的新文件名。MoveTo 执行相同操作，只不过该方法将文件复制到新位置并删除原文件。

![](img/d6f772854306e15fb6df39b861a7b541_131_0.png)

- 1. 创建一个新项目或打开现有项目。
- 2. 打开需要执行文件操作的方法或事件。
- 3. 键入 `Dim myFile As New IO.FileInfo("C:\Text.txt")`，将 myFile 替换为变量名，将 C:\Text.txt 替换为文件的完整路径。
- 4. 要修改文件属性，请键入 `myFile.LastWriteTime =`，将 myFile 替换为分配给 FileInfo 类的变量名，将 LastWriteTime 替换为某个属性。
- 5. 键入一个新值。
- 6. 键入代码以使用某个属性。

## 附加说明

Attributes 属性由 FileAttributes 枚举中的常量按位组合而成。您可以使用 Attributes 属性来测试文件是否具有特定属性。要测试文件，请使用 And 运算符与常量组合。要设置文件的属性，请使用 Or 运算符组合多个属性，并将值赋给 Attributes 属性。此处列出了 FileAttributes 中最重要的常量表。完整列表请参阅 Visual Basic .NET 帮助。

### FILEATTRIBUTE 常量：

| 名称 | 说明 |
|---|---|
| Archive | 应用程序使用此属性标记文件以进行备份或删除。 |
| Directory | 文件夹或目录。 |
| Hidden | 常规目录列表不列出此文件。 |
| Normal | 文件是正常的，并且未设置任何其他属性。 |
| ReadOnly | 您不能写入此文件。 |
| System | 该文件是操作系统的一部分。 |

### 示例：

```
Dim file As New IO.FileInfo("c:\test.txt")
' assign attributes
file.Attributes = IO.FileAttributes.Hidden Or IO.FileAttributes.Archive
Dim test As Boolean
' check attributes
test = file.Attributes And IO.FileAttributes.Hidden
```

![](img/d6f772854306e15fb6df39b861a7b541_132_0.png)

7 要对文件执行操作，请键入 `myFile.CopyTo ("C:\NewTest.txt")`，将 myFile 替换为分配给 FileInfo 类的变量名，并将 "C:\NewTest.txt" 替换为 CopyTo 的目标位置。

或者，您可以将步骤 7 中的 CopyTo 替换为 Delete 或 MoveTo。

8 按 F5 运行项目。

FileInfo 类可修改文件属性、访问文件属性，并使用方法执行磁盘操作。

