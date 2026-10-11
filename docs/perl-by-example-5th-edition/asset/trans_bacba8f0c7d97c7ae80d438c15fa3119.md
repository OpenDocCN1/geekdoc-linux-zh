
虽然 SQL 命令不区分大小写，但按照惯例，为了清晰起见，SQL 关键字通常使用大写，而字段、表和数据库名称仅首字母大写。

```
SELECT * FROM Persons WHERE FirstName='John'
```

在使用 `LIKE` 和 `NOT LIKE` 命令进行模式匹配时，在 MySQL 中，被搜索的模式是区分大小写的。

## 结果集

结果集仅仅是另一个用于保存 SQL 查询结果的表。大多数数据库软件系统甚至允许你使用函数对结果集执行操作，例如“移动到第一条记录”、“获取记录内容”、“移动到下一条记录”等。在图 15.12 所示的示例中，结果集是通过请求 MySQL 显示名为 shippers 的表中所有字段而创建的表。

![](img/8556abcb353c0991f12099420ec28735_559_0.png)

图 15.12 结果集只是由查询产生的一个表。

## 15.3 开始使用 MySQL

MySQL 是一个开源、功能完整的数据库管理系统，已被移植到大多数平台，包括 Linux、Windows、OS/X、HP/UX、AIX 等。MySQL 可移植、快速、可靠、可扩展且易于使用。它是世界上使用最广泛的第二大关系型数据库管理系统，据说已安装在世界各地超过 1000 万台计算机上，包括南极洲。

它有两个版本，一个是购买商业许可证的版本，另一个是免费的（*“免费”* 意味着只要你不复制、修改或分发 MySQL 软件，你就可以在任何应用程序中使用 MySQL）。MySQL 支持多种 API（应用程序编程接口），包括 Perl、PHP、TCL、Python、C/C++、Java 等。

在使用 MySQL 时，会使用一些名称相似但含义不同的术语。表 15.2 旨在帮助澄清这些术语的使用。

