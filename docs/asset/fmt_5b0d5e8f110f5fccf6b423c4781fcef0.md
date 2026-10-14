
```
100 1000 1000000000 ext3 \
  $defaultignore{ } \
  $primary{ } \
  method{ lvm } \
  device{ /dev/sda } \
  vg_name{ vg00 } .
```

当你设置自己的卷组时，你可能还想控制特定分区属于哪个卷组。使用`in_vg{ }`选项来指定特定分区所属的卷组，并使用`lv_name{ }`来命名逻辑卷。例如，如果我想让上面创建的交换分区明确成为`vg00`的一部分并标记为`testswap`，我可以将其更改为如下：

```
64 512 300% linux-swap \
    method{ swap } format{ } \
    lvmok{ } \
    in_vg{ vg00 } \
    lv_name{ testswap } \
.
```

> 注意 由于这些分区声明中的每一行都是上一行的延续，你可以将每个选项单独放在一行或将多个选项放在同一行——由你决定。只要确保在每一行的末尾使用 `\` 符号，并在每个分区的末尾使用 `.` 即可。

## Packages and Mirrors

一种服务器类型与另一种服务器类型的区别在于它运行哪些服务，而在 Ubuntu 上，这最终取决于你决定在系统上安装哪些软件包。虽然你当然可以使用安装程序仅设置一个基础安装镜像，然后稍后再自行添加软件包，但如果你追求完全自动化，你应该研究 preseed 流程中内置的软件包设置。

preseed 文件中的基本软件包选项相当直接且不言自明。让我们从我在默认 preseed 文件中使用的选项开始：

```
d-i mirror/country string US
d-i mirror/http/proxy string
d-i pkgsel/install-language-support boolean false
d-i pkgsel/update-policy select none
tasksel tasksel/first multiselect standard, ubuntu-server
```

第一个选项定义了用于检索软件包和更新的 Ubuntu 镜像（美国的默认镜像）。我不使用代理，但我也不想被提示输入代理，因此我将此选项留空。我不想安装额外的语言包，所以我将`pkgsel/install-language-support`设置为`false`。`pkgsel/update-policy`选项让你可以定义系统是否会自动应用更新。我们将其设置为`none`，因此任何更新都必须手动应用。最后，你可以看到你也可以为`tasksel`预设值；在我的例子中，我告诉它选择`standard`软件包以及`ubuntu-server`任务。我也可以根据需要添加通过手动`tasksel`流程可用的其他任务，例如`lamp-server`。有时你想要安装的额外软件包并不属于特定任务。在这种情况下，你可以使用`pkgsel/include`选项来添加安装程序将为你添加的一系列特定软件包。此示例添加了 openssh-server 和 build-essential 软件包：

```
d-i pkgsel/include string openssh-server build-essential
```

### Custom Package Repositories

除了需要定义的标准设置之外，你还可以在 preseed 文件中对 APT 配置进行许多调整。例如，你可以选择要在 APT 中包含哪些存储库。下面的值包含了 restricted、universe 和 backports 存储库：

```
d-i apt-setup/restricted boolean true
d-i apt-setup/universe boolean true
d-i apt-setup/backports boolean true
```

你可能还决定指定从哪个 Ubuntu 镜像检索软件包，因为你拥有自己的存储库，或者你知道某个对你来说更快的存储库。在任何一种情况下，你只需要将`mirror/country`选项设置为`manual`，然后指定要使用的镜像即可。我将`mirror/http/proxy`值留空，但如果你使用 HTTP 代理，你会将它的值放在那里。

```
d-i mirror/country string manual
d-i mirror/http/hostname string us.archive.ubuntu.com
d-i mirror/http/directory string /ubuntu
d-i mirror/http/proxy string
```

```
d-i apt-setup/local0/repository string \
  http://apt.example.net/ubuntu $release-name; main
d-i apt-setup/local0/comment string local server
d-i apt-setup/local0/source boolean true
d-i apt-setup/local0/key string http://apt.example.net/key
```

这个示例添加了存储在`apt.example.net`上的本地仓库并将其标记为`local1`服务器。`apt-setup/local10/`源行也会添加源代码仓库，而`apt-setup/local10/key`指向你的 APT 仓库必须设置的用于签名软件包的 GPG 密钥。如果你没有设置并提供此密钥，安装时会报错。

## 用户设置

在几乎所有 Linux 安装程序中，你都会找到一个用于配置用户账户的部分。与安装程序的每个其他部分一样，此部分也可以预设。以下是我在默认`preseed.cfg`文件中使用的内容：

```
d-i passwd/user-fullname string Ubuntu User
d-i passwd/username string ubuntu
d-i passwd/user-password password insecure
d-i passwd/user-password-again password insecure
user-setup/udeb user-setup/encrypt-home boolean false
```

每个字段都很容易理解，但请注意我必须指定两次密码。最后一个选项让你定义主目录是否加密。由于这是一台服务器，我们希望安装过程自动化，最简单的方法就是将该选项设置为`false`。现在如果你不想以明文形式列出密码，请在`user-password`行中替换为以下内容：

```
d-i passwd/user-password-crypted password [MD5 hash]
```

如果你确定如何为特定密码计算 MD5 哈希，可以在另一台系统上将用户的密码更改为你想要使用的密码，然后查看`/etc/shadow`文件中为其设置的 MD5 哈希。

Ubuntu 会使用默认 UID 和组 membership 为默认用户设置账户。你也可以使用预设值来覆盖它：

```
d-i passwd/user-uid string 1010
d-i passwd/user-default-groups string audio cdrom video
```

Ubuntu 为提高安全性而做的一件事是默认禁用`root`账户。取而代之的是，用户使用`sudo`程序获得超级用户权限。当然，你也可以使用预设值来覆盖此设置。以下一组选项将同时设置`root`用户和默认用户：

想要在多个设备上安装 GRUB，只需在`grub-installer/bootdev`行上一个接一个地列出它们，用空格分隔。

如果你希望为服务器提供额外安全保护，以防止用户修改 GRUB 以进入单用户模式等，此选项可以对 GRUB 进行密码保护。此选项也可以通过 preseed 自动化：

```
d-i grub-installer/password password insecure
```

```
d-i grub-installer/password-again password insecure
```

与用户密码设置一样，你可以使用上面所示的明文密码，或使用下面所示的 MD5 哈希。

```
d-i grub-installer/password-crypted password [MD5 hash]
```

## 杂项

最后，还有一些额外的选项并非关键，但在某些环境下可能很有用。例如，默认情况下 Ubuntu 会在安装完成后弹出光盘。好吧，如果你远程安装 Ubuntu 而且相隔数千英里，这意味着你只有一次机会在有人重新插入光盘之前完成安装。相反，你可以设置一个 preseed 选项来禁用此操作：

```
d-i cdrom-detect/eject boolean false
```

或者，你可能不想立即重启进入新系统，而是让其停止。这在例如你想提前构建一群机器但不会立即使用它们时可能很有用。

```
d-i debian-installer/exit/halt boolean true
```
