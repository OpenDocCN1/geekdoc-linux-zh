

在这种情况下，eject 包已被移除。反馈信息并不多，不是吗？如果添加 -v，我们能获得更多反馈吗？

```
# rpm -ev eject
#
```

仍然没有任何输出。不过，另一个选项可以提供大量信息。您将在下一节中了解该选项。

## 3.2.1. 使用 -vv 获取更多信息

通过在命令行中添加 -vv，我们通常能更好地感受 RPM 内部正在发生的事情。-vv 选项实际上是专为 RPM 开发人员设计的，其输出可能会变化，但它是深入了解 RPM 内部运行机制的绝佳方式。让我们用 rpm -e 来尝试一下：

```
# rpm -evv eject
D: uninstalling record number 286040
D: running preuninstall script (if any)
D: removing files test = 0
D: /usr/man/man1/eject.1 - removing
D: /usr/bin/eject - removing
D: running postuninstall script (if any)
D: removing database entry
D: removing name index
D: removing group index
D: removing file index for /usr/bin/eject
D: removing file index for /usr/man/man1/eject.1
#
```

虽然 -v 对 RPM 的输出没有影响，但 -vv 提供了大量的输出。但它告诉了我们什么？

首先，RPM 显示了包的记录编号。该编号通常只对处理 RPM 数据库代码的人员有用。

其次，RPM 会执行预卸载脚本（如果存在）。该脚本可以执行在真正删除文件之前移除包所需的任何命令。

files test = 0 这一行表明 RPM 将实际移除该包。如果该数字非零，RPM 仅会测试包的移除操作。这在使用 --test 选项时发生。有关使用 rpm -e 时 --test 选项的更多信息，请参阅第 3.3.1 节。

接下来的两行记录了组成该包的文件被实际删除的过程。包含许多文件的包在使用 -vv 时可能会产生大量输出。

接着，RPM 会执行后卸载脚本（如果存在）。与预卸载脚本类似，该脚本用于执行彻底移除包所需的任何处理。然而，与预卸载脚本不同，后卸载脚本在所有包的文件被移除之后才运行。

最后，最后五行展示了 RPM 从其数据库中移除该包所有痕迹的过程。从这些消息中，我们可以看到数据库包含一些每个包的数据，随后是关于该包安装的所有文件的信息。

## 3.3. 其他选项

如果您对包含大量选项的复杂命令感兴趣，`rpm -e` 并不是查找此类命令的地方。毕竟移除包的方式并不那么多！但还是有一些选项您应该了解。

### 3.3.1. --test: 执行移除包的过程，但实际不移除

如果您对移除包有些顾虑，可以先使用 `--test` 选项来查看 `rpm -e` 会执行什么操作：

```
# rpm -e --test bothér
removing these packages would break dependencies:
bothér >= 3.1 is needed by blather-7.9.1
#
```

很容易看出，如果 bothér 被移除，blather 包将无法正常工作。不过公平地说，除非使用 --noupdeps 选项（我们将在稍后讨论），否则 RPM 在这个例子中不会移除该包。

然而，如果移除包没有遇到问题，您看到的输出将很少：

```
# rpm -e --test eject
#
```

根据之前的经验，我们知道在 `rpm -e` 中 `-v` 不会提供额外的输出。但我们知道 `-vv` 效果显著。让我们看看它会说什么：

```
# rpm -evv --test eject
D: uninstalling record number 286040
D: running preuninstall script (if any)
D: would remove files test = 1
D: /usr/man/man1/eject.1 - would remove
D: /usr/bin/eject - would remove
D: running postuninstall script (if any)
D: would remove database entry
#
```

如您所见，输出与使用 `-vv` 选项的常规移除命令类似，但有以下例外：

- `would remove files test = 1` 这一行以非零数字结尾。这是因为添加了 `--test`。如果命令中未包含 `--test`，该数字将为 0，并且包将被移除。
- 对于 RPM 本会移除的每个文件，都有一行记录，每一行都以 `would remove` 而非 `removing` 结尾。
- 结尾只有一行，显示 `would remove database entry`，而在实际移除过程中，会显示多行输出以展示 RPM 数据库的清理过程。

