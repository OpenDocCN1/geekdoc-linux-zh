

您还可以压缩归档的tar文件。这将生成扩展名为.tar.gz的文件。压缩的归档文件常用于在网络上传输非常大的文件。

```
$ gzip myarch.tar
$ ls
myarch.tar.gz
```

您可以使用调用gzip的tar z选项单独压缩tar文件成员。使用z选项时，tar会在将文件放入归档之前调用gzip对其进行压缩。然而，使用z选项压缩成员的归档无法更新，也不能向其添加内容。所有成员必须同时压缩并同时添加。

## 压缩与解压缩

您还可以使用compress和uncompress命令创建压缩文件。它们生成扩展名为.Z的文件，并使用与gzip不同的压缩格式。compress和uncompress命令使用并不广泛，但您偶尔可能会遇到.Z文件。您可以使用uncompress命令解压缩.Z文件。gzip实用程序是标准的GNU压缩实用程序，应使用它来代替compress。

## 使用bzip2进行压缩

另一个流行的压缩实用程序是bzip2。它使用Burrows-Wheeler块排序文本压缩算法和Huffman编码压缩文件。其命令行选项在设计上与gzip类似，但并不完全相同。有关完整列表，请参阅bzip2手册页。您可以使用bzip2命令压缩文件，并使用bunzip2解压缩。bzip2命令创建扩展名为.bz2的文件。您可以使用bZcat将压缩数据输出到标准输出。bzip2命令按块压缩文件，并允许您指定块的大小（较大的块可提供更高的压缩率）。与gzip一样，您可以使用bzip2压缩tar归档文件。以下示例将mydata文件压缩为扩展名为.bz2的bzip压缩文件：

```
$ bzip2 mydata
$ ls
mydata.bz2
```

要解压缩，请在bzip文件上使用bunzip2命令。

```
$ bunzip2 mydata.bz2
```

## 使用Zip

Zip是一种压缩和归档实用程序，模仿PKZIP设计，PKZIP最初用于DOS系统。Zip是一种跨平台实用程序，可用于Windows、Mac、MS-DOS、OS/2、Unix和Linux系统。Zip命令可以处理由PKZIP和PKZIP程序创建的归档，也可以使用Zip归档。您可以使用zip命令压缩文件，这将创建扩展名为.zip的Zip文件。如果未列出文件，zip会将压缩数据输出到标准输出。您还可以使用-参数让zip从标准输入读取。要压缩目录，请包含-r选项。第一个示例归档并压缩一个文件：

```
$ zip mydata
$ ls
mydata.zip
```

下一个示例归档并压缩reports目录：

```
$ zip -r reports
```

支持全套归档操作。使用-f选项，您可以使用较新版本更新zip归档中的特定文件。-u选项替换或添加文件，-d选项从zip归档中删除文件。还有用于加密文件、DOS到Unix行尾转换以及包含隐藏文件的选项。
要解压缩并提取Zip文件，请使用unzip命令。

```
$ unzip mydata.zip
```

## 应用程序

## 部分

- **第11章**
  办公和数据库应用程序
- **第12章**
  图形工具和多媒体
- **第13章**
  邮件和新闻客户端
- **第14章**
  Web、FTP和Java客户端
- **第15章**
  网络工具

## 章节

## 办公和数据库应用程序

现在有各种各样的办公套件可用于Linux（参见表11-1）。其中包括专业级文字处理器、演示管理器、绘图工具和电子表格。本章介绍可免费获得的版本。Sun已利用StarOffice代码发起了一个开源办公套件的开发。这些应用程序被称为OpenOffice，提供与GNOME集成的办公应用程序。OpenOffice目前是Red Hat支持的主要办公应用程序。KOffice是一个完全免费的办公套件，专为KDE设计。GNOME Office套件将GNOME应用程序集成为一个可免费获得的生产力套件。Ximian正在开发一个专业级办公套件，同时支持KDE和GNOME。您也可以购买商业办公套件，例如Sun的StarOffice 6。

此外，还有各种各样的数据库管理系统可用于Linux。其中包括功能强大、商业级别的数据库管理系统，如Oracle、IBM的DB2和Sybase。大多数可用于Linux的数据库管理系统都设计用于支持大型关系数据库。Red Hat包括MySQL和

## 表11-1
Linux办公套件

| 网站 | 描述 |
|---|---|
| www.openoffice.org | OpenOffice开源办公套件，基于StarOffice |
| www.koffice.org | KOffice套件，适用于KDE |
| www.gnome.org/gnome-office | GNOME Office，适用于GNOME |
| www.ximian.com | Ximian桌面和办公应用程序 |
| www.sun.com/staroffice | StarOffice套件 |
| www.codeweavers.com | CrossOver Office（支持MS Office） |

