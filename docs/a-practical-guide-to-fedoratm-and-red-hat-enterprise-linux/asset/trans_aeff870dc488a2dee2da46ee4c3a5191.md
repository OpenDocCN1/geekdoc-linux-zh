
## 表达式参考

| **表达式** | **匹配内容** |
|---|---|
| `xyz)+` | `xyz` 所匹配内容的一次或多次出现 |
| `xyz)?` | `xyz` 所匹配内容的零次或一次出现 |
| `xyz)*` | `xyz` 所匹配内容的零次或多次出现 |
| `xyz\`abc` | `xyz` 或 `abc` 所匹配的内容之一（在 vim 中使用反斜杠 \） |
| `(xy\|ab)c` | `xyc` 或 `abc` 所匹配的内容之一（在 vim 中使用反斜杠 \） |

表 A-12 列出了在 sed 和 vim 替换字符串中具有特殊含义的字符。

| **字符串** | **表示含义** |
|---|---|
| `&` | 正则表达式（搜索字符串）所匹配的内容 |
| `\n` | 加引号的数字，*n*，表示搜索字符串中第 *n* 个括号括起来的正则表达式所匹配的内容 |
| `$n` | 美元符号后跟的数字，*n*，表示搜索字符串中第 *n* 个括号括起来的正则表达式所匹配的内容（仅限 Perl） |

## 附录 B：帮助

你不需要孤立地作为用户或系统管理员。一个庞大的 Linux 专家社区愿意协助你了解 Linux 系统、帮你解决问题并最大限度地发挥 Linux 系统的优势。然而，在寻求帮助之前，请确保你已经尽一切努力自行解决问题。毫无疑问，在你之前一定有人遇到过同样的问题，而你问题的答案在互联网的某个角落一定存在。你的任务就是找到它。本附录列出了资源，并介绍了可以帮助完成这一任务的方法。

### 本附录内容

- 解决问题 ... 1150
- Linux 新闻组 ... 1152
- 邮件列表 ... 1153
- 指定终端 ... 1153

## 解决问题

以下是一系列可以帮助你在不求助于他人的情况下解决问题的步骤。根据你对所涉及硬件和软件的理解程度及经验，这些步骤可能会引导你找到解决方案。

1. Fedora/RHEL 附带了详尽的文档。阅读你遇到问题的那款特定硬件或软件的文档。如果它是 GNU 产品，请使用 `info`；否则，使用 `man` 查找本地信息。此外，请查看 `/usr/share/doc` 以获取关于特定工具的文档。更多信息请参见第 113 页的“获取帮助”和第 128 页的“从命令行获取帮助”。
2. 当问题涉及某种错误或其他信息时，使用搜索引擎（如 Google (www.google.com) 或 Google Groups (groups.google.com)）在互联网上查找该信息。如果信息较长，请选取信息中独特的一部分进行搜索；10 到 20 个字符通常就足够了。将搜索字符串用双引号括起来。关于此类搜索的示例，请参见第 113 页的“使用互联网获取帮助”。
3. 检查 Linux Documentation Project (www.tldp.org) 是否有关于相关主题的 HOWTO 或 mini-HOWTO。在其网站上搜索与产品和直接相关的关键词。阅读常见问题解答（FAQs）。
4. GNU 手册可在 www.gnu.org/manual 获取。此外，你可以访问 GNU 主页 (www.gnu.org) 以获取其他文档和 GNU 资源。许多 GNU 页面和资源有多种语言版本。
5. 使用 Google 或 Google Groups 搜索与产品和直接相关的关键词。
6. 当其他方法都失败时（或者也许在你尝试其他方法之前），检查 `/var/log` 中的系统日志。首先使用以下命令查看 `messages` 文件的末尾：
   ```bash
   # tail -20 /var/log/messages
   ```
   如果 `messages` 中没有有用的内容，请运行以下命令。它会按时间顺序显示日志文件的名称，最近修改的文件将出现在列表的底部。
   ```bash
   $ ls -ltr /var/log
   ```
   首先查看列表底部的文件。如果问题涉及网络连接，请审查本地和远程系统中的 `secure` 文件。同时在远程系统中查看 `messages` 文件。
