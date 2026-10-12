
```bash
# rpm -evv eject
D: uninstalling record number 286040
D: running preinstall script (if any)
D: removing files test = 0
D: /usr/man/mani/eject.1 - removing
D: /usr/bin/eject - removing
D: running postuninstall script (if any)
D: removing database entry
D: removing name index
D: removing group index
D: removing file index for /usr/bin/eject
D: removing file index for /usr/man/mani/eject.1
#
```

## 3.3 其他选项

尽管 `-v` 没有影响 RPM 的输出，但 `-vv` 我们大量的输出。首先，RPM 显示包的记录号。这个数字只供处理 RPM 数据库的人使用。

接下来，RPM 执行“卸载前”脚本。该脚本可以在实际删除包之前执行任何命令。如果 `files test = 0` 表示 RPM 正在实际删除包。如果是非零，则 RPM 仅执行删除测试。请参阅第 37 页的第 3.3.1 节有关使用 `--test` 选项的更多信息。

两行记录了包的实际删除。具有许多文件的包在使用 `-vv` 时会导致大量输出！

接下来，如果存在，RPM 执行“卸载后”脚本。与卸载前脚本一样，该脚本是为了清理包所需的任何处理。与卸载前脚本不同，卸载后脚本在包的所有文件删除后运行。

最后，最后五行显示了 RPM 从数据库中移除该包的过程。从消息中可以看到数据库包含了某些包数据，后面是每个文件的信息。

如果你对带有许多选项的复杂命令感兴趣，`rpm -e` 不是的地方。删除包的方法有很多！但有几个你应该知道的选项。

### 3.3.1 --test 执行删除包的过程，但不删除它

如果你对删除包有些胆小，可以使用 `--test` 选项先查看 `rpm -e` 会做什么：

```bash
# rpm -e --test bother
removing these packages would break dependencies:
other >= 3.1 is needed by
#
```

很容易看出，如果删除，该包将无法正常工作。但是在这个例子中，除非我们使用了 `--test` 选项，否则 RPM 不会删除包。然而，如果删除包没有问题，你将看不到什么：

```bash
# rpm -e --test eject
#
```

根据以前的经验，我们知道 `-v` 对于 `rpm -e` 没有给我们任何额外的输出。然而，我们知道 `-vv` 效果显著。看看它说什么：

```bash
# rpm -evv --test eject
D: uninstalling record number 286040
D: running preinstall script (if any)
D: would remove files test = 1
D: /usr/man/mani/eject.1 - would remove
D: /usr/bin/eject - would remove
D: running postinstall script (if any)
D: would remove database entry
#
```

你可以看到，输出与使用 `-vv` 的普通命令相似，但例外：

- `would remove files test = 1` 行是非零数字。这是因为添加了 `--test`。如果命令没有包含 `--test`，数字将是 0，包将被删除。
- 对于 RPM 将删除的每个文件都有一行，每行都以 `would remove` 而不是 `removing` 结尾。
- 结尾只有一行，声明：`would remove database entry`，而不是实际删除期间清理 RPM 数据库的多行输出。

将 `--test` 与 `-vv` 使用，可以很容易看到 RPM 在实际删除期间具体会做什么。

### 3.3.2 --nodeps: 删除包之前不检查依赖关系

很有可能某天在删除包时，你会看到这样的内容：

```bash
# rpm -e bother
removing these packages would break dependencies:
other >= 3.1 is needed by
#
```

发生了什么？问题在于系统中安装的一个或多个包需要你正在尝试删除的包。没有它，它们将无法正常工作。在我们的示例中，除非安装了包（具体来说是 3.1 或更高版本），否则该包将无法正常工作。由于我们试图删除它，RPM 要求了删除。

现在，100 次中有 99 次，这正是 RPM 做的正确的事。毕竟，如果包被其他包需要，为什么要删除它呢？与生活中其他事情一样，规则是有例外的。这就是为什么有一个 `--nodeps` 选项。

