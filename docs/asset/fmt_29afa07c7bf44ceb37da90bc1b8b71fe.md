
# 权限说明

第一列显示权限。最左侧的字母表示该项是目录还是文件。左侧位置的横杠（`-`）表示它是一个文件；目录由字母 `d` 表示。接下来的九个字母标识了所有者、组和其他用户对文件的访问权限，每 3 个字符为一个段。从左到右，每个段的权限顺序为读取权限、写权限和执行权限。因此，`rwx` 意味着授予了读取、写入和执行权限。如果任何字母显示为 `-`，则不允许相应的权限。例如，`r-x` 表示授予了读取和执行权限，但没有写入权限。

## 所有者、组和其他用户

所有者是拥有文件的用户 ID，由 `ls -l` 输出的第三列指示。在此情况下，它是 "nadmsup"。所有者的权限从第一列中的前三个权限字符（紧随文件或目录指示符之后）中读取。

组由第四列标识。在此情况下，它是 "notes" 组。组的权限由第一列中接下来的三个字符标识。

其他用户（World）是指任何具有该系统登录权限的用户。他们的权限指定在第一列的最后三个字符中。

## 数据库权限建议

由于 `Domino` 服务器是唯一应该更改或直接读取数据库的程序，且数据库不是可执行程序，数据库的权限应为：

```
-rw---- 1 nadmsup notes 1589248 Feb 22 09:34 log.nsf
```

**适用于 `Linux` 的 `Lotus Domino 6`**

如果权限不正确，您可以执行命令：

`chmod 600 filename`

其中 `filename` 是您想要更改权限的文件名。这将为 `Notes` 用户提供读取和写入权限，且不允许任何其他用户查看。由于 `Domino` 服务器在 `Notes` 用户账户下运行，并代表客户端执行所有的读取和写入调用，大多数组织都希望将文件的访问限制在 `Notes` 用户账户。

## 检查大小写敏感性

在 `NT` 中，文件名不区分大小写，但在 `UNIX` 中是区分的。如果您的脚本调用文件 `log.nsf`，而操作系统列出的文件是 `LOG.NSF`，那么在脚本运行时将找不到该文件。`FTP` 完成后，请检查并确保均为小写，除非您的应用程序另有指定。

```
ls -1
-rw---- 1 ndmadsum notes 1589248 Feb 22 09:34 LOG.NSF
mv log.NSF log.nsf
ls -1
-rw---- 1 ndmadsum notes 1589248 Feb 22 09:34 log.nsf
```

> `FTP` 有两种文件传输模式：二进制（`binary`）和 `ASCII`。二进制传输是精确复制，`FTP` 不会对文件进行任何格式转换。`ASCII` 传输假设您正在传输的文件是文本文件，并在不同平台之间传输时，将尝试将文件格式化为目标机的原生文本格式。如果您在传输数据库时处于 `ASCII` 模式，`Domino` 将无法在目标机访问该数据库。某些版本的 `FTP` 以 `ASCII` 模式启动。因此，在传输任何数据库或模板之前，您应该始终在 `FTP` 命令行中输入 `bin` 以确保您处于二进制模式。

## 补充材料

本红书提到了下文所述可以从互联网下载的补充材料。

### 定位 Web 材料

与本红书相关的 `Web` 材料可以通过 `IBM Redbooks Web` 服务器以软拷贝形式在网上获取。将您的 `Web` 浏览器指向：

```
ftp://www.redbooks.ibm.com/redbooks/SG2468335
```

或者，您可以访问 `IBM Redbooks` 网站：

```
ibm.com/redbooks
```

选择 "Additional materials" 并打开与红书表单号 `SG246835` 对应的目录。

### 使用 Web 材料

随本红书的附加 `Web` 材料包含以下文件：

| 文件名 | 描述 |
|---|---|
| `domino` | 适用于 `Linux` 的 `Domino 6` 启动脚本，用于系统启动期间 |
| `startserver` | 适用于 `Linux` 的 `Domino 6` 启动脚本，用于重启 `Domino` 服务器 |
| `db2empt.zip` | 压缩的 `DB2` 数据库模板 |
| `DB2emp.zip` | 压缩的 `DB2` 数据库，包含 `MySQL` 员工数据文档 |
| `DB2empNODATA.zip` | 压缩的 `DB2` 数据库，空数据库，无数据 |
| `MySQL.zip` | 压缩的数据库，包含 `MySQL` 示例员工数据文档 |
| `MySQLNTF.zip` | 压缩的数据库模板 |

