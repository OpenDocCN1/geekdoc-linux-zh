
## 15.3.3. 可重定位软件被其他软件引用

这些方法都不太吸引人，不是吗？有些软件确实不太容易进行重定位。通常，以下几点是重定位会出问题的警示信号：

- 软件包含一个或多个必须安装在特定目录中的文件。
- 软件使用相对路径引用系统文件（这实际上只是另一种说法，意味着软件必须安装在特定目录中）。

如果出现这些问题，让软件变得可重定位将非常困难。

即使假设软件被编写为可以放入可重定位包中，问题可能依然存在，这涉及到可重定位软件本身，以及引用该可重定位软件的其他程序。

例如，有时包需要执行其他程序。这可能包括需要发送邮件的备份软件，或需要压缩文件的通信程序。如果这些底层程序是可重定位的，并且没有安装在其他软件包期望的位置，它们将没什么用。

当然，这不是一个常见的问题，但它是可能发生的。对于对构建可重定位包感兴趣的包构建者来说，这是一个需要探索的问题。不幸的是，这种类型的问题往往最难发现。

然而，如果发现某个软件产品是可重定位的，构建可重定位包的具体机制则相当直接。让我们来试一试。

## 15.4. 构建可重定位包

对于这个例子，我们将使用我们久经考验的 cdp1ayer 应用程序。让我们先回顾一下 spec 文件，看看可能存在的问题：

```
""#
# Sample spec file for cdp1ayer app...
#
Summary: A CD player app that rocks!
Name: cdp1ayer
...
%files
%doc README
/usr/local/bin/cdp
/usr/local/bin/cdplay
%doc /usr/local/man/man1/cdp.1
%config /etc/cdp-config"
```

除了 `%files` 列表外，其他一切看起来都没问题。在 `/usr/local/bin` 中有文件，在 `/usr/local/man/man1` 中有手册页，在 `/etc` 中有配置文件。前缀 `/usr/local` 运行得相当好，除了那个 `cdp-config` 文件。

为了这次首次构建，我们将声明该配置文件是不必要的，并将其从 `%files` 列表中移除。然后，我们将添加一行前缀标签，将前缀设置为 `/usr/local`。在这些更改完成后，让我们尝试构建：

```
# rpm -ba cdplayer-1.0.spec
\* Package: cdplayer
\+ umask 022
\+ echo Executing: %prep
Executing: %prep
\+ cd /usr/src/redhat/BUILD
\+ cd /usr/src/redhat/BUILD
\+ rm -rf cdplayer-1.0
\+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
....
Binary Packaging: cdplayer-1.0-1
Package Prefix = usr/local
File doesn’t match prefix (usr/local): /usr/doc/cdplayer-1.0-1
File not found: /usr/doc/cdplayer-1.0-1
Build failed.
```

构建一直正常进行，直到实际创建二进制包的那一步。`Package Prefix = usr/local` 这一行确认 RPM 获取了我们的前缀标签行。但构建停止了——在一个名为 `/usr/doc/cdplayer-1.0-1` 的文件上。但那个文件甚至不在 `%files` 列表中。这是怎么回事？

仔细看看 `%files` 列表。看看这一行：`%doc README?` 在第 13 章的 13.6.1 节“Spec 文件内部”中，我们讨论了 `%doc` 指令如何在 `/usr/doc` 下创建一个目录。那个目录就是导致构建失败的文件——由 `%doc` 指令创建的目录。

让我们暂时将该行从 `%files` 列表中移除，再试一次：

```
# rpm -ba cdplayer-1.0.spec
\* Package: cdplayer
\+ umask 022
\+ echo Executing: %prep
Executing: %prep
\+ cd /usr/src/redhat/BUILD
\+ cd /usr/src/redhat/BUILD
\+ rm -rf cdplayer-1.0
\+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
....
Binary Packaging: cdplayer-1.0-1
Package Prefix = usr/local
Finding dependencies...
Requires (2): libc.so.5 libncurses.so.2.0
bin/cdp
bin/cdplay
man/man1/cdp.1
90 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
\+ umask 022
\+ echo Executing: %clean
Executing: %clean

+ cd /usr/src/redhat/BUILD

+ cd cdplayer-1.0

+ exit 0

Source Packaging: cdplayer-1.0-1

cdplayer-1.0.spec

cdplayer-1.0.tgz

82 blocks

Generating signature: 0

Wrote: /usr/src/redhat/RPMS/i/cdplayer-1.0-1.src.rpm
```

