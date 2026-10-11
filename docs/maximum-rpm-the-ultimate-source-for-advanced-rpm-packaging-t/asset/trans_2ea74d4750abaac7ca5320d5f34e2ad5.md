

该文件之所以消失，是因为第二个软件包在使用 --replacefiles 选项安装时，替换了第一个软件包中的 /usr/bin/cdp。随后，当第二个软件包被卸载（erase）时，由于 /usr/bin/cdp 文件归属于第二个软件包，因此也被一并删除。如果先卸载的是第一个软件包，那么就不会出现问题，因为 RPM 会意识到第一个软件包的文件已经被删除，从而保留该文件位置不变。

这种状态唯一的问题是，第一个软件包仍处于安装状态，只是缺少 /usr/bin/cdp。这意味着系统中存在一个部分安装的软件包。该怎么办？也许是时候运用你新学到的知识，通过执行 `rpm -i --replacepkgs` 命令来修复第一个软件包了。

## 2.4.5. --nodeps：在安装软件包前不检查依赖项

总有一天会发生这样的事。当你正在安装一个新软件包时，突然安装过程报错（bombs）：

```
# rpm -i blather-7.9-1.1306.rpm
failed dependencies:
        bother >= 3.1 is needed by blather-7.9-1
#
```

发生了什么？问题在于你正在重新安装的软件包需要另一个软件包已安装才能正常工作。在我们的例子中，除非安装了 `bother` 软件包（更具体地说，是 `bother` 版本 3.1 或更高版本），否则 `blather` 软件包无法正常工作。由于我们的系统中根本没有安装合适版本的 `bother`，RPM 终止了 `blather` 的安装。

现在，在 100 次中有 99 次，RPM 这样做是完全正确的。毕竟，如果软件包缺少正常工作所需的一切，为什么要尝试安装它呢？然而，就像生活中其他所有事物一样，规则也有例外。这就是为什么存在 `--nodeps` 选项的原因。

在安装命令中添加 `--nodeps` 选项会指示 RPM 忽略任何依赖关系相关问题，并完成软件包的安装。让我们回到前面的例子，在命令行中添加 `--nodeps` 选项，看看会发生什么：

```
# rpm -i --nodeps blather-7.9-1.1306.rpm
#
```

软件包悄无声息地安装成功了。它是否能正常工作是另一回事，但它确实被安装了。一般来说，使用 `--nodeps` 来绕过依赖性问题并不是一个好主意。软件包构建者包含依赖要求是有原因的，最好不要怀疑他们的判断。

## 2.4.6. --force：大锤

在安装命令中添加 `--force` 相当于说“无论如何都要安装！”。从本质上讲，它向命令添加了 `--replacepkgs` 和 `--replacefiles`。像大锤一样，`--force` 是一种不可抗拒的力量（并非双关语），它能让事情发生。事实上，当使用 `--force` 时，唯一能阻止安装继续进行的是依赖冲突。

就像使用大锤一样，在真正使用 `--force` 之前，务必完全理解为什么需要使用它。

## 2.4.7. --excludedocs：不安装此软件包的文档

RPM 有许多很好的特性。其中之一是 RPM 将安装的文件分为三类：

- 配置文件
- 包含文档的文件
- 所有其他文件

RPM 使用 `--excludedocs` 选项来防止被归类为文档的文件被安装。在下面的例子中，我们知道该软件包包含文档，具体来说是手册页 /usr/man/man1/cdp.1。让我们看看 `--excludedocs` 如何阻止其安装：

```
# rpm -iv --excludedocs cdp-0.33-3.i386.rpm
Installing cdp-0.33-3.i386.rpm
# ls -al /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
#
```

使用 `--excludedocs` 的主要原因是为了节省磁盘空间。节省的量可能相当可观。例如，在一个通过 RPM 安装的 Linux 系统上，可能存在超过 5,000 个文档文件，占用近 50MB 的空间。

如果你愿意，可以将 `--excludedocs` 设为所有安装操作的默认设置。要做到这一点，只需将以下行添加到 `/etc/rpmrc`、你登录目录中的 `.rpmrc`，或使用 `--rcfile` 选项指定的文件中：

```
excludedocs: 1
```

此后，每次运行 `rpm -i` 命令时，它将不会安装任何文档文件。有关 rpmrc 文件的更多信息，请参阅附录 B，“The rpmrc File”。

## 2.4.8. --includedocs：安装此软件包的文档

