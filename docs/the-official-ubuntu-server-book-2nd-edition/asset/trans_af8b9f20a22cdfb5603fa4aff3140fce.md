

```text
kernel ubuntu-installer/i386/linux
append vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
label cli
    menu label ^Command-line install
    kernel ubuntu-installer/i386/linux
    append tasks=standard pkgsel/language-pack-patterns= pkgsel/install-language-support=false vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
```

默认行告诉 pxelinux，标签为 install 的部分是用户在启动提示符下仅按下 Enter 时默认加载的部分。label install 部分定义了用户可以选择的特定配置。每个以 label 开头的部分都定义了另一个配置。当你浏览此配置文件时，你会看到为你预先设置了许多不同的标签。你可以通过在启动提示符下输入特定的标签然后按 Enter 在不同的部分之间进行选择。因此，虽然我可以直接按 Enter 选择上面标记为 install 且设为默认的部分，但我也可以在启动提示符下输入 install 然后按 Enter。我们需要对这个文件做的只是更改默认启动选项，使其也指向我们的 Kickstart 文件。为此我只需将我的选项添加到 append 行。文件的开头部分从这个：

```text
default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
```

改为这个：

```text
default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz ks=http://10.1.1.5/ks.cfg -- quiet
```

保存更改并退出文本编辑器。Pxelinux 现在已配置完成，你可以进入最后一步。

## Web

过程中的最后一步是设置一个 Web 服务器来托管你的 Kickstart 和 preseed 文件以及你可能拥有的任何自定义脚本。首先安装 apache2 包，它将提供你的 Web 服务器软件及其所有必要的依赖项：

```text
$ sudo apt-get install apache2
```

apache2 包会自动为你设置并启动一个功能正常的 Web 服务器，其默认文档根目录为 /var/www。我在这里不会介绍 Apache 的任何更高级配置，因为我们只需要一个 Web 服务器来托管几个文本文件。此时你需要做的就是将你的 ks.cfg 文件移动到此服务器上的 /var/www。你只需要对 ks.cfg 文件做一个更改以便 PXE 启动。由于我们不会从 CD-ROM 下载文件，我们需要告诉 Kickstart 文件从 Ubuntu 镜像获取文件，因此找到并更改读取以下内容的行

```text
cdrom
```

为

```text
url --url http://us.archive.ubuntu.com/ubuntu
```

> **NOTE** 由于此服务器将直接从 Ubuntu 镜像拉取所有软件包，安装肯定会比从 CD-ROM 安装花费更长时间。如果你计划进行大量自动化的 Ubuntu 安装，你可能需要考虑设置自己的 Ubuntu 归档镜像。

在继续之前，尝试通过 Web 浏览器或使用 wget 之类的工具访问你的 ks.cfg 文件，并确保 Apache 正在提供该文件。如果无法访问该文件，请检查 Apache 错误日志 /var/log/apache2/error.log 以获取可能出错的线索，并检查 ks.cfg 的权限以确保它是世界可读的。如果不是，输入 chmod a+r ks.cfg 使其可读。

## Test Your PXE Server

此时你应该准备好使用新安装来测试你的 PXE 服务器。如何将服务器设置为 PXE 启动并没有单一的说明。在某些服务器上，只需按功能键获取启动选项列表然后选择网络启动即可。在其他服务器上，你需要进入 BIOS 并更改启动顺序。还有一些服务器提供自动网络启动的功能键。你需要研究如何指示你的特定服务器进行网络启动，并确保它连接到与你的 PXE 启动服务器相同的子网。

一旦你通过 PXE 启动服务器，你将看到如图 4-3 所示的 Ubuntu 菜单。由于我们将默认标签设置为使用我们的 Kickstart 选项启动，我们在这里需要做的只是按 Enter。

> **NOTE** 即使是这种自动化的安装也需要一些用户交互，因为你至少需要在每个启动提示符下按 Enter 来开始安装过程。这在某种程度上是一种安全机制，因为如果六个月后你的其中一台服务器重新启动然后进行网络启动会怎样？如果一切完全自动化，该服务器将再次开始安装过程并可能覆盖其所有当前文件——这可能是一件非常糟糕的事情。对于某些组织来说，这种行为是可取的，特别是对于大量相同的机器集群。他们已采取适当的保护措施，确保除非他们希望机器从网络启动，否则不会启动，如果启动了，他们确实希望它执行重新安装。如果你想要一个 100% 自动化的安装，除了打开服务器外不需要任何用户交互，那么只需在 pxelinux.cfg/default 文件中定位 TIMEOUT 值。默认情况下它设置为 0，这意味着它永远不会超时。只需将其更改为 1，任何启动并获取该配置文件<|message|>的服务器将在一秒超时后自动加载默认标签。

![](img/304f637afcecc491b152ee8ac5afadee_173_0.png)

Figure 4-3 Ubuntu PXE boot menu

