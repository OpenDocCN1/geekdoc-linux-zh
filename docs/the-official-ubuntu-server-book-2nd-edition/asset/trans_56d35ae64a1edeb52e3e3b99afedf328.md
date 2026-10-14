

这个功能实际上可以为管理员打开很多选项。例如，假设你管理着纽约、伦敦和东京的三个数据中心。作为一名优秀的管理员，你为每个数据中心设置了唯一的子域名，因此纽约、伦敦和东京的服务器分别使用 ny.example.net、london.example.net 和 tokyo.example.net 作为其域名。更有可能的是，你会希望为每个不同的数据中心设置自定义的 preseed 选项，因此你可以将这些自定义选项放在与通用 preseed.cfg 文件相同的服务器上的 ny.example.net.cfg、london.example.net.cfg 和 tokyo.example.net.cfg 中。然后在你的 preseed.cfg 文件中可以添加

```
d-i preseed/include_command \
string echo `hostname -d`.cfg
```

hostname -d 命令会输出主机的域名，因此如果纽约的一台主机的完全限定域名是 web1.ny.example.net，那么 hostname -d 将输出 ny.example.net。我们的 preseed 命令随后会 echo ny.example.net.cfg。

## 在安装期间运行自定义命令

如果你发现自己在 include_command 选项中编写越来越长的单行命令，那么你肯定会想了解一下其他一些 preseed 选项，这些选项允许你运行整个脚本。有三个不同的 preseed 选项允许你在安装程序环境中执行命令。

我首先要提到的第一个选项在某种程度上是 include 选项的扩展。那些选项允许你列出要下载并读取的额外 preseed 文件，而 preseed/run 选项则会下载并执行你选择的脚本：

```
d-i preseed/run string command.sh
```

这个 command.sh 脚本可以执行你在 include_command 中之前可能使用的所有 shell 逻辑，只是现在组织起来容易得多。你甚至可以在脚本中读取和设置 preseed 值。只需使用 debconf-get 和 debconf-set 命令来获取和设置安装的不同 preseed 设置即可。例如，如果我想检索预设的主机名，我可以运行

```
debconf-get netcfg/get_hostname
```

如果我想在脚本中将该选项设置为 web1，我会运行

```
debconf-set netcfg/get_hostname web1
```

下一个允许你在安装中运行命令的 preseed 选项是 preseed/early_command。该选项允许你指定一个命令，该命令将在安装中尽可能早地运行——基本上是在读取 preseed 文件后立即运行。这与 preseed/run 命令类似，只是你不必检索要执行的脚本——你可以直接从安装环境运行 shell 命令。如果你愿意，可以使用 preseed_fetch 命令使 preseed/early_command 的行为与 preseed/run 完全相同，该命令会为你从 preseed 服务器检索文件。它的第一个参数是要检索的文件，第二个参数告诉命令将下载的文件放置在何处。在此示例中，我重新创建了上面 preseed/run 示例的功能。

```
d-i preseed/early_command string preseed_fetch command.sh \
/tmp/command.sh; sh /tmp/command.sh
```

而 preseed/early_command 在安装过程中尽可能早地执行，preseed/late_command 则尽可能晚地执行。early_command 有助于在安装程序开始大部分安装过程之前为安装程序设置动态值，但 late_command 适用于在你知道基础映像已安装后运行自己的自定义程序。在安装程序的此阶段，服务器的根分区仍安装在 /target 目录下，因此你可以潜在地 chroot 到该目录并运行命令，就好像你直接从已安装的服务器上运行它们一样。

与 early_command 一样，你可以使用 preseed_fetch 来检索要运行的脚本。其中一些最常见的事情已经通过 in-target 和 apt-install 命令为你自动化了。in-target 命令为你自动化了 chroot 过程，因此你在 in-target 之后列出的任何命令都将在已安装的环境中执行。apt-install 命令将使用 APT 来安装任何额外的