顾名思义，`--includedocs` 指示 RPM 安装任何标记为文档的文件。通常不需要此选项，除非引用的 `rpmrc` 文件中包含 `excludedocs: 1` 的 `rpmrc` 文件条目。下面是一个示例。请注意，在这个例子中，`/etc/rpmrc` 包含 `excludedocs: 1`，这指示 RPM 不安装文档文件：

```
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
# rpm -iv cdp-0.33-3.i386.rpm
Installing cdp-0.33-3.i386.rpm
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
#
```

在这里，我们检查以确保 `cdp` 的手册页之前不存在于系统中。然后在安装 `cdp` 软件包后，我们发现 `/etc/rpmrc` 中的 `excludedocs: 1` 起到了作用：手册页未被安装。让我们再试一次，这次加上 `--includedocs` 选项：

```
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
# rpm -iv --includedocs cdp-0.33-3.i386.rpm
Installing cdp-0.33-3.i386.rpm
# ls /usr/man/man1/cdp.1
-rw-r--r-- 1 root root 4550 Apr 24 22:37 /usr/man/man1/cdp.1
#
```

`--includedocs` 选项覆盖了 `rpmrc` 文件中的 `excludedocs: 1` 条目，导致 RPM 安装了文档文件。

## 2.4.9. -prefix <path>：如果可能，将软件包重定位到 <path>

一些软件包为安装人员提供了灵活性，让他们可以决定软件包在系统中应安装的位置。这些被称为*可重定位软件包*。可重定位软件包与不可重定位的软件包只有一个区别——默认前缀的定义。因此，确定一个软件包是否可重定位需要额外的一点努力。但这里有一个可以用来查明情况的 RPM 命令：

```bash
rpm -qp --qrfmt "%{defaultprefix}\n" <packagefile>
```

> **NOTE**
> 
> 你可以在第 5 章“获取关于软件包的信息”中找到更多关于 RPM 查询命令的内容。

只需将 *packagefile* 替换为你想要检查的软件包文件名即可。如果软件包不可重定位，你只会看到单词 **(none)**。另一方面，如果命令显示了一个路径，则该软件包是可重定位的。除非另有说明，软件包中的每个文件都将安装在该默认前缀指定的路径下的某个位置。

如果你想指定其他路径怎么办？很简单。只需使用 `--prefix` 选项。让我们试一试：

```
# rpm -qp --qrfmt "%{defaultprefix}\n" cdplayer-1.0.1.i386.rpm
/usr/local
# rpm -i --prefix /tmp/test cdplayer-1.0.1.i386.rpm
#
```

在这里，我们使用魔法查询命令确定 `cdplayer` 软件包是可重定位的。它通常安装在 /usr/local 之下，但我们想把它移动一下。通过添加 `--prefix` 选项，我们能够让软件包安装在 /tmp/test。如果我们查看该目录，我们会看到 RPM 创建了持有该软件包文件所需的所有目录：

```
# ls -lR /tmp/test/
total 2
drwxr-xr-x 2 root root 1024 Dec 16 13:21 bin
drwxr-xr-x 3 root root 1024 Dec 16 13:21 man
/tmp/test/bin:
total 41
-rwxr-xr-x 1 root root 40739 Oct 14 20:25 cdp*
lrwxrwxrwx 1 root root 17 Dec 16 13:21 cdplay -> /tmp/test/bin/cdp*
/tmp/test/man:
total 1
drwxr-xr-x 2 root root 1024 Dec 16 13:21 man1/
/tmp/test/man/man1:
total 5
-rwxr-xr-x 1 root root 4550 Oct 14 20:25 cdp.1*
#
```

## 2.4.10. --noscripts：不执行预安装和后安装脚本

在讨论 `--noscripts` 选项之前，我们需要补充一点背景知识。在第 2.4.1 节中，你看到了使用 `-vv` 选项进行安装的一些输出。可以看到，有两行提到了 preinstall（预安装）和 postinstall（后安装）脚本。在某些软件包安装时，可能需要在该软件包的文件复制到磁盘之前、之后，或者之前和之后执行某些程序。

> **NOTE**
> 
> 可以使用 RPM 的查询命令来查看软件包是否有预安装或后安装脚本。更多信息见第 5 章的 5.2.2 节。

`--noscripts` 选项阻止这些脚本在安装期间执行。这样做非常危险！`--noscripts` 选项实际上是供软件包构建者使用的

