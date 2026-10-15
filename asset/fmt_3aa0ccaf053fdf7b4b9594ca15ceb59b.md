
当 `sendmail` 启动时，它会查找你的主机名（在本例中，为 `yourbox`）。然后它发现 `yourbox` 的 IP 是 `127.0.0.1`，`sendmail` 不喜欢这样，于是再次进行查找。它会持续进行 `while` 循环，直到最终放弃并退出。解决这个问题非常简单，编辑你的 `/etc/hosts` 文件并将其更改如下内容：

```
127.0.0.1 localhost
10.56.142.1 yourbox
```

## 2.19 我如何配置 RedHat 使用带颜色的 `ls`？Paul Anderson, paul@geeky1.ebtech.net

`RedHat` 的发行版带有一个 `color-ls`，然而，我不明白他们为什么不默认配置为彩色使用。以下是修复方法。

首先，输入 `eval ls='--color=yes'`

接下来，设置 `alias ls='--color=yes'`

并将 `alias...` 放入你的 `/etc/bashrc` 中

## 2.20 我如何找到 `/usr/lib` 中哪个库持有某个特定函数？Pavel Veselow, vps@unicorn.niimm.spb.su

如果你在编译时漏掉了一个需要链接的库怎么办？所有的 `gcc` 都会报告函数名……这里有一个你需要的简单命令：

```
for i in; do echo $i;nm|grep tgetname 2>/dev/null; done
```

其中 `tgetname` 是你正在查找的函数名。

## 3.1 在 Linux 和 Windows 之间共享交换分区。Tony Acero, ace3@midway.uchicago.edu

对于除 `/` 以外的所有挂载文件系统，在调用 `unmount -a` 之前执行。这意味着如果由于某种原因，关机未能杀死所有进程并挂载了磁盘，它们在重启时仍然是洁净的。这为我节省了大量的重启时间。

## 3. 详细技巧

现在，请约束自己，始终！始终！始终！将新的软件包存放在 `/usr/local/src/from (...$WHEREVER.I.GOT.IT/`（`.tar` 或其他文件）下，并在 `/usr/local/src (...$HOSTNAME)/src` 下构建它们。确保它使用了本地层级结构。如果绝对必须安装在 `bin` 或 `usr/bin` 或其他地方——请从本地层级结构为你在任何地方需要的每个元素创建一个符号链接。

之所以这样做——即使工作量更大——是因为它有助于隔离出哪些内容需要备份、恢复或重新安装，以防发生通过发行版方法（现在通常是 CD）的全重新安装。通过使用 `/usr/local/from` 目录记录一份关于源码来自何处的非正式日志——这在你在寻找新更新时，在监控安全公告列表时可能至关重要。

我的其中一个系统（我称之为家的那个）是在我采用这些策略之前组装的。我仍然不知道它与“安装后”系统相比还有哪些不同之处。尽管我对家庭系统的配置几乎没动过手，而且我是唯一使用它的人。

相比之下，我在工作中设置的系统（当我被推向系统管理员一角时）都是按照这种方式配置的——由许多承包商和其他 MIS 人员管理过，并进行了大量的升级和软件包安装。尽管如此，我非常清楚哪些精确的元素是在初始安装和配置之后被放入的。

### 3.5 将目录中的所有文件转换为小写。Justin Dossey, dossey@ou.edu。

我注意到在 Issue 12 的 2c 技巧部分中推荐了一些困难或不必要的步骤。由于有多多个，所以我把它们发给你们：

```bash
#!/bin/sh
# lowerit
# 将当前目录下的所有文件名转换为小写
# 仅对普通文件操作——不更改目录名称
# 在覆盖现有文件之前会请求确认
for x in $(ls)
  do
    if [ -f $x ]; then
      continue
    fi
    lc=$(echo $x | tr '[A-Z]' '[a-z]')
    if [ $lc != $x ]; then
      mv -i $x $lc
    fi
  done
```

哇。这是一个很长的脚本。我不会写脚本来做这个；相反，我会使用这个命令：

```bash
for i in *; do [ -f $i ] && mv -i $i "$(echo $i | tr '[A-Z]' '[a-z]')"; done
```

在命令行上执行。

