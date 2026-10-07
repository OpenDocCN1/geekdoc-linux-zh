
Linux Printing-HOWTO 建议使用 `/usr/bin/smbprint` 命令打印到你的 SMB 打印机。此命令无法与 `printtool` 创建的文件协同工作。Red Linux 的 `smbprint` 命令是 `/usr/bin` 中命令的修改版本。这两个脚本最终依赖 `smclient` 命令来打印文件（或者说，将其重定向到远程 SMB 打印机队列）。

如果你足够勇敢，可以直接使用 `smclient` 命令。它使用一个与 `ftp` 命令类似的界面。你可以添加所有选项进入交互模式，在模式下你可以向上和向下移动目录，获取和放置文件，并运行其他命令（如 `print`）。以下是依赖我们刚刚输入的打印定义使用 `smclient` 的示例：

```
smclient \\\canyons\\canyonsps* asecretpwd -N -c "print file.ps"
```

由于命令是从 shell 运行的，主机名 (`canyons`) 和服务名 (`canyonsps`) 中的所有反斜杠必须双倍。之后，`-N` 选项会抑制密码提示（因为密码已经在命令行给出，所以它可能是多余的，但并无害）。`-c` 选项用于输入你通常在 `smclient` 提示符下交互输入的命令。在这种情况下，它运行命令 `"print file.ps"` 来打印文件。

# 表 17-1（续）

| 厂商 | 完美运行的型号 | 基本运行的型号 | 部分运行的型号 | 完全无法运行型号 |
| --- | --- | --- | --- | --- |
| HP | 2000Cse, 2500C, Designjet 2650C, Deskjet 1200C, Deskjet 1600C, Deskjet 1600Cm, Deskjet 400, Deskjet 420C, Deskjet 500, Deskjet 550C, Deskjet 600, Deskjet 660Cse, Deskjet 690C, Deskjet 850C, Deskjet 855C, Deskjet 870, Deskjet 870Cxi, Deskjet 890, Laserjet 1100, Laserjet 2100, Laserjet 2100M, Laserjet 4000N, Laserjet 4L, Laserjet 5, Laserjet 5L, Laserjet 5MP, Laserjet 6L, Laserjet 6MP, Laserjet 8000, Laserjet 8100, Laserjet 5000, Mopier 320, PaintJet XL300 | HP 660C | Deskjet 1000C, Deskjet 670C, Deskjet 710, Deskjet 720C, Deskjet 722C, Deskjet 820C | Laserjet 3100 |
| IBM | Jetprinter 3852, Lexmark, Optra Color 1200, Optra Color 1275, Optra Color 40, Optra Color 45, Optra E+, Optra Ep, Optra S 1250 | 1020 Business, 3000, 5700, 7000 | | 1000, 1020, 1150, 2030, 2050, 2070, 5000, 7200, Winwriter 100, Winwriter 150c, Winwriter 200 |
| ed | PagePro 6, PagePro 8 | | | | |
| NEC | P2X | SuperScript 100C, SuperScript 1260, SuperScript 150C, SuperScript 650C, SuperScript 750C, SuperScript 860, SuperScript 870 | | | SuperScript 660i, SuperScript 660plus |
| Okidata | OL 410e, OL 610e/PS, OL 810e/PS, Okepage 6e, Okepage 6ex, Okepage 8c | Okipage 4w | | Okipage 8w, Okijet 2010 |
| Olivetti | JP350S | | | | |
| Panasonic | KX-P1123, KX-P4440, KX-P5400, KX-P8420, KX-P8475 | KX-P6500 | | KX-P6100, KX-P8410 |
| QMS | 2425 Turbo EX | | | | |
| Ricoh | 4801, 6000 | | | | |
| Xerox | DocuPrint C55, DocuPrint N17, DocuPrint N32 | | | | |

# 第 17 章 设置打印服务器

## 在 Red Hat Linux 中管理文档打印

Red Hat Linux 中的大多数打印操作可以通过 `lpr` 命令完成。通过 Red Hat `printtool`，你可以为每台打印机定义所需的过滤器，以便文本能够正确格式化。`lpr` 命令的选项可以添加过滤器来正确处理文本。管理打印文档的其他命令包括 `lpq`（查看打印队列内容）、`lprm`（从队列中删除打印作业）和用于控制打印机的 `lpc`。

还有用于将打印作业定向到远程打印机（例如 NetWare 或 SMB 打印服务器上的打印机）。如前所述，打印到 SMB 打印机可以使用 `smclient` 命令。同样，对于 NetWare 打印，有 `nprint` 命令。`lpr` 命令分别依赖这些命令来实现向 SMB 和 NetWare 打印。然而，如果你想在打印时选择不同的选项，可以直接使用 `smclient` 或 `nprint`。

第 6 章提供了如何以多种不同格式化和打印文档的示例，包括 `troff` 和 `TeX`。

## 使用 lpr 打印

使用 `lpr` 命令，你可以将文档打印到本地和远程打印机。文档文件可以添加到 `lpr` 命令行的末尾，或者通过管道（`|`）定向到 `lpr` 命令。以下是一个简单的 `lpr` 命令示例：

