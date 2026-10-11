

如您所见，我们已添加了 `%files` 列表，分别用于：

- 主 foo 包
- foo-server 子包
- foo-client 子包
- bazlib 子包

每个包仅包含一个文件。（嘿，我们说过这是一个简单的示例！）如果不需要主包，我们只需删除未命名的 `%files` 列表即可。请记住，即使您没有创建主包，定义在主包前导部分中的标签仍会出现在某处——具体来说，就是在源码包文件中。

让我们来看看 spec 文件中最后一个子包特有的部分：安装和卸载时的脚本。

### 18.4.3. 安装和卸载时的脚本

安装和卸载时的脚本 `%pre`、`%preun`、`%post` 和 `%postun`，都可以使用与 spec 文件其他子包特定部分完全相同的方法进行命名。

用于包验证的脚本 `%verify` 也可以针对特定包进行定义。使用我们示例 spec 文件中的子包结构，最终会得到如下的脚本定义：

```
%pre server
%postun client
%preun -n bazlib
%verifyscript client
```

除了命名方式的变化外，为子包创建脚本时只需要注意一件事。重要的是要考虑不同子包的脚本之间可能相互影响的可能性。当然，即使涉及的包之间没有关联，这也是一项良好的脚本编写实践。

### 18.4.3.1. 回到 Spec 文件

这里我们在 spec 文件中添加了一些脚本。为了避免示例变得过于复杂，我们仅为每个包添加了预安装脚本：

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
Copyright: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junque
%description
This is the long description of the foo app, and the baz library needed to
build it...
%package server
Summary: The foo server
Group: bogus/junque
%description server
This is the long description for the foo server...
%package client
Summary: The foo client
Group: bogus/junque
%description client
This is the long description for the foo client...
%package -n bazlib
Version: 5.6
Summary: The baz library
Group: bogus/junque
%description -n bazlib
This is the long description for the bazlib...
%pre
echo "This is the foo package preinstall script"
%pre server
echo "This is the foo-server subpackage preinstall script"
%pre client
echo "This is the foo-client subpackage preinstall script"
%pre -n bazlib
echo "This is the bazlib subpackage preinstall script"

%files
/usr/local/foo-file

%files server
/usr/local/server-file

%files client
/usr/local/client-file

%files -n bazlib
/usr/local/bazlib-file
```

就预安装脚本而言，这些脚本的功能并不多。但它们允许我们查看如何定义子包特定的脚本。

那些构建过包的人可能已经意识到，我们的 spec 文件缺少某些内容。让我们现在添加那部分。

## 18.5. 构建时脚本：子包无需更改

尽管创建子包会改变 spec 文件的一般结构，但有一个部分不会改变：构建时脚本。这意味着在任何 spec 文件中，只有一套 `%prep`、`%build` 和 `%install` 脚本。

当然，即使 RPM 不要求修改这些脚本，您可能仍需要对其进行一些与子包相关的修改。通常，这些修改涉及执行必要的操作以解包、构建和安装所有软件。例如，如果在打包客户端/服务器软件，必须解包客户端和服务器的软件，然后必须构建并安装客户端和服务器二进制文件。

### 18.5.1. 我们的 Spec 文件：最后看一眼

让我们添加一些构建时脚本，最后看一眼 spec 文件：

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
Copyright: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junque
%description
This is the long description of the foo app, and the baz library needed to build it...
%package server
Summary: The foo server
Group: bogus/junque
%description server
This is the long description for the foo server...
%package client
Summary: The foo client
Group: bogus/junque
%description client
This is the long description for the foo client...
%package -n bazlib
Version: 5.6
Summary: The baz library
Group: bogus/junque
%description -n bazlib
This is the long description for the bazlib...
%prep
%setup
%build
make
%install
make install
%pre
echo "This is the foo package preinstall script"
%pre server
echo "This is the foo-server subpackage preinstall script"
#%pre client
echo "This is the foo-client subpackage preinstall script"
%pre -n bazlib
echo "This is the bazlib subpackage preinstall script"
%files
/usr/local/foo-file
%files server
/usr/local/server-file
%files client
/usr/local/client-file
%files -n bazlib
/usr/local/bazlib-file
```

如您所见，构建时脚本简单得不能再简单了。这是编造示例的优势。更贴近实际应用的 spec 文件无疑会有更有趣的脚本。

## 18.6. 构建子包

现在是时候尝试一下我们的示例 spec 文件了。构建过程与单个包的 spec 文件没有太大不同：

```
# rpm -ba foo-2.7.spec
Package: foo
Package: foo-server
Package: foo-client
Package: bazlib
...
Executing: %prep
...
Executing: %build
...
Executing: %install
...
Executing: special doc
+ cd /usr/src/redhat/BUILD
+ cd foo-2.7
+ DOCDIR=/usr/doc/foo-2.7-1
+ DOCDIR=/usr/doc/foo-server-2.7-1
+ DOCDIR=/usr/doc/foo-client-2.7-1
+ DOCDIR=/usr/doc/bazlib-5.6-1
+ exit 0
Binary Packaging: foo-2.7-1
Finding dependencies...
usr/local/foo-file
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/foo-2.7-1.i386.rpm
Binary Packaging: foo-server-2.7-1
Finding dependencies...
usr/local/server-file
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/foo-server-2.7-1.i386.rpm
Binary Packaging: foo-client-2.7-1
Finding dependencies...
usr/local/client-file
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/foo-client-2.7-1.i386.rpm
Binary Packaging: bazlib-5.6-1
Finding dependencies...
usr/local/bazlib-file
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/bazlib-5.6-1.i386.rpm
...
Source Packaging: foo-2.7-1
foo-2.7.spec
foo-2.7.tgz
4 blocks
Generating signature: 0
Wrote: /usr/src/redhat/SRPMS/foo-2.7-1.src.rpm
#
```

从头开始，我们使用通常的命令启动构建。紧接着命令之后，RPM 指示将从此 spec 文件构建四个包。然后，`%prep`、`%build` 和 `%install` 脚本按常规执行。

接下来，RPM 执行其特殊的内部 `%doc` 脚本，即使我们没有声明任何文件作为文档。值得注意的是，`DOCDIR` 环境变量表明，如果 spec 文件将某些文件声明为文档，RPM 会为每个包创建相应的文档目录。

此时，RPM 创建二进制包。如您所见，每个包包含其 `%files` 列表中定义的文件。

最后，创建源码包文件。它包含 spec 文件和原始源码，与其他任何源码包一样。

一个 spec 文件。一套源码。一条构建命令。四个包（如果把源码包也算上就是五个）。总而言之，这是一笔相当划算的交易，不是吗？

### 18.6.1. 全面查看子包

让我们来看看新创建的包。与其他任何包一样，每个子包都应通过在尚未安装该软件的系统上进行安装来测试。在本节中，我们将指出子包与其非子包对应物之间的区别。

首先，让我们只看看每个包的信息：

```
# rpm -qip foo-2.7-1.i386.rpm
Name          : foo
Version       : 2.7
Release       : 1
Install date  : (none)
Group         : bogus/junque
Size          : 35
Summary       : The foo app, and the baz library needed to build it
Description:
This is the long description of the foo app, and the baz library needed to build it...
```

```
# rpm -qip foo-server-2.7-1.i386.rpm
Name          : foo-server
Version       : 2.7
Release       : 1
Install date  : (none)
Group         : bogus/junque
Size          : 42
Summary       : The foo server
Description:
This is the long description for the foo server...
```