构建正常完成。注意，将要放入二进制包文件中的文件被列出了，但没有前缀 /usr/local。你们中有些人可能想知道为什么 cdp.1 文件没有引起问题。毕竟，它也有一个 %doc 指令。答案在于文件指定的方式。由于文件是使用绝对路径指定的，并且该路径以 /usr/local 开头，所以没有问题。关于 %doc 指令更完整的讨论可以在第 13 章的 13.6.1 节中找到。

### 15.4.1. 善后工作

在构建这个包的过程中，我们遇到了两个障碍：

- 配置文件 cdp-config 无法安装到 /etc。
- README 文件无法使用 %doc 指令打包。

这两个问题都源于这些文件的路径不以默认前缀路径 /usr/local 开头。这意味着这个包不能被重定位吗？可能如此，但有两个选项需要考虑。第一个选项是审查前缀。对于我们的例子，如果我们选择 /usr 而不是 /usr/local 作为前缀，由于默认文档目录是 /usr/doc，README 文件就可以使用 %doc 指令打包。另一种方法是使用 %docdir 指令在前缀路径上的某个位置定义另一个用于存放文档的目录。（关于 %docdir 指令的更多信息，请参见第 13 章的 13.6.2 节。）

这种方法对 /etc/cdp-config 不起作用。为了打包那个文件，我们需要采取更极端的措施。基本上，这种方法将涉及在可接受的目录中打包文件（在 /usr/local 下的某个位置），并使用 %post 安装后脚本将文件移动到 /etc。将符号链接指向配置文件是另一种可能性。

当然，这种方法有一些问题。首先，你需要编写一个 %postun 脚本来撤销 %post 脚本所做的操作。（安装和卸载脚本有一个环境变量 **RPM_INSTALL_PREFIX**，可以用来编写脚本，以便在包被重定位时采取适当的行动。更多信息请参见第 13 章的 13.3.2 节。）一个确保文件就位验证脚本也很不错。其次，由于文件或符号链接不是由 RPM 安装的，RPM 数据库中没有任何关于它的条目。这降低了在发出查询时 `RPM` 的 `-c` 和 `-o` 选项的实用性。最后，如果你确实使用 %post 脚本移动文件，你移动的文件将无法正确验证，并且当包被擦除时，当 RPM 找不到要擦除的移动文件时，你的用户将会收到一些令人不安的信息。如果你不得不诉诸于这些技巧，最好还是放弃让包变得可重定位的念头。

## 15.4.2. 测试可重定位包

看起来 cdplayer 并不是一个适合被重定位的候选对象。然而，由于我们确实成功构建了一个功能受限的版本，我们可以用它来展示如何测试可重定位包。首先，让我们看看二进制包文件的前缀是否被正确记录。我们可以通过使用 RPM 查询模式的 --queryformat 选项来做到这一点：

```
# rpm -q --queryformat '%{DEFAULTPREFIX}\n' cdplayer-1.0-1.i386.rpm
/usr/local
#
```

**DEFAULTPREFIX** 标签指示 RPM 显示构建时使用前缀。我们可以看到，它是 /usr/local，正如我们预期的那样。--queryformat 选项在第 5 章的 5.2.2 节“获取关于包的信息”中进行了讨论。

所以看起来我们有一个可重定位的包。让我们尝试几次安装，看看我们是否真的可以在不同的位置安装它。首先，让我们尝试一次常规安装，不指定前缀：

```
# rpm -Uvh cdplayer-1.0-1.i386.rpm
cdplayer ################################################################
#
```

这似乎运行得足够好。让我们看看文件是否去了我们预期的位置：

```
# ls -a1 /usr/local/bin
total 558
-rwxr-xr-x 1 root root 40739 Oct 7 13:23 cd*
lrwxrwxrwx 1 root root 18 Oct 7 13:40 cdplay -> /usr/local/bin/cdp*
...
# ls -a1 /usr/local/man/man1
total 9
-rwxr-xr-x 1 root root 4550 Oct 7 13:23 cdpl.1*
...
#
```

看起来不错。让我们擦除该包并使用不同的前缀重新安装它：

```
# rpm -e cdplayer
# rpm -Uvh --prefix /usr/foonly/blather cdplayer-1.0-1.i386.rpm
cdplayer ################################################################
#
```

请注意，在安装 cdplayer 之前，目录 foonly 和 blather 并不存在。