```
lpr doc1.ps
```

当你使用 `lpr` 指定文档文件时，输出将定向到默认打印机。作为个人用户，你可以通过设置 `PRINTER` 变量的值来更改默认打印机。通常，你会将 `PRINTER` 变量添加到你的其中一个启动文件中，例如 `~/.bashrc`。以下是如何将你的默认打印机设置为 `lp3`：

```
export PRINTER=lp3
```

要覆盖默认打印机，可以在 `lpr` 命令上指定特定的打印机。以下示例使用 `-P` 选项选择不同的打印机：

```
lpr -P lp3 doc1.ps
```

# 596 第四部分 ♦ Red Hat Linux 网络与服务器设置

要查看打印作业的详细信息，请如下所示使用 `lq` 的 `-l` 选项：

```
lq -l

lp0 is ready and printing      [job 010AudWypb]

root: active

/tmp/out.ps                13887 bytes
```

`-l` 选项显示作业编号。可以使用该数字删除单个作业（`lrm job#`）。

## 配置打印服务器

连接到你的 Red Hat Linux 系统的打印机可以通过不同的方式与网络上的其他计算机共享。你的计算机不仅可以充当 Linux 打印服务器，还可以向其他客户端计算机显示为 NetWare 或 SMB 打印服务器。一旦本地打印机连接到你的 Red Hat Linux 系统，你就可以使用本节中的程序通过 Linux (UNIX)、NetWare 或 SMB 接口与客户端计算机共享。

## 使用 lpd 配置共享打印机

一旦将本地打印机添加到你的 Red Hat Linux 计算机上要让网络上的其他计算机可以使用它就相当简单。如果共享打印机的计算机之间存在 TCP/IP 网络连接，那么你只需要授予远程主机上的单个主机或用户访问你计算机打印服务的权限即可。设置本地打印机的程序在本章前面讨论过。

要让远程计算机访问你的本地打印机，你必须将远程计算机的名称添加到以下文件之一：

- `/etc/hosts.equiv` — 此文件中列出的主机名被授予访问你的 Red Hat Linux 系统上任何打印机的权限。此文件被多个不同的服务（如远程打印和远程登录）用于，允许此文件中提到的主机的用户自动访问这些服务。

- `/etc/hosts.lpd` — 与 hosts 文件不同，此文件中列出的主机并不被授予访问你计算机主机的权限。然而，`hosts.lpd` 文件中的主机被授予访问你打印服务的权限。这是允许计算机访问你的打印机而无需开放你计算机上其他服务访问的好方法。

一旦你启用了主机对打印机的访问，有一个选项允许你限制来自访问打印机的主机的用户访问。通过在你的 `/etc/printcap` 文件中的共享打印机条目中放置 `rs` 选项，仅允许来自已批准主机且在本地 Linux 计算机上拥有用户账户的用户访问打印机。要学习如何在 Red Hat Linux 客户端上设置此打印机，请参阅本章前面关于添加远程 UNIX 打印机的节。

## 配置共享 NetWare 打印机

Red Hat Linux 提供的 NetWare 服务器功能通过 `mars_nwe` 包提供。该包允许从 Red Hat Linux 进行文件和打印机共享，就像所共享的资源来自 NetWare 服务器一样。虽然没有提供所有的 NetWare 功能，但 `mars_nwe` 包在基础文件和打印机共享方面表现良好。

请参阅第18章有关设置 `mars_nwe` 包以共享 NetWare 资源的信息。

你可以通过向 `/etc/nswerv.conf` 文件添加条目，使你的 Red Hat Linux 打印机作为 NetWare 打印机可用。此文件用于配置大多数 `mars_nwe` 信息。我们对添加打印机特别感兴趣的是打印队列部分（第21节）。Red Hat 打印机通过将每行指定为第21条目来识别为 NetWare 打印队列。这是一个示例：

```
21 PSPRINT SYS:/PRINT/PSPRINT lpr -Ppsprint
```

数字 `21` 将该条目识别为 NetWare 打印队列。`PSPRINT` 是队列的名称。队列目录被识别为 `SYS/PRINT/PSPRINT`。注意，队列目录与 `lpd` 缓存目录不同。最后，条目的最后部分用于打印提交到此打印队列的文档的 `lpr`命令行。

## 配置共享 Samba 打印机

你可以使用 Samba `SWAT` 程序（Samba Web 管理工具）将你的 Red Hat Linux 打印机配置为 SMB 打印机。要使用 SWAT，你需要安装 `samba` 包并配置 `swat` 服务，以便 SWAT 可以在你的浏览器窗口中打开。你还需要与将使用你打印机的客户端计算机之间建立 TCP/IP 连接。

第18章描述了如何设置 Samba 和 SWAT 以在浏览器中使用。

配置 SWAT 后，你可以通过在本地计算机上打开 Netscape 并在位置框中输入以下地址来打开该程序：

```
http://localhost:901/
```
