
- 其他相关信息（例如“我正在使用软盘安装方法来自 CD。”）

## 如何发送

Red Hat 的支持系统是基于电子邮件的且部分自动化的；因此，确保您以正确的格式发送支持问题非常重要，这样您的消息才能被识别并路由给适当的支持技术人员。为了获得您的 Red Hat Software 产品的技术支持，您必须先注册。

提交故障单（trouble tickets）可以通过传统的电子邮件方式发送，也可以通过万维网发起。在提供注册信息后，您将看到一个新的菜单，允许您编辑注册信息或开启故障单。尽快登录并在 Web 上开工单！http://www.redhat.com/support/register/

要通过电子邮件开启支持单，您只需发送支持系统消息，主题为：`[registration #nnnn nnnn nnnn]`，其中 `nnnn nnnn nnnn` 是您请求支持的产品注册号。例如，如果您的注册号是 `fffe fff0`，则主题行应为：

```
Subject: [registration #fffe fff0 fff 00]
```

方括号、数字符号和“registration”一词必须存在。如果您愿意，可以在主题行添加解释性文本：

```
Subject: [registration #fffe fff0 fff 00] CD-ROM problem
```

一旦您开启了故障单，支持回复将带有支持单号在主题行中发送给您：

`Subject: [ticket #12015] CD-ROM problem`

要就同一个问题进行通信，只需发送相同主题的回复即可：

`Subject: Re: [ticket #12015] CD-ROM problem`

如果您觉得问题已经解决，您也可以关闭故障单。只需在相同主题上添加关闭标签：

`Subject: Re: [close ticket #12015] CD-ROM problem`

一旦您的问题解决或问题得到解答，处理您支持单的技术人员就可以关闭故障单。这也可以通过网站完成。哪种方法都会收到来自支持系统的消息，说明故障单已关闭并包含问题的摘要。

## A.3 支持 FAQ（常见问题）

Red Hat 支持的地址为 `support@redhat.com`；所有支持问题都应发送到那里。还有其他相关地址：

- 如需 Red Hat FAQ（常见问题及解答）副本，请发送邮件至 `faq@redhat.com`。
- 如需 Red Hat Tips（关于设置 PPP 连接的提示）副本，请发送邮件至 `ppp-tips@redhat.com`。
- 报告 Bug，请发送邮件至 `bugs@redhat.com`。

### 支持常见问题

以下是支持人员经常看到的问题：

问题：我向支持系统发送了多次消息，但完全没有收到回复。那里有人吗？

解答：检查您的注册信息，确保您的电子邮件地址正确。您可以通过登录 http://www.redhat.com/ 进行检查。

问题：我知道我已经注册了，但一直收到支持系统发来的我未注册的消息。系统坏了吗？

解答：请确保您通过万维网 http://www.redhat.com/support/register/ 进行注册。如果没有这样做，请先访问注册页面。接下来，输入登录名并点击“创建登录”。之后系统将提示您输入一些个人信息。完成后点击“提交”按钮，然后是注册号，类似于 `fffe ff00`。务必输入有关系统的所有信息。

问题：但我通过电子邮件注册了。为什么支持系统不起作用？

解答：当您通过电子邮件注册时，消息会发送给人工进行手动注册；这可能会导致您的注册延迟几小时到几天不等。

问题：我完美地完成了注册所有操作，但仍然收到我的注册号无效的消息。

解答：请确保您使用的是有效的产品注册号。如果您没有从 Red Hat Software 或销售官方版本的供应商购买官方盒（盒上会有“official”字样），您将无法注册，因为 Red Hat Software 不支持其他软件发行商包装的产品。

问题：我在注册页面上看到一个要求我的登录名的东西？我的登录名是什么？

解答：如果您是支持系统的首次用户，或者在 1997 年 8 月 15 日之后访问支持系统，那么登录名可以是您想要的任何。它必须是一个完整的单词，如果已经重复，您将收到错误警告。如果您在此之前访问过系统并拥有有效注册，您的登录名将是您的电子邮件地址。

### 支持常见问题解答 (FAQ)

注册时密码将是旧的 Support ID 数字。如果您愿意，可以更改密码；但登录名无法更改。

**问题** – 我尝试输入登录名和密码但系统不接受。为什么它不接受我尝试输入的密码？

