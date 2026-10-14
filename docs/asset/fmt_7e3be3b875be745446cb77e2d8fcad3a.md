
# 命令

命令由不同的部分组成。首先是参数或选项。当您按下 `ls` 时，会执行该命令。在此之前，您可以轻松编辑命令行、纠正选项或拼写错误。最常用的命令之一是 `ls`，您可以使用它或带指定的参数使用它。在控制台中输入 `ls` 即可显示您当前所在目录的内容。选项以前加连字符为标记。如果您输入 `ls -l`，将以详细的形式显示目录内容。除了文件名之外，您还会看到文件的创建日期、字节大小以及我们稍后将讨论的其他信息。最重要的选项之一（很多命令都有这个选项）是 `--help`。如果您输入 `ls --help`，将向您显示 `ls` 命令的所有选项。

通过 `ls`，您也可以查看其他目录。为此，您将要显示的目录作为参数传递。例如，要显示子目录 Desktop 的内容，请输入 `ls -l Desktop`。

# 文件与目录

要有效地与 Shell 工作，需要了解 Linux 下文件和目录结构的知识。目录是用于存放文件、程序或其他目录的文件夹。根目录位于层级结构的顶端，通过`/`进行访问。

`/home` 目录中包含每个用户的目录，其中存放着他们的个人文件。图 7 显示了 Linux 下的标准目录树，带有示例用户 yxz、linux 和 tux 的家目录（Home）。您的 Linux 系统的目录树在功能上是划分的（“文件系统标准”），在下一页的表格 7.1 中，您将获得 Linux 下标准目录的简要描述。

![](img/7c7b5e54e6579952ad3fd8bde9e1a136_132_0.png)

| 路径 | 描述 |
| :--- | :--- |
| / | 根目录（英语 root directory），目录树的起点 |
| /home | 用户文件的（私有）目录 |
| /dev | 代表设备硬件组件 |
| /etc/init.d | 系统配置的重要文件（脚本） |
| /usr/bin | 启动系统时已需要的通用命令 |
| /usr/sbin | 供系统管理员保留的命令 |
| /sbin | 供系统管理员保留且启动系统所需的命令 |
| /usr/include | C 编译器的头文件 |
| /usr/include/g++ | C++ 编译器的头文件 |
| /usr/share/doc | 各种文档文件 |
| /usr/share/man | 帮助文本（手册页） |
| /usr/src | 内核源码 |
| /usr/src/linux | 临时文件 |
| /tmp | 大的临时文件 |
| /var/tmp | 存放所有的应用程序 |
| /var | 配置文件（例如，从 /usr 链接） |
| /var/log | 日志文件 |
| /var/adm | 系统管理 |
| /lib | 库（用于动态链接程序） |
| /proc | 进程文件系统 |
| /usr/local | 可选软件 |
| /opt | 较大的系统 |

表格 7.1：Linux 下标准目录

# Bash 功能

Bash 的两个重要功能简化了工作：

字体 历史（History）：当您调用该命令时，按下按键。
- 扩展功能：如果没有带有该字母的文件，Shell 将补全字符串。

**文件操作**

您知道如何与 Shell 工作，哪些目录可以简化操作：

1. 要显示目录内容，请使用 `ls`。
2. 要查看内容，需要 `ls` 位于一级。
3. 使用 `mkdir`（英语 make directory）创建一个新的子目录。
4. 要查看移动是否成功，请使用命令 `cd`（英语 change directory）切换目录。
5. 如果您需要文件的副本，请使用命令 `cp`（英语 copy）。

## 示例：处理路径

另一个示例将向您展示如何在您的 SuSE Linux 系统的目录结构中导航。

- 使用 `cd` 切换到您的主目录。通过 `mkdir test2` 创建另一个子目录 `test2`。
- 使用 `cd test2` 切换该目录，并创建一个名为 `Unterverzeichnis` 的目录。通过仅按 `Tab` 键使用扩展功能来自动补全字符串的剩余部分。
- 现在您位于子目录中，需要在不切换目录的情况下移动之前创建的备份 `Testsicherung`。为此，您必须指定所需文件的路径。不要忘记命令 `mv ../test/Testsicherung .` 末尾的点，它将当前目录设置为移动的目标。通过使用两个点，可以将一个选定的文件分别移动到您的目录中。

# 通配符 (Wildcards)

通配符的进一步优势是这四个字符。“Wildcards”或通配符字符：

