
`root@kali:~/Downloads#`

“processing triggers”（处理触发器）行指的是软件包安装、扩展或调整某些注册表时自然执行的代码。例如，`mime support` 包 `/usr/lib/mime/` 执行该目录（如 `/usr/lib/mime/packages/man-db`）中任何更改的。

有时 `dpkg` 会忽略安装损坏的包。在任何情况下，你都可以安排 `dpkg` 忽略此并带有不同的 `--force-*` 选项。执行 `dpkg --force` 将显示这些选项的完整列表。例如，你可以使用 `dpkg` 强制安装 `zsh`：

```
$ dpkg -i --force-overwrite zsh_5.2-5+b1_amd64.deb
```

如果软件包包含另一个软件包已添加的文件，`dpkg` 将无法添加。在这种情况下，如果你认为此文件对系统的安全不构成严重危险（通常情况下如此），可以使用 `--force-overwrite` 覆盖文件。

虽然有很多 `--force-*` 选项，但只有 `--force-overwrite` 可能被频繁使用。这些选项是为了某些情况存在的，但在遵循软件包规则时最好忽略它们。请记住，这些规则确保了系统的一致性和稳定性。

### 5.3.2 使用 APT 安装软件包

尽管 `APT` 比 `dpkg` 先进得多并在后台完成更多工作，但你会发现处理软件包非常简单。你可以通过基础的安装命令将包添加到系统中：

```
# sudo apt install protonvpn 或 sudo apt install protonvpn -y
```

这里 `-y` 用于跳过警告（你要继续吗？）

```
kali@kali:~ sudo apt install protonvpn

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

The following packages were automatically installed and no longer required

The following additional packages will be installed:

protonvpn python3-proton-client proton3-protonvpn-nm-lib

Suggested packages:

girl.2-applicator-3-0.1

The following NEW packages will be installed:

protonvpn-gui

The following packages will be upgraded:

protonvpn-cli python3-proton-client python3-protonvpn-nm-lib

4 upgraded, 1 newly installed, 0 to remove and 567 not upgraded.

Need to get 3,094 KB of archives.

After this operation, 7,559 KB of additional disk space will be used.

Do you want to continue? [Y/n]
```

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_119_0.png)

你可以使用 `apt-get install package` 或 `aptitude package`。你甚至可以通过连续列出它们来一次安装多个包。

对于基础包安装，它们执行的操作基本上相似。正如你稍后看到的，这些差异在版本升级或依赖项没有理想安排时更为重要。如果发生这种情况，`list` 返回了几个不同的版本，你可以通过 `install package=version` 确定包版本，但使用 `apt install package/distribution` 显示其分发地（`Kali`、`Kali-dev` 或 `Kali-bleeding-edge`）通常更受青。

和 `dpkg` 一样，你也可以训练相应的命令使用 `--force-overwrite` 来强制安装包并覆盖文件，由于语法有点奇怪，因为你正在通过 `dpkg` 传递参数：

```
# apt -o Dpkg:Options::="--force-overwrite" install zsh
```

## 5.4 移除和清除包

移除一个包比安装一个包要简单得多。让我们来研究如何使用 `dpkg` 和 `APT` 移除一个包。要使用 `dpkg` 移除包，请提供 `-r` 或 `--remove` 选项，后跟包名。尽管如此，这种移除并不是彻底的：大多数文档、维护者内容、日志记录（框架日志）、由守护进程创建的信息（例如 `LDAP` 服务器索引的内容或 `SQL` 服务器数据库的内容）以及由包处理的其他客户端信息都将完好无损。清除操作使得卸载程序并在稍后以类似的配置重新安装它变得简单。同样，请记住配置状态不会被清除。考虑这个模型：

使用 `apt` 移除 `vlc`

```
sudo apt --purge remove vlc

kali:~# sudo apt --purge remove vlc 100 x1 @

Reading package lists... Done

Building dependency... Done

Reading state information... Done

The following packages were automatically installed and are no longer required

Use sudo apt autoremove to remove them.

The following packages will be REMOVED:

vlc* 0 upgraded, 0 newly installed, 1 to remove and 571 not upgraded.

After this operation, 231 kb disk space will be freed.

Do you want to continue? [Y/n] █
```

使用 `dpkg` 移除 `vlc`

```
sudo dpkg --remove vlc

kali:~# sudo dpkg --remove vlc 100 x1 @
```

你也可以使用合适的移除包命令从框架中驱逐包。`APT` 随后会删除依赖于被清除包的包。与 `dpkg` 的情况类似，配置文件和用户数据不会被清除。通过在包名后扩展后缀，你可以利用 `APT`（或 `apt-get` 和 `aptitude`）在类似的方向线上安装某些包并移除其他包。使用 `APT` 安装指令，在想要清除的包名前面加 `-`。使用合适的清除指令，在想要引入的包名前面加 `+`。

# Secbay 出版

下面的模型展示了安装 `package1` 和移除 `package2` 的两种不同方法。

### `apt install kali-package2-`

```
ckptkali:~$ sudo apt install vlc protonvpn

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

nvlc is already the newest version (3.0.12-3*)

The following packages were automatically installed and are no longer required

The following packages will be REMOVED:

protonvpn

0 upgraded, 0 newly installed, 1 to remove and 567 not upgraded.

After this operation, 9,216 B disk space will be freed.

Do you want to continue? [Y/n]
```

图 43 `apt install package` 命令

### `apt-purge remove package1+ package2`

```
ckptkali:~$ sudo apt --purge remove vlc+ protonvpn

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

vlc is already the newest version (3.0.12-3*)

The following packages were automatically installed and are no longer required

The following packages will be REMOVED:
```
