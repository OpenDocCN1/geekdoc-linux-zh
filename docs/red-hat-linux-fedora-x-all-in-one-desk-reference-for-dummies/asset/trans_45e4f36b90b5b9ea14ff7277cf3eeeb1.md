

# 数据库 181

然后将标准输入重定向自该文件运行 psql。例如，假设有一个名为 `sample.sql` 的文件包含一些你想在 `books` 数据库上尝试的 SQL 命令。那么，你通过以下命令运行 psql：

```
psql books < sample.sql
```

我通过这种方式使用 psql 来创建数据库表。

# 定义表

为了创建一个名为 books 的表，我编辑了一个名为 `makedb.sql` 的文本文件，并在文件中放置了以下行内容：

```sql
/*
* 表 'books' 的结构 world
*/
CREATE TABLE books (
  isbn CHAR(10) NOT NULL PRIMARY KEY,
  title CHAR(80),
  author1 CHAR(20),
  author2 CHAR(20),
  pubname CHAR(30),
  pubyear INT,
  pagecount INT
);
```

`CREATE TABLE books` 是创建一个名为 `books` 的表的 SQL 语句。语句末尾的 `@` 是 psql 命令。表的属性出现在括号括起来的行中

如果表包含固定数据，你还可以包含其他 SQL 语句（如 `INSERT INTO`），在表创建后立即将数据加载到表中

为了执行 `makedb.sql` 文件中创建 `books` 表的 SQL 语句，我如下所示运行 psql：

```
psql books < makedb.sql
```

现在 `books` 数据库包含一个名为 `books` 的表。（好吧，也许我应该给它们起不同的名字，但用相同的名字命名似乎很方便。）我现在可以向表中加载数据了。

![](img/d9230b719dc0efd80851f363d8c6f571_207_0.png)

# 182 数据库

# 向表中插入记录

将数据加载到表的一种方法是在另一个文件中准备 SQL 语句，然后将该文件作为输入运行 psql。例如，假设我想向 `books` 表添加以下书籍信息：

```
isbn = '0765441331'
title = 'Red Hat Linux 9 Professional Secrets'
author1 = 'Naba Barkakati'
author2 = NULL
pubname = 'Wiley Publishing, Inc.'
pubyear = 2003
pagecount = 1070
```

然后，下面的 SQL 语句将这些信息加载到 `books` 表：

```sql
INSERT INTO books VALUES
('0765441331', 'Red Hat Linux 9 Professional Secrets',
'Naba Barkakati', NULL,
'Wiley Publishing, Inc.', 2003, 1070); \g
```

另一方面，假设各个可用字段的顺序不同（即 `CREATE TABLE` 语句定义表属性的顺序）。在这种情况下，你可以使用 `INSERT INTO` 命令的不同形式来添加行，如下例所示：

```sql
INSERT INTO books (pubyear, author1, author2, title)
(1996, 'Naba Barkakati', NULL, 'Linux SECRETS', 900, 'IDG Books Worldwide', '1568798X'); \g
```

本质上，你必须列出属性以及对应的值，并确保属性的顺序与值的顺序匹配

如果我将所有的 `INSERT` 命令保存在名为 `additems.sql` 的文件中，我可以通过 psql 命令行使用 `\i` 命令按如下方式加载数据库（输入 `psql books` 来启动 PostgreSQL 客户端）：

```
books=> \i additems.sql
```

# 查询数据库

你可以通过 `psql` 交互式程序交互地查询数据库。（当然，你必须了解 SQL 才能此操作。）例如，为了查询 `books` 数据库，我使用以下命令启动 SQL 客户端：

# 183 多媒体应用

psql books

```
books=> select isbn, title from books where pubyear > 2002 \
isbn | title
0764452583 | Red Hat Linux All-in-One Desk Reference for Dummies
0764451331 | Red Hat Linux 9 Professional Secrets
(2 rows)
books=> \q
```

![](img/d9230b719dc0efd80851f363d8c6f571_209_0.png)

第二 卷
第 4 章

核心应用程序
探索 Fedora

# 多媒体应用

Fedora Core 包含相当少的多媒体应用——主要是多媒体音频播放器和 CD 播放器，还有用于数码相机和刻录 CD-ROM 的应用程序。要播放其他多媒体文件（如 MPEG 视频），你必须在 Fedora Core 系统下载并安装额外的软件。这里是一些典型的多媒体任务以及你可以用于执行这些任务的应用程序概述：

- **使用数码相机：** 使用 Digital Camera 工具从 Fedora Core 中的数码相机下载照片。
- **播放音频 CD：** 使用 Fedora Core 可以的许多音频 CD 之一。
- **播放声音文件：** 使用 Rhythmbox 或 XMMS 多媒体音频播放器（你需要下载一些额外的软件来用 Rhythmbox 或 XMMS 播放 MP3 文件）。你也可以从互联网下载其他播放器。
- **刻录 CD：** 使用 X-CDast 刻录你的 CD。

# 使用数码相机

Fedora 带有 gtcam 这是一个数码相机应用程序，你可以用它从数码相机下载照片。gtcam 是 gPhoto2 命令行应用程序的 GUI 前端

# 184 多媒体应用

gPhoto2 网站 (www.gphoto.org/proj/libphoto2/support.php) 用于支持的相机列表。

要使用 gtcam 使用你的数码相机，请遵循以下步骤：

1. 将数码相机连接到串口或 USB 端口（取决于接口）并打开相机。
2. 选择 Graphics:Digital Camera 启动 gtcam。
3. 从 gtcam 菜单选择 Add:Camera。
4. 在弹出的对话框中点击 Detect。

如果你的相机被支持，我将在步骤末尾描述一种替代方法。gtcam 显示相机图标，相机名称在左侧面板。

5. 双击相机图标，gtcam 在右侧面板显示缩略图。
6. 点击选择你想下载的照片；然后点击工具栏上的 Save。

gtcam 下载图像并将每个图像放置在你的主目录下。你现在可以在 GIMP 或你喜欢的编辑器中编辑照片。

> 如果 gtcam 无法识别你的数码相机，不要沮望。你仍然可以将存储介质（例如存储卡）作为 USB 存储设备，只要你的相机支持 USB 存储。要访问 USB 相上的图像，请遵循以下步骤：

![](img/d9230b719dc0efd80851f363d8c6f571_210_0.png)

1. 读取相机说明并使用相机的菜单选项将 USB 设置为 Mass Storage。

如果相机不支持 USB Mass Storage，你无法使用此过程访问照片。

2. 使用相机自带电缆将数码相机连接到 USB 端口并打开相机。

3. 输入以下命令挂载相机存储介质：

```
mount /mnt/camera
```

相机图标出现在 GNOME 桌面上。

5. 双击 GNOME 桌面的相机图标。

相机的内容出现在 Nautilus 文件管理器中。你可以双击文件夹找到包含照片的文件夹。通常这些数字照片是带有 .jpg 扩展名的 JPEG 文件。在默认视图下，Nautilus 显示照片的缩略图，所以你不需要担心加密文件名。

6. 点击选择照片将其复制到硬盘。

你也可以在终端中使用 `cp` 命令将所有或部分图像复制到硬盘上的目录。例如，为了将所有 JPEG 照片复制到当前目录，输入

```
cp /camera/*.jpg
```

# 185 多媒体应用

3. 要查看相机是否被检测，输入以下命令：

```
cat /proc/bus/devices
```

输出显示相机为质存储设备。从第二个 T: 行开始的所有行都涉及 Nikon Coolpix 2500 相机。你可以在输出中看到一些细节，如制造商名称和相机型号。