- `?` 替换任意一个字符。
- `*` 替换任意数量的字符。
- `[set]` 替换任意一个一个字符，但方括号内指定的字符除外（字符字符串“*set”）。
- `[set]]` 包含任意一个字符，但“set”中指定的字符除外。

如果您在目录中有文件 `Testdatei`、`Testdatei2` 和 `date`，并输入 `ls Testdatei`，您将获得 `Testdatei` 和 `Testdatei2`。通过 `ls *` 您还将获得文件 `Testdatei`。
`ls *` 命令将向您显示所有通配文件，而您可以使用通配符集匹配最后一个字符为数字的任何字符：`Testdatei[1-9]`。
最重要的始终是 `*` 通配符：通过使用它，您可以将一个目录中的文件复制到另一个目录或删除。例如，命令 `rm *date*` 会删除您 `test` 目录中所有名称中包含字符串“date”的文件。

# 更多或更少

两个小型程序允许您直接在 Shell 中查看文本文件。我们甚至不需要启动编辑器。要打开文件 `Datei.txt` 文件，只需输入 `less README.txt`。控制台窗口将只显示文本。使用方向键可以一直向下翻页，但您可以使用 `↑` 和 `↓` 键在文本中向前或向后移动。按 `G` 键退出程序。

该程序以“少即是多”为格言命名，不仅可以用于读取文本文件，还可以用于命令输出。相关内容请阅读本页的“重定向”部分。

此外可以使用较旧的程序 `more`，但它没有那么方便，因为您无法向前和向后翻页。

# 重定向

通常情况下，Shell 中的标准输出是您的显示器或控制台窗口，标准输入通过键盘进行。如果您想将一个命令的输出传递给程序，则必须使用所谓的“管道”（Pipeline）。

要查看 `test` 目录中的文件，请输入命令 `ls test | less`。在德语键盘上，通过同时按下 `Alt` 和带有字符 `<` 的键来获取符号 `|` 符号。您现在会在控制台中查看到 `test` 目录的内容。这仅在普通输出过于混乱时才有用。例如，使用 `ls /dev` 查看目录，您在窗口中只能看到内容的一部分，而通过 `ls /dev | all` 则可以列出所有文件。

如果您想将命令的输出保存到文件中，示例中的命令将是：`ls > Inhalt`。之后您将有一个名为“Inhalt”的新文件，其中包含 `test` 中的文件和目录。您可以使用 `less` 查看该文件。
相反，您可以使用文件作为命令的源。例如，通过 `sort < Testdatei` 让您自己编写的测试文件的行按字母顺序排序。命令的输出将在屏幕上显示。您现在可以看到之前编写的文本，它们已根据每行的首字母进行了排序。这在例如需要排序未排序的名称列表时非常有帮助。

# 7

如果您想创建一个带有排序列表的新文件，则必须将 `sort` 命令的输出重新重定向到文件中。如果您想理解这一过程，请在编辑器中创建一个无序列表 `Namensliste`，并将其保存为 `test` 目录下的 `liste`。

进入该目录并调用命令 `sort < liste > sortierteListe`。使用 `less` 查看新列表。

标准错误输出也是屏幕。如果您想将这些错误重定向到名为“Fehler”的文件，请在命令后输入：`2> Fehler`。使用 `>` 将输出同时重定向到标准输出和标准错误输出。如果在该处使用 `>>` 而不是 `>`，则输出将追加到现有文件中。

# 存档与数据压缩

在您已经创建了一些文件和目录之后，我们来看存档和数据压缩的主题。假设您想将 `test` 目录打包到一个文件中，以便将其保存到磁盘上或通过电子邮件发送。为此您使用 `tar` 命令。

- `-c` (engl. create) 创建新存档。
- `-t` (engl. table) 显示存档内容。
- `-x` (engl. extract) 解包。
- `-v` (engl. verbose) 在处理时显示所有文件。
- `-f` (engl. file) 指定文件名。

使用 Shell
SuSE Linux

