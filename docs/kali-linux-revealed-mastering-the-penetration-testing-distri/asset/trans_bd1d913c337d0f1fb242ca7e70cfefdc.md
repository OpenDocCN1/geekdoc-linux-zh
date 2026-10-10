

## 降级到可用的版本

如果问题是明显的回归（即旧版本可以正常工作），你可以尝试降级该包。在这种情况下，你需要旧版本的副本。如果你可以在 APT 配置中的某个仓库访问到旧版本，你可以使用一个简单的单行命令来降级（参见第 8.2.2.2 节，“使用 APT 安装包”[第 177 页]）。但在 Kali 的滚动发行版中，通常在任何时候每个包只有一个版本。

你仍然可以尝试找到旧的 .deb 文件并使用 dpkg 手动安装它。旧的 .deb 文件可以在多个地方找到：

- 在 APT 的缓存目录 /var/cache/apt/archives/ 中
- 在你常用的 Kali 镜像站点的 pool 目录中（已删除和过时的包会保留三到四天，以避免用户没有最新包索引的问题）
- 如果受影响的包是由 Debian 而不是 Kali 提供的，可以在 http://snapshot.debian.org 找到；该服务保留了所有 Debian 包的历史版本

## 处理损坏的维护脚本

有时，升级会因为某个包维护脚本失败（通常是 postinst）而中断。在这些情况下，你可以尝试诊断问题，并可能通过编辑有问题的脚本来绕过它。

这里我们依赖于维护脚本存储在 /var/lib/dpkg/info/ 中且我们可以审查和修改这一事实。

由于维护脚本通常只是简单的 shell 脚本，可以在 shebang 行之后添加 `set -x` 行，并安排它们重新运行（对于 postinst 使用 `dpkg --configure -a`），以精确查看正在发生什么以及在哪里失败。此输出也可以很好地补充你可能提交的任何 bug 报告。

利用新获得的知识，你可以修复根本问题，或者将失败的命令转换为可工作的命令（例如，在行尾添加 `|| true`）。

请注意，此技巧不适用于失败的 preinst，因为该脚本在包安装之前就会执行，因此它尚未处于其最终位置。它对 postrm 和 prerm 有效，但你需要执行包移除（相应地，升级）来触发它们。

## dpkg 日志文件

dpkg 工具在 /var/log/dpkg.log 中记录其所有操作的日志。由于它详细记录了每个包的各个阶段，因此该日志非常详尽。除了提供一种跟踪 dpkg 行为的方法外，它还有助于保持系统发展的历史记录：你可以找到每个包安装或更新的准确时刻，这些信息在理解最近的行为变化时极其有用。此外，由于记录了所有版本，很容易将信息与相关包的变更日志、Debian.gz 或在线 bug 报告进行交叉核对。

```
# tail /var/log/dpkg.log

2016-12-22 09:04:05 status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 startup packages remove
2016-12-22 09:20:07 status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 remove kali-linux-gpu:amd64 2016.3.2 <none>
2016-12-22 09:20:07 status half-configured kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status half-installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status not-installed kali-linux-gpu:amd64 <none>
```

## 使用 apt --reinstall 和 aptitude reinstall 重新安装包

当你错误地通过删除或修改某些文件损坏系统时，恢复它们最简单的方法是重新安装受影响的包。不幸的是，打包系统发现该包已安装，并礼貌地拒绝重新安装它。为了避免这种情况，请使用 apt 和 apt-get 命令的 --reinstall 选项。以下命令即使 postfix 已经存在也会重新安装它：

```
# apt --reinstall install postfix
```

aptitude 命令行略有不同，但通过 aptitude reinstall postfix 可以达到相同的结果。dpkg 命令不会阻止重新安装，但它很少被直接调用。

**不要使用 apt --reinstall 来恢复遭受攻击的系统**

使用 apt --reinstall 来恢复在攻击期间被修改的包肯定不能将系统恢复到攻击前的状态。在攻击之后，你不能依赖任何东西：dpkg 和 apt 可能被恶意程序替换，并不会按你希望的方式重新安装文件。攻击者也可能修改或创建了 dpkg 控制范围之外的文件。

请记住，你也可以使用 apt 指定特定发行版，这意味着你可以回滚到包的一个较旧版本（如果例如你知道它能很好地工作），前提是该版本仍在 sources.list 文件引用的某个源中可用：

```
# apt install w3af/kali-rolling
```

## 利用 --force-* 修复损坏的依赖关系

如果你不小心，使用 --force-* 选项或其他故障可能导致系统状态使 APT 命令族拒绝运行。实际上，其中一些选项允许在依赖项未满足或存在冲突时安装包。结果是，从依赖项角度来看，系统变得不一致，并且 APT 命令会拒绝执行任何操作，除了那些使系统恢复一致状态的操作（这通常包括安装缺失的依赖项或移除有问题的包）。这通常会导致如下所示的消息，这是在安装新版本的 *rdesktop* 的同时忽略其对更新版本 *libc6* 的依赖项后获得的：

```
# apt full-upgrade
[...]
You might want to run 'apt-get -f install' to correct these.
The following packages have unmet dependencies:
 rdesktop: Depends: libc6 (>= 2.5) but 2.3.6.ds1-13ietch7 is installed
E: Unmet dependencies. Try using -f.
```

如果你是一个有胆识的管理员，并且确信你的分析是正确的，你可以选择忽略依赖项或冲突，并使用相应的 *-force-* 选项。在这种情况下，如果你希望继续能够使用 *apt* 或 *apt-get*，你必须编辑 */var/lib/dpkg/status* 以删除或修改你选择覆盖的依赖项或冲突。

这种操作是一种丑陋的变通方法，除非在最极端的必要情况下，否则永远不要使用。很多时候，更合适的解决方案是重新编译导致问题的包，或者使用提供 backports 的仓库中的新版本（可能是已修复的）（backports 是特别重新编译以在较旧环境中工作的新版本）。

## 8.2.7. 前端：aptitude 和 synaptic

APT 是一个 C++ 程序，其代码主要位于 *libapt-pkg* 共享库中。得益于这个共享库，它为创建用户界面（前端）打开了大门，因为共享库代码可以很容易地重复使用。从历史上看，*apt-get* 最初仅被设计为 *libapt-pkg* 的测试前端，但其成功趋势掩盖了这一事实。

随着时间推移，尽管像 *apt* 和 *apt-get* 这样的命令行界面很受欢迎，但开发出了各种图形界面。我们将在本节中查看这两个界面：*aptitude* 和 *synaptic*。

## Aptitude

Aptitude，如图 8.1“*aptitude 包管理器*”[第 191 页] 所示，是一个交互式程序，可以在控制台上以半图形模式使用。你可以浏览已安装和可用的包列表，查找所有信息，并选择要安装或移除的包。该程序专门设计供管理员使用，因此其默认行为比 APT 更智能，其界面也更容易理解。

