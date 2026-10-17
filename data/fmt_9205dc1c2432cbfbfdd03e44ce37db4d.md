
# Linux 入门指南

在 dummies.com 获取免费电子贴士

Dee-Ann LeBlanc

Linux 讲师

![](img/e40c80c470cf7ea45bb6271fce82ad29_0_0.png)

## 获取帮助

| 命令 | 说明 |
|---|---|
| `apropos [keyword]` | 在数据库中搜索包含关键词的命令。 |
| `info [command]` | 以另一种格式显示文件的帮助信息。 |
| `man [command]` | 显示文件的帮助信息。 |
| `whatis [command]` | 显示命令的简短描述。 |

## 常用命令

| 命令 | 说明 |
|---|---|
| `cat [filename]` | 将文件内容显示到标准输出设备（通常是你的显示器）。 |
| `cd [/directory]` | 切换目录。 |
| `chmod [options] mode filename` | 更改文件的权限。 |
| `chown [options] filename` | 更改文件的所有者。 |
| `cp [options] source destination` | 复制文件和目录。 |
| `date [options]` | 显示或设置系统日期和时间。 |
| `df [options]` | 显示已用和磁盘空间。 |
| `du [options]` | 显示每个文件的空间。 |
| `file [filename]` | 确定文件中数据的类型。 |
| `find [pathname] [expression]` | 搜索匹配模式的文件。 |
| `grep [options] pattern [filename]` | 在文件或输出中搜索特定模式。 |
| `kill [options] pid` | 停止进程。如果进程拒绝停止，请使用 `kill -9 pid`。 |
| `less [filename]` | 逐页查看文件内容。 |
| `ln [options] source [destination]` | 创建快捷方式。 |
| `lpr [options]` | 发送打印作业。 |
| `ls [options]` | 列出目录内容。 |
| `mkdir [options]` | 创建新目录。 |
| `mv [options] source destination` | 重命名或移动文件或目录。 |
| `passwd [name] [password]` | 更改密码或允许（系统管理员）更改任何密码。 |
| `ps [options]` | 显示当前运行进程的快照。 |
| `pwd` | 显示当前目录的路径。 |
| `rm [options] directory` | （删除）文件和或目录。 |
| `rmdir [options] directory` | 删除空目录。 |
| `su [options] [user [arguments]]` | 切换到另一个用户。 |
| `tail [options] [filename]` | 显示文件的最后 n 行（默认为 10）。 |
| `tar [options] filename` | 从 tar 文件 (`*.tar`) 或存档 (`*tar.gz` 或 `.tgz`) 中存储和提取文件。 |
| `who [options]` | 显示登录用户。 |

### CD-ROM 操作

| 发行版 | 命令/操作 |
|---|---|
| Red Hat 和 Mandrake | **访问**：如果你处于 GUI 环境，红帽应该在插入 CD 时自动看到它。如果你在命令提示符处，执行 `mount /mnt/cdrom`。 |
| | **移除**：如果你处于 GUI 环境，右键点击桌面上的 CD 图标，然后选择“弹出”。如果你在命令行，利用 `umount /mnt/cdrom` 将 CD 从你的文件系统中移除，然后手动弹出它。 |
| SuSe | **访问**：你可能需要尝试几种方法来确定在 SuSE 中具体该使用什么。在命令行中，从尝试 `/media/cdrom` 开始。如果这不起作用，最简单的方法是尝试 `mount -t iso9660 /dev/device /media/cdrom`，其中 device 是 `hda`、`hdb`、`hdc` 等，直到成功为止——记录下结果以便以后再次使用。如果你到 `hdg` 仍然不起作用，那么说明还有其他问题。如果你不在 GUI 环境中，请在弹出 CD 之前输入 `umount /media/cdrom`。 |

## vi 编辑器

| 键位 | 初始光标位置 | 结果 |
|---|---|---|
| `A` | 在你想添加文本的地方前留一个空格 | vi 在光标位置后直接进入插入模式。 |
| `dd` | 在你想剪切的（第一）行任意位置 | vi 剪切整行。 |
| `d` | 直接位于你想删除的（第一）字符上方 | vi 删除指定的字符。 |
| `dd` | 在你想删除的（第一）行任意位置 | vi 删除整行。 |
| `P` | 直接位于你想让文本出现的地方 | vi 将缓冲区中的文本复制到文档。 |
| `u` | 在文件任意位置 | vi 撤销你上一次的操作。 |
| `x` | 直接位于你想剪切的（第一）字符上方 | vi 删除指定的字符。 |
| `yy` | 在行任意位置 | vi 复制该行（几行）。 |