在删除命令中添加 `--nodeps` 选项指示 RPM 忽略任何与依赖关系的问题并删除包。回到上面的示例，让我们在命令行中添加 `--nodeps` 选项看看发生什么：

```bash
# rpm -e --nodeps
```

包在没有任何声息的情况下被删除了。该包是否能正常工作是另一回事。通常，使用 `--nodeps` 来绕过依赖问题不是一个好主意。包构建者包含依赖关系是有原因的，最好不要质疑它们。

### 3.3.3 --noscript 不执行卸载前和卸载后脚本

在第 36 页的第 3.2.1 节中，我们使用 `-vv` 选项查看 RPM 在删除包时实际做什么。我们注意到有两个脚本，卸载前和卸载后，用于在删除包的过程中执行所需的命令。

`--noscript` 选项防止在删除时执行这些脚本。这是一个非常危险的操作！`--noscript` 选项实际上是供包构建者在开发包时使用的。通过防止卸载前和卸载后脚本运行，包构建者可以防止一个有错误的包搞 own他们的开发系统。一旦发现并消除了错误，很少需要阻止这些脚本运行；事实上，这样做可能会导致问题！

### 3.3.4 --rcfile <rcfile> 读取 <rcfile> 获取 RPM 默认设置

`--rcfile` 选项用于指定包含 RPM 默认设置的文件。通常不需要此选项。默认情况下，RPM 使用 `/etc/rpmrc` 以及位于你登录目录的名为 `.rpmrc` 的文件。

如果需要切换不同的 RPM 默认设置，就会使用此选项。软件开发人员和包构建者通常是唯一使用 `--rcfile` 选项的人。关于 `rpmrc` 文件的更多信息，请参阅第 363 页的附录 B。

### 3.3.5 --root <path> — 使用 <path> 作为根目录

在安装命令中添加 `--root <path>` 会强制 RPM 假设由 `<path>`指定的目录实际上是“根”目录。`--root` 选项会影响安装过程的每一个方面，因此安装前和安装后脚本将以 `<path>` 作为它们的根目录运行（如果你非要知道的话，它们是使用了 `chroot(2)`）。此外，RPM 期望其数据库位于由 `rpmrc` 文件中的 `dbpath` 指定的目录中，且该目录相对于 `<path>`。¹

通常，此选项仅在初始系统安装期间，或者当系统从“救援磁盘”启动且需要重新安装某些包时使用。

### 3.3.6 --dbpath <path>: 使用 <path> 查找 RPM 数据库

为了让 RPM 执行其工作，它需要访问 RPM 数据库。通常，该数据库存在于 `rpmrc` 文件中 `dbpath` 指定的目录中。默认情况下，`dbpath` 设置为 `/var/lib/rpm`。

虽然可以在适当的 `rpmrc` 文件中修改 `dbpath` 条目，但当需要临时更改 `dbpath` 时，`--dbpath` 选项可能是更好的选择。`--dbpath` 选项派上用场的一个例子是需要检查从另一个系统复制的 RPM 数据库时。严格来说，这种情况并不常见，而且很难用其他方式处理。

## 3.4 rpm -e 和 文件

如果你对最初由 RPM 安装的配置文件进行了更改，那么在删除该包时，你的更改不会丢失。例如，假设我们对 `/etc/skel/.bashrc`（一个配置文件）进行了更改，它是作为 `etcksel` 包的一部分安装的。稍后，我们删除了 `etcksel`：

```bash
# rpm -e etcksel
#
ls -al
total 5
drwxr-xr-x 3 root root 1024 Jun 17 22:01 .
drwxr-xr-x 8 root root 2048 Jun 17 19:01 ..
-rw-r--r-- 1 root root 152 Jun 17 21:54 .bashrc.rpmsave
drwxr-xr-x 2 root root 1024 May 13 13:18 .xfm
#
```

但如果我们查看 `/etc/skel`，看看那里有什么：
