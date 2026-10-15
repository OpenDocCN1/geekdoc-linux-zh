
```
##### dpkg --unpack man-db_2.7.0-2.5_amd64.deb
(Reading database ... 86425 files and directories currently installed.)
Preparing to unpack man-db_2.7.0-2.5_amd64.deb ...
Unpacking man-db (2.7.0-2.5) over (2.7.0.2-5) ...
Processing triggers for mime-support (3.58) ...
##### dpkg --configure man-db
Setting up man-db (2.7.0-2.5) ...
Updating database of manual pages ...
```

请注意，“处理触发器”行指的是每当包在受监控的目录中添加、删除或修改文件时自动执行的代码。例如，`mime-support`包监控`/usr/lib/mime/packages`，并在此目录中发生任何变化（例如在`man-db`的特定情况下为`/usr/lib/mime/packages/man-db`）时执行`update-mime`命令。

有时`dpkg`会因安装失败而返回错误。然而，你可以命令`dpkg`忽略此错误，仅发出警告，使用各种`--force-`选项。执行`dpkg --force-help`命令将显示这些选项的完整列表。例如，你可以使用`dpkg`强制安装`zsh`：

```
$ dpkg -i --force-overwrite zsh_5.2-5+b1_amd64.deb
```

常见的错误，你迟早会遇到，是文件冲突。当包含的文件已被另一个包安装时，`dpkg`将拒绝安装。此时会出现以下类型的消息：

```
Unpacking libgdm (from .../libgdm 3.8.3-2 amd64.deb) ...
dpkg: error processing /var/cache/apt/archives/libgdm_3.8.3-2_amd64.deb (--unpack):
  !! trying to overwrite '/usr/bin/gdmflexiserver', which is also in package gdm3
  !! 3.4.1-9
```

在这种情况下，如果你认为替换此文件对系统稳定性没有重大风险（通常就是这样），可以使用`--force-overwrite`来覆盖该文件。

虽然有许多可用的`--force-`选项，但只有`--force-overwrite`是经常使用的。这些选项用于特殊情况，为了尊重打包机制施加的规则，最好尽可能避免使用它们。请记住，这些规则确保了系统的一致性和稳定性。

#### 使用 APT 安装包

虽然 APT 比`dpkg`更先进，并且在幕后做了更多的工作，但你 interacting with packages 会发现非常简单。你可以用简单的`apt install` `package`将包添加到系统中。APT 会自动安装必要的依赖项：

```
##### apt install kali-linux-gpu
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  oclgausscrack occlhashcat
The following NEW packages will be installed:
  kali-linux-gpu oclgausscrack occlhashcat
0 upgraded, 3 newly installed, 0 to remove and 416 not upgraded.
Need to get 2,494 kB of archives.
After this operation, 51.5 MB of additional disk space will be used.
Do you want to continue? [Y/n]
Get:1 http://archive-2.kali.org/kali kali-rolling/non-free amd64 oclhashcat amd64 2.01+
  git20160114-0kali2 [2,451 kB]
Get:2 http://archive-2.kali.org/kali kali-rolling/main amd64 oclgausscrack amd64 1.3-1
  [37.2 kB]
Get:3 http://archive-2.kali.org/kali kali-rolling/main amd64 kali-linux-gpu amd64
  2016.3.2 [6,412 B]
Fetched 2,494 kB in 0s (3,060 kB/s)
Selecting previously unselected package oclhashcat.
(Reading database ... 317084 files and directories currently installed.)
Preparing to unpack .../0-oclhashcat 2.01+git20160114-0kali2_amd64.deb ...
Unpacking oclhashcat (2.01+git20160114-0kali2) ...
Selecting previously unselected package oclgausscrack.
Preparing to unpack .../1-oclgausscrack 1.3-1kali2_amd64.deb ...
Unpacking oclgausscrack (1.3-1kali2) ...
Selecting previously unselected package kali-linux-gpu.
Preparing to unpack .../2-kali-linux-gpu 2016.3.2_amd64.deb ...
Unpacking kali-linux-gpu (2016.3.2) ...
Setting up oclhashcat (2.01+git20160114-0kali2) ...
Setting up oclgausscrack (1.3-1kali2) ...
Setting up kali-linux-gpu (2016.3.2) ...
```

你也可以使用`apt-get install package`或`aptitude install package`。对于简单的安装包，它们本质上做的是相同的事情。正如你稍后所见，对于升级或当依赖项解析没有完美解决方案时，差异更有意义。

如果` sources.list`列出了多个发行版，你可以使用`apt install package=version`指定包版本，但通常更推荐使用`apt install package/distribution`来指示其来源发行版（`kali-rolling`、`kali-dev`或`kali-bleeding-edge`）。

与`dpkg`类似，你也可以指示`apt`强制安装包并覆盖文件，使用`--force-overwrite`，但语法有点奇怪，因为你是将参数传递给`dpkg`：

```
##### apt -o Dpkg::Options::="--force-overwrite" install zsh
```

### 8.2.3. 升级 Kali Linux

作为一个滚动发行版，Kali Linux 具有出色的升级能力。在本节中，我们将看看升级 Kali 有多简单，并讨论规划更新的策略。

我们建议定期升级，因为这会安装最新的安全更新。要升级，使用`apt update`，然后使用`apt upgrade`、`apt-get upgrade`或`aptitude safe-upgrade`。这些命令寻找可以升级而不删除任何包的已安装包。换句话说，目标是确保尽可能最小的侵入式升级。`apt-get`命令行工具比`aptitude`或`apt`稍微严格一些，因为它会拒绝安装之前未安装的包。

`apt`工具通常会选择最新的版本号（除了来自`kali-bleeding-edge`的包，无论其版本号如何，默认都会被忽略）。

要告诉`apt`在搜索升级包时使用特定发行版，需要使用`-t`或`--target-release`选项，后跟你想使用的发行版名称（例如：`apt -t kali-rolling upgrade`）。为了避免每次使用`apt`时都要指定此选项，你可以在文件`/etc/apt/apt.conf.d/local`中添加`APT::Default-Release "kali-rolling";`。