4. 对于 100% 符合 GPL 协议的用户，MySQL 是免费使用的。详情请参阅 [http://www.mysql.com/company/legal/licensing/opensource-license.html](http://www.mysql.com/company/legal/licensing/opensource-license.html)。

### 表 15.2 MySQL 中的术语

| 术语 | 定义 |
| --- | --- |
| MySQL | 数据库管理系统的实际软件 |
| mysqld | MySQL 守护进程，即服务器进程 |
| *mysql monitor* | 用于发出 MySQL 命令的监视器（命令行解释器） |
| *mysql* | MySQL 用于管理访问权限的数据库的名称 |
| *mysqladmin* | 用于管理数据库的 MySQL 实用程序 |

### 15.3.1 安装 MySQL

这里假设你已经安装了一个数据库服务器并且它正在运行。下载和安装 MySQL 通常是一个简单的过程。你可以从 *mysql.com* 网站获取 MySQL，或使用集成应用程序，如 XAMPP 或 WAMP。XAMPP（适用于 Windows、Linux、Mac OS 和 Solaris）是一个免费的、易于安装的 Apache 发行版，包含 MySQL、PHP 和 Perl。你只需下载、解压并启动它即可。详情请访问 [http://www.apachefriends.org/en/xampp.html](http://www.apachefriends.org/en/xampp.html)。

完整的安装说明请参见 [http://dev.mysql.com](http://dev.mysql.com)（见图 15.13）。

![](img/8556abcb353c0991f12099420ec28735_560_0.png)

**图 15.13** MySQL 安装文档。

### 15.3.2 连接 MySQL

MySQL 数据库系统使用第 15.2.1 节中描述的客户端/服务器模型，“客户端/服务器数据库”。你是客户端，从命令行、图形用户界面或程序中连接数据库。在从 Perl 程序连接数据库之前，我们首先使用 MySQL 命令行客户端。

MySQL 命令行客户端随 MySQL 安装一起提供，并且普遍可用。它是位于 MySQL 安装目录中 *bin* 文件夹内的一个 *mysql* 程序。要运行这个命令行应用程序，你必须启动命令行提示符。

- 在 Windows 上，转到 *开始* 菜单，选择 *运行...* 选项，然后在运行窗口中键入 *cmd*。
- 在 Mac OS X 上，在你的 *Finder*（访达）中转到 *应用程序* 文件夹，然后导航到 *实用工具*。你会在那里找到 *终端* 应用程序。你应该导航到安装 MySQL 的位置并找到 *bin* 文件夹。
- 在 UNIX 上，在终端窗口的 shell 提示符下输入命令。

MySQL 客户端可执行文件通常位于 *bin* 文件夹中。

要使用此客户端连接数据库，你需要输入类似于以下行的信息：

```
mysql --user=root --password=my_password --host=localhost
```

无论选择哪种类型的客户端，可能需要指定用户名和要连接的主机机器。大多数配置预期你都有一个密码，但如果只是单独工作，则不需要。你还可以选择指定默认数据库。

一旦成功连接，你将看到 *mysql>* 提示符，而不是标准的 DOS/UNIX 提示符（见图 15.14）。这意味着你正在向 MySQL 数据库服务器发送命令，而不是向本地计算机的操作系统发送命令。

![](img/8556abcb353c0991f12099420ec28735_561_0.png)

**图 15.14 MySQL 客户端。**

**MySQL 控制台中的编辑键**。MySQL 支持输入行编辑。上箭头和下箭头键允许你在之前的输入行之间上下移动，左箭头和右箭头键允许你在行内前后移动。退格键（Backspace）和删除键（Delete）用于擦除行中的字符并在光标位置输入新字符。要提交编辑后的行，请按回车键。对于 UNIX 用户，MySQL 还支持制表符补全功能，允许你输入关键字或标识符的一部分，并使用 Tab 键完成补全。

**设置密码**。下载 MySQL 后，在某些安装过程中，可能会要求你为用户 *root* 输入密码。即使没有强制要求创建密码，设置一个密码来保护数据库的安全性也是一个好主意。要设置密码，请转到 MySQL 控制台并输入以下 MySQL 命令。请将 `'MyNewPassword'` 替换为你的密码。

```
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPassword');
```

设置密码后，你可以停止 MySQL 服务器，然后再次以正常模式重新启动它。如果将服务器作为服务运行，请从 Windows 服务窗口启动它。如果是手动启动服务器，请使用你通常使用的命令。你应该能够使用新密码进行连接。

以下示例展示了如何在 *mysql* 提示符下设置密码。

# 示例 15.1

```
1       $ mysql -u root
        ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
        $ 
        $ mysql -u root -p
        Enter password: ********
        Welcome to the MySQL monitor.  Commands end with ; or \g.
        Your MySQL connection id is 91 to server version: 5.0.21-community-nt

        Type 'help;' or '\h' for help.  Type '\c' to clear the current buffer.
```

### 15.3.3 图形用户工具

**MySQL Query Browser**。MySQL Query Browser 是一个图形用户界面 (GUI) 客户端，可从 *mysql.com* 获取，用于连接 MySQL 数据库服务器。下载后，按照简单的安装向导操作，你就可以在 Windows 下通过 *开始* 菜单启动该应用程序。

MySQL Query Browser 随后会显示一个连接对话框（见图 15.15）。你必须指定想要连接的 MySQL 服务器、在该服务器上进行身份验证所需的凭据、该服务器运行的机器（及其监听的端口），以及你将使用的默认数据库（称为 **schema**，即模式）。如果有必要，还可以指定一些其他选项。

你必须选择一个默认数据库才能发出查询。虽然可以在连接到服务器后选择默认数据库，但从连接对话框中设置默认数据库可以节省后续连接的时间。

![](img/8556abcb353c0991f12099420ec28735_563_0.png)

要输入的信息与命令行客户端非常相似：**用户名**、**密码**以及数据库服务器正在运行的服务器主机。你可以选择输入数据库名称和端口号（MySQL 默认为 3306），并在 *Stored Connection*（已存储的连接）部分将连接信息保存为书签。

通过使用应用程序窗口右侧熟悉的树状导航结构，你还可以在 MySQL Query Browser 中导航各个数据库（见图 15.16）。