**答案** – 密码长度至少为 5 个字母数字字符，最多不超过 8 个。请确保在注册页面的两个密码字段中输入的密码完全一致。

**问题** – 我听说可以更改我的注册信息并查看所有的旧工单以及过去的往来邮件。我该如何操作？

**答案** – 只需登录 http://www.redhat.com/support/register 注册页面即可可以使用所有这些选项。如果您需要引用旧的故障工单、更改系统信息或仅检查故障工单状态，请访问此页面。您还可以直接从这些页面通过网页使用有效的注册数字创建故障工单。

# 制作安装磁盘

虽然 Red Hat Linux/Intel 盒装版包含了启动磁盘和补充磁盘，但 Red Hat Linux 的 Alpha 和 SPARC 版本并非如此。此外，尝试安装 Red Hat Linux/Intel 的人员可能需要使用从 Red Hat Linux Errata 获取的更新磁盘镜像。因此，有时需要从镜像文件创建磁盘。

顾顾名，镜像文件是一个包含磁盘内容精确副本（或镜像）的文件。由于磁盘除了文件中包含的数据外，还包含文件系统信息，因此在镜像文件写入磁盘之前，它是无法使用的。

开始之前，您需要一个空白、已格式化的高密度（1.44 MB）3.5 英寸磁盘。您需要访问一台带有 3.5 英寸磁盘驱动器且能够运行 DOS 程序或大多数类 Linux 操作系统中自带 `dd` 工具程序的计算机。

镜像文件位于您的 Red Hat Linux CD 的以下目录中：

- `images` – 包含 Red Hat Linux/Intel 的启动和补充镜像，以及 Red Hat Linux/Alpha 的各种内核和内存盘镜像。在 Red Hat Linux/SPARC CD 上，此目录包含一个启动镜像和一个用于网络启动的镜像。
- `milo` -- 包含 Red Hat Linux/ Alpha 微型加载程序 MILO 的各种镜像。此目录仅存在于 Red Hat Linux/ Alpha CD 上。

一旦您选择了正确的镜像，就可以将镜像文件传输到磁盘中了。如前所述，这可以在支持 DOS 的系统上完成，也可以在运行类 Linux 操作系统的系统中完成。

## B.1 在 MS-DOS 下制作磁盘

在 MS-DOS 下制作磁盘，请使用 Red Hat Linux CD 中 `dosutils` 目录下的 `rawwrite` 工具。首先，对一个空白、已格式化的 3.5 英寸磁盘进行适当的标记（例如“Boot Diskette”、“Supplemental Diskette”等）。将其插入磁盘驱动器。然后，使用以下命令（假设您的 CD 是 d 盘）：

```
C:\> d:
D:\> cd dosutils
D:\dosutils> rawwrite
Enter image source file name: ..images\boot.img
Enter target diskette drive: a:
nPlease insert a formatted diskette into drive A: and
press --ENTER-- : EnternD:\dosutils>
```

`rawwrite` 会要求您输入磁盘镜像的文件名以及想要写入的镜像名称（例如 `..images/boot.img`）。然后 `rawwrite` 会询问要将镜像写入哪个磁盘驱动器，请输入 `a:`。最后，`rawwrite` 会确认所选驱动器中是否已插入已格式化的磁盘。按下 Enter 键确认后，`rawwrite` 将镜像文件复制到磁盘上。如果您需要制作另一个磁盘，请标记另一个磁盘并再次运行 `rawwrite`，指定相应的镜像文件。

## B.2 在类 Linux 系统下制作磁盘

在 Linux（或任何其他类 操作系统）下制作磁盘，您必须拥有写入代表 3.5 英寸磁盘驱动设备的权限（在 Linux 下称为 `/dev/fd0`）。首先，对一个空白、已格式化的磁盘进行适当的标记（例如“Boot Diskette”、“Supplemental Diskette”等）。将其插入磁盘驱动器（但不要执行 `mount` 命令）。挂载 Red Hat Linux CD 后，切换到包含目标镜像文件的目录，并使用以下命令（根据情况更改文件名和磁盘设备名称）：

```
# dd if=boot.img of=/dev/fd0 bs=1440k
```

如果您需要制作另一个磁盘，请标记另一个磁盘并再次运行 `dd`，指定相应的镜像文件。

# C 关于 Red Hat Linux/SPARC 的特定信息
