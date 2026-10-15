
在本文正文中，通过 `SECTION`（章节）菜单，可以查看九个帮助主题区域中每个区域的可用文本列表。可以通过鼠标点击来选择所需的主题。

`man` 命令中最有用的命令是 `SEARCH`（搜索）。它能快速搜索并显示所需的帮助主题。当使用 `APROPPOS` 按钮停止搜索时，`xman` 会显示包含搜索词的主题列表。然而，`Apropos` 搜索并不是全文搜索。它只对每个 `man` 文本的关键词进行搜索。

`xman` 对鼠标的支持不仅限于选择和滚动文本。配合 `Shift` 键和鼠标中键可以在主题列表和显示的 `man` 文本之间快速切换。`Ctrl` 和鼠标中键可以显示 `OPTIONS`（选项）菜单。

遗憾的是，`xman` 的键盘快捷键与 `man` 的快捷键并不对应。特别是，光标方向键无法用于滚动帮助文本。下表总结了可用的快捷键：

#### xman 键盘快捷键

| 键 | 描述 |
| :--- | :--- |
| `F` / `B` | 向前或向后一页 |
| `Spacebar` | 向前一页 |
| `1` 到 `4` | 向前一到四行 |
| `Ctrl+S` | 搜索手册文本 |

#### tkman

与 `xman` 类似，`tkman` 提供了一个 `X` 接口来显示 `man` 页面。一旦成功安装 `tkman`（它需要安装编程语言 `Tcl` 和 `Tk` 等），`tkman` 相比 `xman` 具有以下优势：

## man - 所有命令的在线手册 73

![](img/b30873dd3d753687a59253fb9ad26a0b_100_0.png)

图 4.1 使用 `xman` 读取 `man` 文本。

- 通过简单双击高亮文本即可与其他页面进行交叉引用。
- 管理最近查看过的 `man` 文本列表。
- 在 `man` 文本内进行轻松搜索。
- 可以高亮文本片段并永久存储这些高亮内容。
- 丰富的配置可能性。

![](img/b30873dd3d753687a59253fb9ad26a0b_100_1.png)

图 4.2 使用 `tkman` 读取 `man` 文本。

## man 内部

`man` 的中心文件是 `/etc/man.config`。在该文件中，设置了各种文件的路径。该文件还包含了使用 `less` 程序来显示 `man` 文本的规范。（因此，当显示文本时，`man` 和 `less` 的键盘命令是相同的。）

通常，不需要修改 `man.config`。如果你想指定 `man` 搜索的额外目录，可以在 `/etc/profile` 中相应设置 `MANPATH` 环境变量。在标准配置下，`man` 在以下目录中搜索 `man` 文本：

```
/usr/man
/usr/local/man
/usr/X118R6/man
```

这些目录都包含从 `man1` 到 `man8` 的子目录，其中包含了源文件。为了能在屏幕上显示这些文本，必须使用 `groff` 程序将它们转换为 ASCII 格式。为了避免每次访问 `man` 页面都重复这种转换，格式化后的文本存储在各自的目录中（在上述目录中为 `cat`，或者在子目录中）。

# LINUX 特定于在线文档 77

通常情况下，Linux 发行版只提供极少数的常见问题解答（`FAQ`）（如果有的话，通常可以在 `/usr/doc/faq` 目录下找到）。

最有趣的是 `Linux FAQ`：当 Linux 出现问题时，这个文件应该是首选参考。它涵盖了如安装、兼容性问题、Linux 文件系统处理、X 窗口系统等主题。

### HOWTO – 它是如何工作的？

`HOWTO` 文本与 `FAQ` 文件的主要区别在于，它们是系统化构建的，并传授基础知识。`HOWTO` 文本是 Linux 关于安装、配置和硬件问题最重要的信息来源。唯一的缺点是许多文本内容相当详实。你获得的信息比你实际需要的多得多。