### 下载 Web 材料的系统要求

建议的系统配置如下：

- 硬盘空间：文件至少 `10 MB`
- 操作系统：`Red Hat 7.2` 或 `SuSE 8.0`

### 如何使用 Web 材料

在您的工作站上创建一个子目录（文件夹），并解压 `Web` 内容。

关于如何使用 `Domino` 的详细说明，请参考第 130 页的 "Starting Domino from a script"。

## 相关书籍

本节列出的出版物非常适合深入本文红书涵盖的主题。有关订购这些出版物的信息，请参阅第 448 页的 "How to get Redbooks"。

## 其他资源

这些出版物也可作为相关来源：

- `LINUX in a Nutshell`, Hekman, `O’Reilly, Inc.`, ISBN `0596002512`
- `Essential System Administration, 2nd Edition`, Frish, `O’Reilly, Inc.`, ISBN `0596000343`
- `Running Linux, 3rd Edition`, Welsh al, `O'Reilly, Inc.`, ISBN `1565924002`
- `Linux Administration Handbook`, Nemeth al, `Prentice Hall`, ISBN `0130084662`

## 参考网站

这些网站也是相关进一步信息的来源：

- `IBM Linux`: `http://www.ibm.com/linux`
- `Red Hat`: `http://www.redhat.com`
- `SuSE`: `http://www.suse.com`
- `UnitedLinux`: `http://www.unitedlinux.com`
- `Linux Documentation Project`: `http://www.tldp.org`
- `O'Reilly & Associates, Inc.`: `http://www.oreilly.com`
- `Guardian Digital, inc.`: `http://www.linuxsecurity.com`
- `CodeWeavers`: `http://www.codeweavers.com`
- `Wine`: `http://www.winehq.org`

## 如何获取 IBM Redbooks

您可以通过以下网站订购纸质版 `Redbooks`，并在那里查看、下载或搜索 `Redbooks`：

`ibm.com/redbooks`

你也可以从该网站下载额外的材料（代码示例或磁盘/`CD-ROM` 镜像）。

# IBM Redbooks 集合

`Redbooks` 也通过 `CD-ROM` 提供。点击 `Redbooks` 网站上的 `CD-ROM` 按钮可获取有关所有提供的 `CD-ROM` 以及更新和格式的信息。

# 索引

# 符号

`.bashrc` 环境文件 305

# A

+   - 访问控制 373
- 访问外部数据 288
- 激活 266
- `Active Directory` 266
- 容器 276, 285
- 用户容器 285
- `Active Directory` 同步
- 添加新的 `Linux` 用户 32
- 从 `Windows 2000` 管理用户和组组
- 远程管理 `Domino` 服务器 192
- 管理 133, 262
- 策略 267
- 员客户端
- 参见 `Domino` 管理客户端
- `AdminP` 178
- `AD` 266
- 访问控制列表 276
- `Active Directory` 容器 270
- 管理 ID 274
- 管理员密码 271
- 容器映射 276
- 创建 `Domino` 用户 270
- 创建新组 266
- 创建新用户 266
- 创建用户 278–281
- 在 `AD` 中创建用户和组 270
- 自定义同步选项 273
- `Domino` 信息 281
- 启用 `Lotus Domino Options` 270
- 启用同步选项 273
- 现有 `AD` 用户 278
- 扩展访问控制列表 276
- 字段映射标签 275
- 组类型映射 274
- 初始化 `ADSync` 工具 271–272
- 映射字段 275
+   - `Notes` 设置选项卡 274
- `Notes` 同步选项 273
- 从 `Domino` 注册 `AD` 用户 282
- 注册 `Domino` 用户 277
- 注册服务器 274
- 要求 267
- 安全设置 277
- 服务器架构图 268
- 用户删除选项 274
- 用户注册 270
- 分析工具 387
- 杀病毒 391
- 用于 `Domino` 服务器 392
- `Norton` 杀病毒 393
- `OS` 级 392