7. `/var/spool` 目录包含带有有用信息的子目录：`cups` 保存打印队列；`postfix`、`mail` 或 `exim4` 保存用户的邮件文件；等等。

如果你无法自行解决问题，向合适的新闻组（见下页）或邮件列表（见第 1153 页）提出经过深思熟虑的问题，通常能获取有用的信息。发送或发布问题时，请确保仔细描述问题并识别本地系统。包括 Fedora/RHEL 以及与问题相关的任何软件包的版本号。如有必要，请描述硬件。发布问题有一套礼仪——请参阅 www.catb.org/~esr/tags/smart-questions.html，这是 Eric S. Raymond 和 Rick Moe 的一篇好文章，题为 *如何聪明地提问*。付费情况下，Red Hat 提供多种类型的支持。

作者的主页 (www.sobell.com) 包含对本书的更正、选定章节练习的答案以及其他 Linux 站点的指引。

## 查找 Unix/Linux 信息

Fedora/RHEL 附带了在线存储的参考页。你可以使用 `man`（见第 128 页）或 `info`（见第 131 页）实用程序阅读这些文档。你可以阅读 `man` 和 `info` 页面，在阅读本书时获取更多关于特定主题的信息，或确定 Linux 提供了哪些功能。要搜索主题，请使用 `apropos`（见第 130 页）或输入命令 `man apropos`。

### 桌面输入设备

Linux 上有许多图形应用程序可用；表 B-1 列出了其中的一些。

**表 B-1 桌面输入设备**

| **站点** | **关于该站点** | **URL** |
| :--- | :--- | :--- |
| openoffice.org | openoffice.org 套件包括文字处理、电子表格、演示文稿、图形和数据库应用程序。 | openoffice.org |
| LibreOffice | LibreOffice 套件包括文字处理、电子表格、演示文稿、图形和数据库应用程序。 | libreoffice.org |
| Thunderbird | Thunderbird 是一个跨平台的电子邮件、新闻和聊天客户端。 | mozilla.org/thunderbird |
| Firefox | Firefox 是一个 Web 浏览器。 | mozilla.org/firefox |
| Blender | Blender 是一个用于建模、动画、渲染、后期制作、交互式创建和播放（游戏）的套件。 | blender.org |

**表 B-1 桌面应用程序（续）**

| **站点** | **关于该站点** | **URL** |
| :--- | :--- | :--- |
| gimp | GIMP（GNU 图像操纵程序）是用于照片修饰、图像合成和图像创作等任务的软件。 | gimp.org |
| audacity | Audacity 是一个多轨道音频编辑器和录音机。 | audacity.sourceforge.net |
| ImageMagick | ImageMagick 是一个用于创建、编辑、合成或转换位图图像的软件套件。 | imagemagick.org |
| pico | Pico 是原本用于 `pine` 邮件系统的文本编辑器。 | accc.uic.edu/service/shell_accounts/pico |

## 编程语言

运行 Linux 可以让你访问广泛的编程语言；表 B-2 列出了其中的一些。

**表 B-2 编程语言**

| **站点** | **关于该站点** | **URL** |
| :--- | :--- | :--- |
| PostgreSQL | PostgreSQL 是一个强大的对象关系数据库系统；`postgresql-server` 软件包。 | postgresql.org |
| C | C 是一种通用编程语言；`gcc` 软件包。 | wikipedia.org/wiki/C_(programming_language) gcc.gnu.org |
| Perl | Perl 语言是一种通用编程语言；`perl` 软件包。 | perl.org |
| PHP | PHP 是一种适合 Web 开发的通用脚本语言，可以嵌入到 HTML 中；`php` 软件包。 | php.net |

## Linux 新闻组

获取特定信息的最佳方式之一是通过新闻组。通常，通过阅读新闻组的帖子就能找到问题的答案。尝试使用 Google Groups (groups.google.com) 搜索新闻组，看看你的问题是否已经被问过并得到回答。或者，打开一个新闻阅读器程序并订阅合适的新闻组。如有必要，你