涵盖的主题包括：对特殊硬件组件的处理（`SCSI` 磁盘、`CD-ROM` 驱动器、磁带机、以太网卡、键盘）以及 Linux 使用的特殊功能（打印、网络配置，包括 `UUCP`、`Term` 和 `News` 等）。以 ASCII 格式计算，`HOWTO` 文本总共占用超过 4 MB —— 这比这本白书要稀有得多！（作为对比：本本的 `.tex` 文件占用高达 2 MB）。

`HOWTO` 文件通常位于 `/usr/doc/HOWTO`。在 Linux 下，`HOWTO` 文本有两种形式：普通版本和精简版本。精简版本位于 `mini` 子目录中，仅以 ASCII 格式存在。相反，“大型” `HOWTO` 也可以以其他格式提供（`other-formats` 子目录）。

最有趣的格式是 HTML 版本，它可以被任何 `WWW` 浏览器读取，而且由于不同的字体大小和交叉引用，它比 ASCII 版本更清晰、更容易阅读。

像往常一样，最新版本可以在互联网上找到：

```
http://metalab.unc.edu/LDP/HOWTO
```

作为一个一般原则，你应该始终检查所有在线文件的最后修改日期。偶尔，仍然存在一些文件，其内容已由于所描述程序的较新版本而早已过。

### Linux HOWTOs

| 3dfx | Busmouse | DNS | Esperanto |
| :--- | :--- | :--- | :--- |
| AX25 | CD-Writing | DOS-Win-to-Linux | Ethernet |
| Access | CDROM | DOS-to-Linux | Finnish |
| Alpha | Chinese | DOSEMU | Firewall |
| Assembly | Commercial | Danish | French |
| Benchmarking | Config | Distribution | Ftape |
| BootPrompt | Consultants | ELF | GCC |
| Bootdisk | Cyrillic | Emacspeak | German |
| Glibc2 | Multi-Disk | RPM | Tips |
| HAM | Multicast | Reading-List | UMSDOS |
| Hardware | NET-3 | ROOT-AID | UPS |
| Hebrew | NFS | SCSI-Programming | UUCP |
| INFO-SHEET | NIS | User-Group | |
| IPX | Networking-Overv | SRM | VAR |
| ISP-Hookup | Optical-Disk | VME | |
| Installation | Oracleing | VMS-to-Linux | |
| Intranet-Server | PCI | Serial-Programming | VMS2linux |
| Italian | PCMCIA | Shadow-Pass | Virtual-Services |
| Java-CGI | PPP | Slovenian | WWW |
| Kernel | Parallel-Process | Sound | WWW-MSQL |
| Keyboard-Console | Pilot | Sound-Playing | XFree86 |
| LinuxDoc+Emacs+IS | Polish | Spanish | XFree86-Video-Tim |
| MGR | PostgreSQL | Text-Terminal | |
| MILO | Printing | | |
| Mail | Printing-Usage | Thai | |

### Linux-Mini-HOWTOs

- 3-Button-Mouse Firewall-Piercing Man-Page Sendmail+UCP
- ADSL GIS-GRASS Modules Small-Memory
- ADSM-Backup GTK+-BSS-550 Multiboot-LILO Software-Building
- AI-Alife Hard-Disk-Upgrade QCD-Terminal Software-RAID
- Advocacy IC-Post-Program NFS-Root Soundblast-Awe
- Backup-With-FDS IP-Alias NFS-Root-Client StarOffice
- Battery-Powered IP-Masquerade Netscape+Pro Term-wall
- Boca IP-Subnetwork News-Leisfite TKR
- BogoMips ISP-Connectivity Offline-Mapping Token-Ring
- Bridge Install-ZIP Partition Ultra-DMA
- Bridge+Firewall Kernel Partition-Rescue Update
- Bzip2 LBX Path Upgrade
- Cable-Model LILO Pre-Install-Check VPN
- Clock Large-Disk Process-Accounting Visual-Bell
- Coffee Leased-Line Linux+00DS+Win95 Pro-AppX-Subset Win-Model-Share
