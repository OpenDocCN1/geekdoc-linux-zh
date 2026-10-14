

每个用户在 /home 目录下都有一个分支用于存放自己的文件，称为其主目录。上一幅图中的层级结构有两个主目录：joe 和 jon，它们都是 /home 的子目录。

![](img/be7f02611e5cefde1a18c788fede22f7_159_0.png)

Figure 5-1. The root directory tree.

当你在使用 shell 时，你始终位于系统上的某个目录中，该目录称为当前工作目录。当你首次登录系统时，你的主目录就是当前工作目录。

在向工具或应用程序指定文件名作为参数时，你可以给出相对于当前工作目录的以斜杠分隔的路径名。例如，如果 /home/joe 是当前工作目录，你可以使用 "work" 来指定目录 /home/joe/work，而使用 "work/schedule" 来指定 /home/joe/work 目录中的文件 schedule。

每个目录都有两个特殊文件，其名称由一个和两个句点组成：.. 指的是当前工作目录的父目录，而 . 指的是当前工作目录本身。如果当前工作目录是 /home/joe，你可以使用 . 来指定 /home/joe，而使用 .. 来指定 /home。此外，你可以指定 /home/jon 目录为 ../jon。

指定文件名的另一种方法是指定从根目录（/）开始，一直到要指定的文件为止的所有目录分支的以斜杠分隔的列表。从根目录到文件的这种唯一、特定的路径称为文件的 *full path name*。 （当引用一个不是目录的文件时，这有时被称为 *absolute file name*）。

你可以通过给出其完整路径名来指定系统上的任何文件或目录。文件可以与系统上不同目录中的其他文件同名，但没有两个文件或目录可以共享相同的完整路径名。例如，用户 `joe` 可以在其 `/home/joe/work` 目录中有一个文件 `schedule`，也可以在其 `/home/joe/play` 目录中有一个文件 `schedule`。虽然这两个文件同名（`schedule`），但它们位于不同的目录中，因此每个都有唯一的完整路径名——`/home/joe/work/schedule` 和 `/home/joe/play/schedule`。

然而，你不必键入工具或应用程序的完整路径名即可启动它。shell 维护一个目录列表，称为 *path*，它会在其中搜索程序。如果程序“在你的路径中”，即位于这些目录之一中，你只需键入其名称即可运行它。

默认情况下，路径包括 `/bin` 和 `/usr/bin`。例如，`who` 命令位于 `/usr/bin` 目录中，因此其完整路径名为 `/usr/bin/who`。由于 `/usr/bin` 目录在路径中，你可以键入 `who` 来运行 `/usr/bin/who`，无论当前工作目录是什么。

下表描述了 Linux 系统上的一些标准目录。

| Directory | Description |
|---|---|
| `/` | 系统上所有目录的祖先；所有其他目录都是此目录的子目录，无论是直接还是通过其他子目录。 |
| `/bin` | 基本工具和其他程序（或 *binaries*）。 |
| `/dev` | 表示系统各种硬件 *devices* 的文件。例如，你使用文件 `/dev/cdrom` 来访问 CD-ROM 驱动器。 |
| `/etc` | 各种系统配置文件、启动文件，*et cetera*。 |
| `/home` | 系统所有用户的 *home* 目录。 |
| `/lib` | `/bin` 中工具使用的基本系统 *library* 文件。 |
| `/proc` | 提供有关当前系统 *processes* 信息的文件。 |
| `/root` | 超级用户的家目录，其用户名为 root。 （过去，超级用户的主目录只是 /；后来采用 /root 用于此目的，以减少 / 中的杂乱。） |
| `/sbin` | 基本系统管理员工具，或系统二进制文件。 |
| `/tmp` | 临时文件。 |
| `/usr` | 与用户工具和应用程序相关的子目录中的文件。 |
| `/usr/X11R6` | 与 X Window System 相关的文件，包括仅在 X 下运行的那些程序（在 /usr/X11R6/bin 中）。 |
| `/usr/bin` | 用户的工具和应用程序。 |
| `/usr/dict` | 词典和词表（正逐渐被 /usr/share/dict 取代）。 |
| `/usr/doc` | 各种系统文档。 |
| `/usr/games` | 游戏和娱乐。 |
| `/usr/info` | Gnu Info 超文本系统（见 Recipe 2.8.5 [Reading an Info Manual], page 48）的文件。 |
| `/usr/lib` | /usr/bin 中工具使用的库。 |
| `/usr/local` | 本地文件——特定于单个系统的文件——包括本地文档（在 /usr/local/doc 中）和程序（在 /usr/local/bin 中）。 |
| `/usr/man` | 在线手册，可通过 man 命令阅读（见 Recipe 2.8.4 [Reading a Page from the System Manual], page 46）。 |
| `/usr/share` | 已安装应用程序的数据，其与体系结构无关且可在系统之间共享。 这里出现了许多与 /usr 中等价的子目录，包括 /usr/share/doc、/usr/share/info 和 /usr/share/icons。 |