现在要将目录中的所有文件打包成名为 `test.tar` 的存档，我们至少需要 `-c` 和 `-f` 选项。由于我们要跟踪存档过程，我们加上 `-v` 选项。使用 `cd` 进入该目录。现在的输入为：`tar -cvf test.tar`。使用 `tar -tf test.tar` 查看内容。这对硬盘上的目录保持不变。要解压存档，您必须输入 `tar -xvf test.tar`。如果我们想压缩存档文件以节省空间，请不要这样做。
推荐使用广泛的 `gzip`，即 `gzip test.tar`。现在输入 `ls`，您会看到 `test.tar` 文件消失了，取而代之的是一个 `test.tar.gz`。该文件更小，因此更容易发送。
现在应该将存档复制到 `test2`。您使用 `cp test.tar.gz test2`。使用 `cd test2` 进入目录。解包以 `.gz` 结尾的压缩文件使用 `gunzip` 命令，因此输入为 `gunzip test.tar.gz`。我们得到了 `test.tar` 文件，它仍需 `tar -xvf test.tar` 解析。您也可以直接为 `tar` 命令添加 `-z` 选项并解包压缩存档：`tar -xvzf test.tar.gz`。

通过输入 `ls` 您将看到有一个与主目录内容相同的新目录。

# mtools

`mtools` 组可以操作 MS-DOS 文件系统的命令。这对于磁盘驱动器的工作非常重要。在 MS-DOS 下可以通过 `a:` 调用驱动器。这些命令与 MS-DOS 下的命令相似，但显示如下：

- `mdir a:` - 显示驱动器 `a:` 磁盘的内容。
- `mcopy a:Testdatei a:` - 将文件 `Testdatei` 复制到磁盘上。
- `mdel a:Testdatei` - 删除 `a:` 上的 `Testdatei`。
- `mformat a:` - 使用 `fform` 命令以 MS-DOS 格式格式化磁盘。

`cd a:` - wechseln in Ihr aktuelle Verzeichnis.

`mkdir a:test` - erstellt das Unterverzeichnis test auf der Festplatte.

`rmdir a:test` - löscht das Unterverzeichnis test auf der Festplatte.

# 清理

In diesem Crash-Kurs haben Sie die wichtigsten Grundlagen im Umgang mit der Shell gelernt. Damit Ihr Heimatverzeichnis nicht zu unübersichtlich wird, sollten Sie Dateien und Verzeichnisse nicht einfach mit den Befehlen `rm` und `rmdir` wieder löschen.
Am Ende dieses Kapitels finden Sie eine Liste mit den wichtigsten Befehlen und entsprechenden Kurzbeschreibungen.

# Benutzerrechte

Linux wurde von Anfang an als Multiuser-System konzipiert, also für die gleichzeitige Nutzung durch mehrere Anwendungen. Daraus ergeben sich einige wichtige Unterschiede zu Microsoft System Windows.
Das deutlichste Unterscheidungsmerkmal ist der Zwang, sich zu Beginn einer Arbeitssitzung am System anzumelden. Dazu wird dem Benutzer ein eigener „Benutzername“ mit zugehörigen Passwort gewährt, dass Unbefugte keinen Einblick in für sie gesperrte Inhalte erhalten können. Größere Veränderungen am System, z. B. die Installation von Programmen, sind einem Benutzer in der Regel nicht oder nur beschränkt möglich. Nur root, der Administrator, verfügt über praktisch unbegrenzten Zugriff auf alle Dateien. Dieses Konzept ist sicher und nutzt sich, indem man sich nur bei Bedarf als root einloggt, was die Gefahr unbeabsichtigter Datenverluste stark eingrenzt: Da im Normalfall nur der Administrator Systemdateien löschen oder Festplatten formatieren kann, wird die Bedrohung durch Trojanische Pferde oder wesentlich eingegebene destrukt Befehle stark eingeschränkt.

# Rechte im Dateisystem

Grundsätzlich gehört jede Datei im Linux-Dateisystem einem Benutzer und einer Gruppe. Jeder dieser beiden Parteien, auch „Fremden“, können vom Besitzer Schreib-, Lese- sowie Ausführrechte zugiesen werden.

Als Gruppe werden Zusammenschlüsse von Benutzern mit bestimmten kollektiven Rechten bezeichnet. So ist eine solche Gruppe eine einem bestimmten Projekt arbeitende Arbeitsgruppe, nennen wir sie projekt3. Jeder Benutzer unter Linux ist Mitglied in mindestens einer Verwaltungseinheit, standardmäßig wird nur users eingetragen. Wir können nahezu beliebig Gruppen anlegen, allerdings ist nur root dazu. Jeder Benutzer kann mit dem Befehl herausfinden, in welcher Gruppe er Mitglied ist.

# Rechte auf Dateien

Betrachten wir die Rechtestruktur im Dateisystem genauer und beginnen mit den Dateien. Die Ausgabe von `ls -l` kann beisweise so aussehen:

```
