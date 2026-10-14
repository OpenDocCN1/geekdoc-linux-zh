
最后一个属性值是`nosearch`。如果菜单项包含`Attribute=nosearch`行，则该项将显示给客户端，但在执行菜单项搜索（如下一节所示）时不会使用其标题。

## 第 5 章：设置 Gopher

菜单中`Attribute=`字段当前允许的值为`invisible`、`gopheronly`、`httponly`、`nosearch`和`gnlink`。在菜单属性行输入时，这些值的大小写不敏感。单个菜单项无法拥有两个属性。

### 向 HTTP 客户端提供项目

有多种方法向 HTTP 客户端提供项目。不同的方法适用于不同的情况。但在所有情况下，这些选择将不会显示给 Gopher 客户端，仅对 HTTP 客户端可用。

也许最简单且自然的方法是使用`httpText=`和`endregion=`关键字。这些关键字为 HTTP 客户端提供任意 HTML，包括超文本链接。

当对象是本地文件时，可以使用`Attribute=httponly`行。这在上一节中讨论过。

另一种方法是使用如下的菜单条目：

```
URLlink=A file for HTTP clients only on a remote server
Url=http://host.name.edu/0/dir/file
```

这为 HTTP 客户端提供了任意对象，包括来自远程服务器的项目。该项目的标题可以使用 HTML，例如：

```
URLlink=file for HTTP clients <<strong>only</strong>&lt;/a> (on remote server)
Url=http://host.name.edu/0/dir/file
```

注意，当使用`URLlink=`时，你必须提供`<A>`超链接终止符，类似于`HName=`行。

## 设置“搜索所有菜单”项目

`gn`的一个内置功能是允许创建一个菜单项，该项在被选中时会提示用户输入搜索词，并返回一个包含该词的所有菜单项的虚拟菜单。事实上，此类项可以出现在任何层级，并返回该服务器上所有菜单的匹配项，或返回所选层级及以下的所有匹配项。

以下是设置方法。在你想让搜索项出现的菜单文件中创建一个如下的条目：

```
Name=Search all menus on this server
Type=7
Path=7c/.cache
```

（如果你希望搜索仅覆盖`/foo/bar/`目录下的项目，则`Path`行应为`Path=7c/foo/bar/.cache`）。现在运行`mkcache`将新的菜单文件转换为`.cache`文件，操作就完成了。`Type`、`Host`和`Port`行是可选的——如果省略它们，`mkcache`将使用默认值或命令行提供的值。当你更改服务器上的任何一个菜单并重新生成`.cache`文件时，`gn`将自动在菜单搜索中反映这些变化。`gn`在`gn`层级结构中的搜索深度有一个最大限制。该值可以通过编辑`config.h`文件并重新编译来更改。

如果你想要搜索的目录树与你想要包含搜索项的菜单不是同一个，那么你需要在两个菜单文件中都放置搜索项：一个放在搜索项应该出现的菜单中，另一个放在要被搜索目录的菜单中（可以通过`Attribute=invisible`将其隐藏）。第一个将搜索项置于客户端的菜单中，第二个则授予服务器执行搜索的权限。

## 压缩文件

如果你愿意，可以将文件以压缩格式保存在服务器上，并在客户端请求时即时解压。你需要一个用于压缩文件的程序和一个用于解压的文件的配套程序。推荐使用 GNU 项目的 `gzip` 和 `zcat`。它们比 UNIX 标准的 `compress` 高效得多。

在配置编译`gn`时，请务必在`config.h`文件中将`#define DECOMPRESS`设置为解压你已压缩程序的路径。该默认值为`/usr/local/bin/zcat`。另一种可能性是`/usr/ucb/uncompress -c`。

如果你想要提供的文件是`rootdir/dir1/bigfile`，首先必须使用`compress`命令对其进行压缩，这将将其替换为`bigfile.gz`或`bigfile.Z`。然后你创建一个如下菜单条目（假设`bigfile`是文本文件且你已经生成了`bigfile.gz`）：

```
Name=All the text in Bigfile
Path=0Z/dir/bigfile.gz
Type=0
```

关键在于`Z`，它是`Path`字段的第二个字符。它表示该文件是压缩的。对于任何压缩的文本文件，`Path`都会以`0Z`（零 Z）开头。文件是如何压缩的或其名称是`bigfile.Z`、`bigfile.gz`还是其他并不重要。你已经通过在`config.h`中指定`DECOMPRESS`程序告诉了`gn`解压缩该文件。

当然，如果`bigfile`是二进制文件，`Path`字段将是`9Z|dir/bigfile.gz`，且`Type`为`9`。对于音频文件，`Path=sZ/dir/bigfile.gz`，`Type=s`等。类型为0、4、5、9和I的文件可以被压缩；结构化文件（`Type 1m`）不能被压缩。

你可能想让用户以压缩格式下载文件。你可以通过像上面带有`Path=0Z/dir|bigfile.gz`的菜单项来提供此选项，并设置另一个菜单项：

```
Name=Bigfile in compressed format
Path=9/dir/bigfile.gz
Type=9
```

注意`Z`，它是`Path`字段的第二个字符。它表示该文件是压缩的。对于任何压缩的文本文件，`Path`都会以`0Z`（零 Z）开头。文件是如何压缩的或其名称是`bigfile.Z`、`bigfile.gz`还是其他并不重要。你已经通过在`config.h`中指定`DECOMPRESS`程序告诉了`gn`解压缩该文件。

## 提供程序的输出

有时让程序返回其输出非常方便。这是通过CGI（通用网关接口标准实现的。脚本名称必须以`.cgi`后缀结尾（或编译时在`config.h`文件中设置的替换），且脚本的任何目录不能以此后缀结尾。这样做的原因是传递给脚本参数的方式特殊。不像前面的示例使用冒号，参数是附加在路径末尾的。要执行带有参数`foo`的上述脚本，你将使用URL：

```
http://host/CGI/dir/script.cgi/foo
```

此URL通常由脚本本身生成，额外的路径信息用于保存状态。你也可以将其放入菜单文件，以便带该参数执行脚本：

```
Name=A CGI script
Path=CGI/dir/script.cgi/foo
```