通过使用 `--test` 结合 `-vv`，很容易看出在实际移除过程中 RPM 会执行哪些操作。

### 3.3.2. --nodeps: 在移除包前不检查依赖项

很可能在移除某个包时，您会看到类似这样的信息：

```
# rpm -e bother
removing these packages would break dependencies:
bother >= 3.1 is needed by blather-7.9-1
#
```

发生了什么？问题在于系统上安装的一个或多个包需要您试图移除的包。没有它，那些包将无法正常工作。在我们的例子中，除非安装了 `bother` 包（更具体地说，是 3.1 或更高版本的 `bother`），否则 `blather` 包将无法正常工作。由于我们试图移除 `bother`，RPM 中止了移除操作。

现在，十次中有九次，RPM 这样做是完全正确的。毕竟，如果其他包需要该包，为什么要试图移除它呢？和生活中所有事物一样，规则总有例外。这就是为什么有 `--nodeps` 选项。

在移除命令中添加 `--nodeps` 选项会指示 RPM 忽略任何与依赖项相关的问题并移除该包。回到我们之前的例子，让我们在命令行中添加 `--nodeps` 选项，看看会发生什么：

```
# rpm -e --nodeps bother
```

包被移除且没有任何提示。`blather` 包是否能正常工作则是另一回事。通常，使用 `--nodeps` 来绕过依赖项问题是个坏主意。包构建者包含依赖项要求是有原因的，最好不要去质疑他们的决定。

### 3.3.3. --noscripts: 不执行预卸载和后卸载脚本

在第 3.2.1 节中，我们使用 `-vv` 选项来查看 RPM 在移除包时实际执行的操作。我们注意到有两个脚本，即预卸载脚本和后卸载脚本，用于执行移除包过程中所需的命令。

`--noscripts` 选项可以防止在移除过程中执行这些脚本。这是一个非常危险的操作！`--noscripts` 选项实际上是供包构建者在开发其包时使用的。通过阻止预卸载和后卸载脚本运行，包构建者可以防止有缺陷的包拖垮其开发系统。在找到并消除缺陷之后，几乎没有理由阻止这些脚本运行；事实上，这样做可能会导致问题！

### 3.3.4. --rcfile <rcfile>: 从 <rcfile> 读取 RPM 默认设置

`--rcfile` 选项用于指定包含 RPM 默认设置的文件。通常不需要此选项。默认情况下，RPM 使用 `/etc/rpmrc` 以及位于您的登录目录中名为 `.rpmrc` 的文件。

如果需要在一组或多组 RPM 默认设置之间切换，则会使用此选项。软件开发人员和包构建者通常是使用 `--rcfile` 选项的人群。有关 `rpmrc` 文件的更多信息，请参阅附录 B，“`rpmrc` 文件”。

### 3.3.5. --root <path>: 使用 <path> 作为根目录

在移除命令中添加 `--root <path>` 会强制 RPM 假设 <path> 指定的目录实际上是根目录。`--root` 选项会影响移除过程的各个方面，因此预卸载和后卸载脚本将以 <path> 作为其根目录运行（如果您一定要知道的话，使用 chroot(2)）。此外，RPM 期望其数据库位于 <path> 指定的 `rpmrc` 文件条目中的目录，相对于 <path>。

通常此选项仅在初始系统安装，或者系统通过救援盘启动且需要重新安装某些包时使用。

### 3.3.6. --dbpath <path>: 使用 <path> 查找 RPM 数据库

为了使 RPM 能够工作，它需要访问 RPM 数据库。通常，该数据库位于 `rpmrc` 文件条目中指定的目录，即 `dbpath`。默认情况下，`dbpath` 设置为 `/var/lib/rpm`。

虽然可以在相应的 `rpmrc` 文件中修改 `dbpath` 条目，但当需要临时更改数据库路径时，使用 `--dbpath` 选项可能是更好的选择。使用 `--dbpath` 选项有用的一个例子是当需要检查从另一系统复制的 RPM 数据库时。虽然这不是常见情况，但很难用其他方式处理。