贡献者说他写那个脚本是为了易读性（见下文）。

在下一个技巧中，即关于添加和删除用户的那个，Geoff 在最后一步之前一直很好。重启？

老兄，我希望他不要每次删除用户都重启。你们只需要做前两步。而且，那个用户到底有什么进程？在 `bot` 运行中吗？用一个简单的命令杀死进程：

```bash
kill -9 'ps -aux |grep <username> |tr -s " " |cut -d " " -f2'
```

例如，用户名是 `foo`

```bash
kill -9 'ps -aux |grep foo |tr -s " " |cut -d " " -f2'
```

卸载后，用它来处理忘记的 `root` 密码。

`Gazette` 提供的解决方案是最通用的，但不是最简单的。通过 `LILO` 和 `loadlin`，可以提供启动参数 `"single"` 直接进入默认 shell 且没有登录密码提示。从那里开始，你可以在输入 `"init 3"` 启动用户模式之前更改或删除任何密码。重启次数：1。另一种方法重启次数：2。

`Justin Dossey`

### 3.6 给新系统管理员的的一些建议。Jim Dennis, jadestar@gmail.net

创建并维护 `/README.hostname` 和/或 `/etc/README.hostname` [可能还有 `/usr/local/etc/README.hostname`] —— 维护。

绝对要，从管理系统的 第一天 起，就在在线日志文件中记录笔记。你可能可以将 `vi /README.($hostname)` 设为 `root/.bash_logout` 中的一行。另一种方法是编写它或使用执行某些操作的脚本：

```bash
function edit \
  { unset exit; exit; \
    cat >> /tmp/session.\$(date +%y%m%d); \
    >> /README.($hostname) && \
    vi /README.($hostname);
  }
script -a "/tmp/session.\$(date +%y%m%d)" /bin/sh
```

（使用 `script` 命令创建会话日志并创建一个函数来自动更新日志）。

我承认我还没有实现这种自动化策略——到目前为止一直依靠自律。然而，我一直在尝试这个想法（甚至已经到了原型脚本和 shell 函数的阶段，如你所见）。阻碍这一点的是 `script` 命令本身。我认为在决定使用它之前，我必须获取源码并添加几行参数（以暂停从命令行开始记录）。我的最后一个建议（针对这一轮）：`Root` 的路径由 `PATH=/bin` 组成。仅此而已。没有别的。`root` 提供的通过 `/bin` 的符号链接、别名或 `/bin` 中的脚本提供的内容，都是在没有显式路径的情况下使用的。这让任何以 `root` 身份运行的人（有时是痛苦的）意识到多用户将将定期查看 `/bin`。

## 2. 不耐等待者的快速上手

此修订版本是对初始版本重大重写后的更新，包含了关于 `xterms` 和内核补丁的信息。

本文中的信息已在 `Redhat` 4.1 上确认，最初是基于 `Slack` 2.0.2 版本和 1.1.54 内核编译的。内核补丁信息获取自 `slackware` 2.2.0（使用 1.2.13 内核，并以 `tsh` 为默认 shell），随后在 2.0.27 内核上进行了确认。如果你使用任何其他配置或 Unix 版本，若能提供说明你的操作系统以及是否支持标准颜色的备注，我将不胜感激。

## 2 针对不耐等待者的快速上手

如果你有一个新的 Linux 发行版，请对家目录下的这些文件进行以下修改。修改将在下次登录后生效。

```
/.bashrc:
  alias ls='ls --color'

/.cshrc:
  alias ls='ls --color'
```

搞定！

你可能还想运行 `eval $(dircolors $HOME/.colourrc` 来获取你自己的颜色。此文件是通过 `dircolors -p $HOME/.colourrc` 创建的，并带有详细的注释以便进一步编辑。

## 3 我真的有这个功能吗？

首先，你需要知道你是否有一个可以正确显示颜色的 `ls` 版本。在 Linux 文本终端中尝试此命令（尽管 `xterm` 也可以）：

```
% ls --color
```

（如果你收到错误消息，指示 `ls` 不理解该选项，你需要安装新版本的 GNU 工具包。如果你的发行版没有升级包，请直接从你的 GNU 镜像站获取最新版本并从源码安装。）
