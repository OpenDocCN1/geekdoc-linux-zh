
```bash
# rpm -ba --buildroot /tmp/foonly cdplayer-1.0.spec
* 软件包: cdplayer
执行: %prep
+ cd /usr/src/redhat/BUILD
...
+ exit 0
执行: %build
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
...
+ exit 0
+ umask 022
执行: %install
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ make ROOT=/tmp/foonly install
install -m 755 -o 0 -g 0 -d /tmp/foonly/usr/local/bin/
install -m 755 -o 0 -g 0 cdp /tmp/foonly/usr/local/bin/
rm -f /tmp/foonly/usr/local/bin/cdplay
ln -s /tmp/foonly/usr/local/bin/cdp /tmp/foonly/usr/local/bin/cdplay
install -m 755 -o 0 -g 0 -d /tmp/foonly/usr/man/
install -m 755 -o 0 -g 0 cdp.1 /tmp/foonly/usr/local/man/man1/
+ exit 0
执行: 特殊文档
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ DOCDIR=/tmp/foonly//usr/doc/cdplayer-1.0-1
+ rm -rf /tmp/foonly//usr/doc/cdplayer-1.0-1
+ mkdir -p /tmp/foonly//usr/doc/cdplayer-1.0-1
+ cp -a README /tmp/foonly//usr/doc/cdplayer-1.0-1
+ exit 0
二进制软件包封装: cdplayer-1.0-1
正在查找依赖项...
Requires (2): libc.so.5 libncurses.so.2.0
usr/doc/cdplayer-1.0-1
usr/doc/cdplayer-1.0-1/README
usr/local/bin/cdp
usr/local/bin/cdplay
usr/local/man/man1/cdp.1
93 块
生成签名: 0
已写入: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
+ umask 022
+ echo 执行: %clean
执行: %clean
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ exit 0
源软件包封装: cdplayer-1.0-1
cdplayer-1.0.spec
cdplayer-1.0.tgz
82 块
生成签名: 0
已写入: /usr/src/redhat/RPMS/cdplayer-1.0-1.src.rpm
```

正如经过略微编辑的输出所示，`%prep`、`%build` 和 `%install` 部分是在 RPM 的正常构建目录中执行的。然而，当执行 `make install` 时，`--buildroot` 选项开始发挥作用。我们可以看到，`ROOT` 变量被设置为 `/tmp/foonly`，这是命令行中 `--buildroot` 后面的值。从那时起，我们可以看到 `make` 在安装阶段替换了新的构建根值。

构建根也用于安装文档文件。文档目录 `cdplayer-1.0-1` 在 `/tmp/foonly/usr/doc` 中创建，并且 `README` 文件被放置在其中。

使用 `--buildroot` 导致的唯一剩余差异是，要包含在二进制软件包中的文件不相对于构建系统的根目录定位。相反，它们相对于构建根 `/tmp/foonly` 定位。生成的二进制软件包和源软件包文件在功能上等效于不使用 `--buildroot` 构建的软件包。

### 12.1.13.1. 使用 --buildroot 可能会反噬你！

虽然 `--buildroot` 选项可以解决一些问题，但使用构建根实际上可能是危险的。为什么？考虑以下情况：

- 一个 spec 文件被配置为使用构建根 `/tmp/blather`，例如。
- 在 `%prep` 部分（或 `%clean` 部分；这并不重要——最终结果相同），有一个 `rm -rf $RPM_BUILD_ROOT` 命令用于清理任何旧的安装软件。
- 你决定构建软件，使其相对于系统根目录安装，因此你输入以下命令：`rpm -ba --buildroot / foo.spec`。

结果如何？由于将 `/` 指定为构建根会将 `RPM_BUILD_ROOT` 设置为 `/`，那个看似无害的 `rm -rf $RPM_BUILD_ROOT` 变成了 `rm -rf /`！从系统根目录开始的递归删除，如果你能及时发现，可能不会造成彻底灾难，但在任何情况下，你都要测试自己从备份恢复的能力（嗯，你有备份吧，对吧？）。

这个故事的教训是在使用 `--buildroot` 时要非常小心。一个好的经验法则是始终指定一个唯一的构建根。例如，不要指定 `/tmp` 作为构建根（可能会丢失系统用于存放临时文件的目录），而是使用路径 `/tmp/mypackage`，其中目录 `mypackage` 仅由你正在构建的软件包使用。

### 12.1.14. `--timecheck <secs>`：如果待打包的文件比 `<secs>` 旧，则打印警告

虽然可以使用 `rpm -bi` 检测 `%files` 列表中的许多错误，但还有另一类问题无法被检测。考虑以下场景：

- 你正在构建的一个软件包创建文件 `/usr/bin/foo`。
- 由于软件包 makefile 中的问题，`foo` 从未被复制到 `/usr/bin`。
- 一个较旧的、不兼容的 `foo` 版本，几个月前创建，已经存在于 `/usr/bin` 中。
- RPM 创建二进制软件包文件。

不兼容的 `/usr/bin/foo` 是否包含在软件包中？绝对是！如果 RPM 有某种方式可以捕捉到这类问题就好了。

好吧，有的！如果你添加 `--timecheck`，后面跟一个数字，RPM 将检查每个正在打包的文件，看该文件是否比指定的秒数更旧。如果是，将显示一条警告消息。`--timecheck` 选项可以与 `-ba` 或 `-bi` 选项一起使用。这里是一个使用 `-bi` 的示例：

```bash
# rpm -bi --timecheck 3600 ccdplayer-1.0.spec
* 软件包: ccdplayer
文件列表检查: ccdplayer-1.0-1
警告: TIMECHECK 失败: /usr/doc/ccdplayer-1.0-1/README
正在查找依赖项 ...
Requires (2): libc.so.5 libncurses.so.2.0
```

在这个示例中，文件 `/usr/doc/ccdplayer-1.0-1/README` 比 3,600 秒或 1 小时更旧。如果我们查看该文件，我们会发现它如下所示（注意软件包构建时间远晚于 1995 年 11 月）：

```bash
# ls -al /usr/doc/ccdplayer-1.0-1/README
-rw-r--r-- 1 root root 1885 Nov 10 1995 README
```

在这种情况下，来自 `--timecheck` 的警告无需惊慌。由于 `README` 文件只是从原始源代码复制而来，而该源代码创建于 1995 年 11 月 10 日，其日期未变。如果该文件是一个可执行文件 or 库，且假定是最近构建的，那么 `--timecheck` 的警告应更受重视。

如果你希望将默认时间检查值设置为一小时，你可以在 `rpmmac` 文件中包含以下行：

```text
timecheck: 3600
```

如果需要，此值仍可通过命令行上的值进行覆盖。有关使用 `rpmmac` 文件的更多信息，请参阅附录 B，《`rpmmac` 文件》。

### 12.1.15. `-vv`：显示调试信息

与其他大多数 `RPM` 命令不同，`rpm -b` 没有 `-v` 选项。这是因为该命令的默认行为是冗长的。然而，通过添加 `-vv` 可以获得更多信息。这里是一个示例：
