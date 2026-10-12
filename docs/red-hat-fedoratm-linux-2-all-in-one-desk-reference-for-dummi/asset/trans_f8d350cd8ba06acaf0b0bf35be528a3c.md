

然后从 CD-ROM 安装 Microsoft Office。安装 Microsoft Office 后，你可以直接从 GNOME 或 KDE 桌面访问 Office 应用程序。

CrossOver Office 使用 Wine —— 一种基于 X 窗口系统的开源 Windows Win32 和 Win16 应用程序编程接口（API）实现，旨在 UNIX 和 Linux 系统上运行。Wine 包含 Wine 加载器和 Winelib。Wine 加载器可以加载并运行 Windows 应用程序。Winelib 用于在 Linux 中编译和链接 Windows 应用程序。Wine 可免费下载自 [www.winehq.com](https://www.winehq.com)。

CodeWeavers 使用自定义版本的 Wine 创建了 CrossOver Office，以确保 Microsoft Office 应用程序，特别是 Microsoft Word、Excel 和 PowerPoint（来自 Office 97 或 Office 2000）能在 Wine 上正常运行。CodeWeavers 对 CrossOver Office 收取少量费用——单份许可列表价为 54.95 美元（多份购买可享更低成本）——但对 Wine 的所有修改都会回馈给 Wine 项目。因此，Wine 开源项目受益于 CrossOver Office 的销售。

你可以在 CodeWeavers 网站（[www.codeweavers.com/products/office/](https://www.codeweavers.com/products/office/)）上了解更多关于 CrossOver Office 的信息并购买该产品。

## aspell 拼写检查器

aspell 实用程序是一个交互式拼写检查工具。你可以用它来检查文本文件中单词的拼写。为此，只需在终端窗口中输入以下命令：

```
aspell check filename
```

如果你想试用 aspell，请输入一些笔记并将它们保存为名为 notes.txt 的文本文件（文件名可以是任意名称，但我在本节中使用此文件名）。要对该文件运行拼写检查器，请在终端窗口中输入以下命令：

```
aspell check notes.txt
This note describes the *concensus* reached during the August
   16 meeting.
   1) consensual    6) consensous
   2) con census    7) consciences
   3) con-census    8) incenses
   4) condenses     9) consensual’s
   5) concens       0) consensuses
   i) Ignore       I) Ignore all
   r) Replace      R) Replace all
   a) Add          x) Exit
   ?
```

从第二行开始的所有内容都是 aspell 显示的内容。当 aspell 发现拼写错误的单词（任何未出现在其词典中的单词）时，它会显示包含该拼写错误单词（*concensus*）的句子，并通过在一对星号内包围该单词来突出显示它。在该句子下方，aspell 列出了可能的更正选项，并从 1 开始依次编号。在这种情况下，aspell 将 *con census* —— 正确的选择 —— 列为 *concensus* 的第一个更正选项。

在句子之后，aspell 显示一个包含 16 个选项的列表——10 个编号为 0 到 9，6 个用单个字母 i, r, a, l, R 和 x 标记——后跟一个问号提示。你必须按下列表中显示的数字或字母之一，以指示你希望 aspell 执行的操作。编号选项显示了拼写错误单词的 10 个可能替换词。以下是字母选项的含义：

- 空格键表示本次接受该单词。
- i 表示忽略该拼写错误的单词。
- I 表示忽略该单词的所有出现。
- r 表示替换此次出现（你必须输入一个替换单词）。
- R 表示替换所有出现（你必须输入一个替换单词）。
- a 表示接受该单词并将其添加到你的私人词典中。
- x 表示保存文件的剩余部分并退出，忽略拼写错误。

![](img/9f89727199836b0f871f1745838aa8b2_202_0.png)

这些选项区分大小写。请确保没有启用大写锁定（Caps Lock）。

## 数据库

Fedora Core 附带两个关系型数据库——PostgreSQL 和 MySQL。我将简要向你展示如何使用 PostgreSQL。

*PostgreSQL*（发音为 *Post Gres Que Eel*），是一个强大且流行的*关系型数据库*（一种作为连接表集合工作的数据库类型）。你可以使用结构化查询语言（SQL）来处理数据库。

PostgreSQL 由一个开发团队开发，并根据 BSD（伯克利系统开发）开源许可证分发。该许可证对 PostgreSQL 源代码的使用方式没有限制。为了跟踪 PostgreSQL 的最新发展，请访问 [www.PostgreSQL.org](https://www.PostgreSQL.org)。

要检查你的系统上是否安装了 PostgreSQL，请输入 `rpm -qa postgresql`。你会看到至少三个 RPM 的列表——*postgresql*、*postgresql-libs* 和 *postgresql-server*。如果消息告知你这些软件包未安装，你可以使用以下步骤从本书配套 DVD 中安装它们：

1. 以 root 身份登录，并将 DVD 插入 DVD 光驱。
   - 如果你正在使用 GNOME 或 KDE，DVD 会自动挂载。如果没有，请在终端窗口中输入以下命令来挂载 DVD：
     ```
     mount /mnt/cdrom
     ```
   - 如果你有一个主 CD-ROM 光驱并添加了第二个 DVD/CD 光驱，请输入 `mount /mnt/cdrom1` 来挂载 DVD。

2. 输入以下命令来安装 PostgreSQL：
   ```
   cd /mnt/cdrom/Fedora/RPMS
   rpm -ivh postgresql*
   ```
   使用 PostgreSQL 所需的软件包将安装到你的系统上。

要使用 PostgreSQL，你必须首先以 **root** 身份登录，并使用以下命令启动数据库服务器：

```
service postgresql start
```

PostgreSQL 服务器进程启动，称为 *postmaster*。服务器是一个守护进程（一个连续在后台运行的进程），它接受来自客户端进程的数据库查询，并代表客户端执行数据库任务（如添加表）。

如果你希望 PostgreSQL 数据库服务器在系统每次启动时都启动，请输入以下命令来启用它：

```
chkconfig postgresql on
```

现在，你必须设计一个数据库，在 PostgreSQL 中创建该数据库，并将数据加载到其中。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

### 添加数据库用户

PostgreSQL 拥有独立于 Linux 用户账户的自身用户概念。要允许用户访问你系统上的 PostgreSQL 数据库，你必须将该用户名添加为 PostgreSQL 用户。

要添加 PostgreSQL 用户，请遵循以下步骤：

1. 以 root 身份登录。然后在终端窗口中输入以下命令：
   ```
   su - postgres
   ```
   你以 *postgres* 身份登录——这是 PostgreSQL 数据库服务器运行的用户名。你必须在此用户名下执行 PostgreSQL 管理任务。

2. 在终端窗口中输入以下命令：
   ```
   createuser
   ```
   此实用程序允许你添加 PostgreSQL 用户。程序会提示输入要添加的用户名：

3. 输入你授予数据库权限的用户的 Linux 用户名。
   例如，要添加我自己作为用户，我输入我的 Linux 用户名 *naba*。

4. 回答接下来的两个提示：
   ```
   Shall the new user be allowed to create databases? (y/n)
   Shall the new user be allowed to create more new users? (y/n)
   ```
   通常，你不希望用户创建数据库或添加新用户，因此你按 N 键来回应这些提示。
   你可以使用此过程运行 `createuser` 并添加任意数量的数据库用户。

## 回顾构建数据库的步骤

遵循以下基本步骤序列来构建数据库：

1. 设计数据库。
   此步骤涉及定义将用于存储信息的表和属性。

2. 创建一个空数据库。
   在你添加表之前，数据库系统要求你构建一个空数据库。

3. 在数据库中创建表。
   在此步骤中，你使用 SQL 的 `CREATE TABLE` 语句定义表。

4. 将固定数据加载到表中。
   例如，如果你有一个制造商名称或出版商名称（对于书籍的情况）的表，你希望将该表加载已知信息。

5. 备份初始数据库。
   如果需要从头创建数据库，此步骤是必要的，以确保你可以做到这一点。

6. 将数据加载到表中。
   你可以从数据库的早期转储中加载数据，或者通过表单交互式加载。

7. 使用数据库。
   使用 SQL 命令进行查询、更新记录或插入新记录。

### 设计数据库

我的简单示例并未遵循数据库构建的所有可能步骤。对于这个示例，数据库设计步骤很琐碎，因为我的图书目录数据库仅包含一个表。该表的属性如下：

- 书籍标题，最多 50 个字符
- 第一作者姓名，最多 20 个字符
- 第二作者姓名（如果有），最多 20 个字符
- 出版商姓名，最多 30 个字符
- 页数，作为数字
- 出版年份，作为数字（如 2002）
- 国际标准书号（ISBN），作为 10 个字符的文本（如 0764567934）

我将 ISBN 存储为不包含典型书籍 ISBN 中嵌入的破折号。我还将 ISBN 用作表的主键，因为 ISBN 是书籍的全球识别系统。这意味着每个书籍条目必须有一个唯一的 ISBN，这对于书籍来说是真实的。