> *(注：上述 vi 表格中的某些 OCR 痕迹已修正为标准的 vi 命令：`d`、`dd`、`x`、`yy`。)*

# 作者致谢

Dee-Ann 像往常一样，有许多想要感谢的人。首先，感谢 John "maddog" Hall 让她有机会接手这本书的演进。他当时正忙于领导 Compaq 的 UNIX 软件组、担任 Linux International 的执行董事，并担任 Cair Linux/GNU 认证第五版的顾问委员会成员，分身乏术。

其次，感谢 LANrights 的同事们在之前的两个版本中所付出的所有努力。第三，感谢 Melanie Hoag 和 Evan Blomquist，他们在最近的两个版本中也付出了巨大的努力。最后，当然要感谢 Wiley Publishing, Inc. 的编辑和员工。没有他们的指导，这本书将无法存在，更无法随着时间的推移而不断完善。

最重要的是，我想感谢那些向我提出问题、建议和疑虑的读者。对于任何迷失在海量电子邮件中而没有得到答复的人，我深表歉意；但请相信，至少当我三个月后从那堆邮件中找出你的邮件时，我已经将其归类为下一版本中需要考虑的事项之一。正是读者的参与让这样的书籍多年来不断改进，我的目标是继续完善《Linux 傻瓜指南》（Linux For Dummies），使其成为最好的桌面 Linux 教程。

> — Dee-Ann LeBlanc

# 出版致谢

我们对这本书感到自豪；请通过位于 `www.dummies.com/register/` 的在线注册表向我们提交您的意见。

帮助这本书上市的人员包括：

## 策划、编辑与媒体开发

- **项目编辑**：Christopher Morris（上一版本：Kala Schrager）
- **策划编辑**：Theresa Varveris
- **校对编辑**：Rebecca Whitney
- **技术编辑**：Dave Taylor
- **编辑经理**：Kevin Kirschner
- **权限编辑**：Laura Moss
- **媒体开发专家**：Travis Silvers
- **媒体开发经理**：Laura VanWinkle
- **媒体开发主管**：Richard Graves
- **编辑助理**：Amanda Foxworth
- **漫画**：Rich Tennant (`www.the5thwave.com`)

## 制作

- **项目协调员**：Courtney Macintyre
- **排版与图形**：Michael Kruzil, Lynsey Osborn, Heather Ryan, Jacque Schneider, Shae Lynn Wilson
- **校对员**：Laura Albert, Andy Hollandbeck, Carl Pierce, TECHBOOKS Production Services
- **索引员**：TECHBOOKS Production Services
- **特别协助**：Andrea Dahl

## 《技术傻瓜》系列出版与编辑

- **Richard Swadley**，副总裁兼执行集团出版经理
- **Andy Cummings**，副总裁兼出版经理
- **Mary C. Corder**，编辑总监

## 《消费者傻瓜》系列出版

- **Diane Graves Steele**，副总裁兼出版经理
- **Joyce Pepple**，策划总监

## 制作服务

- **Gerry Fahey**，制作服务副总裁
- **Debbie Stailey**，制作服务总监

## 目录摘录

- 第 18 章：安全的 Linux 环境 ................................................ 313
- GNU 是什么？ ................................................................................ 13
- 到底是谁在管理 Linux？ ................................................. 15
- 爱因斯坦也是个志愿者 ........................................................................ 15
- Linux 打包：发行版 ................................... 16
- 在 Windows 2000 和 Windows XP 中查看磁盘空间 ................................................................................ 21
- 在 Windows 98 中检查磁盘空间 ................................ 23
- 处理磁盘分区 ............................................................ 26
- 选择分区工具 ............................................................ 26
- 从零开始双系统分区 ................................... 27
- 使用 FIPS 安全地调整分区 ........................................ 27
- 运行 Windows 和 Linux ................................... 30
- 评估你的电脑 ............................................................ 31
- 最后，为你的安装做准备 ................... 34
- 启用从 CD- 或 DVD-ROM 启动 ................................ 36
- 准备从软盘安装盘启动 ................ 37
- 发行版版图 ................................................................................................ 64
