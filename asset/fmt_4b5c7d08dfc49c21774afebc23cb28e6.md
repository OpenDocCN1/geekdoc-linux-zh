
图 2.17: 过滤关键消息

此命令仅显示分类为关键（critical）的日志，为需要立即关注的严重系统问题提供见解。这种方法帮助我们快速识别并解决关键问题，确保系统顺利运行，而不被不重要的日志所淹没。

写入或执行内容，确保只有经过授权的用户才能执行特定操作。

## 理解文件权限

在 Rocky Linux 9 中，文件权限控制对文件和目录的访问。我们可以使用 `ls -l` 命令检查权限，该命令会显示：

- 文件类型（例如：目录、文件、符号链接）
- 用户（所有者）、组和其他用户的权限位
- 文件所有者和所属组
- 最后修改时间

## 文件类型指示

当使用 `ls -1` 时，第一个字符表示文件类型：

- `d`: 目录
- `-`: 普通文件
- `l`: 符号链接

## 权限结构

权限由三组三个字符组成表示：

- 用户（所有者）：第一组（例如，`rwx`）
- 组：第二组（例如，`r-x`）
- 其他：第三组（例如，`r-x`）

## 每个字符代表：

- `r`: 读取权限
- `w`: 写入权限
- `x`: 执行权限
- `-`: 未授予权限

## 示例：`drwxr-xr-x`

- `d`: 目录
- `rwx`: 所有者可以读取、写入、执行
- `r-x`: 组可以读取和执行
- `r-x`: 其他用户可以读取和执行

## 使用 chmod 修改权限

我们可以通过两种方式使用 `chmod` 命令修改权限：

### 使用数字表示

每个权限都有一个数值：

- `7`: 读取、写入、执行 (`rwx`)
- `6`: 读取、写入 (`rw-`)
- `5`: 读取、执行 (`r-x`)
- `4`: 仅读取 (`r--`)
- `3`: 写入、执行 (`-wx`)
- `2`: 仅写入 (`-w`)
- `1`: 仅执行 (`--x`)
- `0`: 无权限 (`---`)

![](img/b8b015d9ebe4ee947c12a4edae6c2170_108_0.png)

此图提供了 Linux 环境文件和目录权限显示方式的可视化表示。该图说明了 `ls -l` 命令的输出，显示了文件类型指示以及用户、组和其他对应的读、写、执行权限。通过视觉示例，管理员可以更好地理解权限结构的工作原理以及它如何反映在实际的文件和目录中。这种可视化拆解有助于快速识别哪些用户或组具有特定文件的访问权限以及他们拥有的访问级别，便于管理和排除 Linux 系统中的文件权限。

## 理解 Linux 文件权限：符号与数字

在 Linux 中，文件权限定义了谁可以读取、写入或执行文件或目录。这些权限分为三类用户：

- 所有者（用户）
- 组
- 其他用户

每种类别可以分配三种权限：

- 读取 (`r`) = 4
- 写入 (`w`) = 2
- 执行 (`x`) = 1

这些权限以两种格式表示：

- 符号（例如，`rwxr-xr--`）
- 数字（例如，`754`）

例如，`chmod 754 filename` 设置：

- 所有者：`rwx` (7 = 4+2+1)：完全访问
- 组：`r-x` (5 = 4+1)：读取和执行
- 其他用户：`r--` (4)：仅读取

可以使用以下命令更改所有权：

- `chown alice file.txt`：将所有者设置为 alice
- `chgrp developers file.txt`：将组设置为 developers
- `chown alice:developers file.txt`：一步到位更改所有者

通过理解这些格式，用户可以更有效地管理文件访问，并维护安全的 Linux 环境。

## 符号与数字映射

下表概述了 Linux 中的四种基本权限类型，展示了它们的符号表示、数值、功能含义、适用用户类以及代表性示例。权限通过符号字符 (`r`, `w`, `x`, `-`) 和数值 (`4`, `2`, `1`, `0`) 的组合定义，共同决定所有者、组和其他用户的访问级别。例如，权限字符串 `-rw-r-r--` 表示所有者具有读取和写入权限，而组和其他用户仅限于只读访问。这种结构化模型对 Unix 操作系统中的文件和目录访问性提供了细粒度的控制。

| 类型 | 符号 | 数值 | 含义 | 适用对象 | 示例 |
| --- | --- | --- | --- | --- | --- |
| 读取 | r | 4 | 可以查看文件内容或列出目录 | 组、其他 | -rw-r-r-- -- 所有者读/写，组和其他用户可读 |
| 写入 | w | 2 | 可以修改文件或在目录中添加/删除文件 | 其他 | -rwwxr-xr-- -- 所有者读/写/执行 |
| 执行 | x | 1 | 可以运行文件或访问目录 | 其他 | -rwx -- 所有者具有完全访问 |
| 无权限 | 0 | 无访问 | | -- 没有任何权限 |

表 2.3：理解 Linux 文件权限 (`chmod`, `chown`, `chgrp`)

## 数字权限

下表提供了 Linux 数字权限的详细拆解，按用户类进行分类。每种类别——所有者 (`u`)、组 (`g`) 和其他 (`o`)——都关联一个符号简写和相应的数值。这些数值决定了授予的访问级别：7 (`rwx`) 代表完全访问，5 (`r-x`) 代表读取-执行，4 (`r--`) 代表仅读取。

| 用户类 | 符号 | 数值 | 代表什么 |
| --- | --- | --- | --- |
| 所有者 | u | 7 | 完全访问 |
| 组 | g | 5 | 读取和执行 |
| 其他 | o | 4 | 仅读取 |

表 2.4：数字权限拆解

- **权限：** `r`(读), `w` (写), `x` (执行)

```bash
chmod a+x filename
```

```
[cesarserver@RockyLinux permissions]$ chmod a+x filename
[cesarserver@RockyLinux permissions]$ ls -l filename
-r-xr-x-x-. 1 cesarserver cesarserver 0 Nov 19 15:50 filename
```

> 图 2.22: 为所有人添加执行权限

此命令为用户、组和其他人添加执行权限。

## 示例 2：移除组和和其他的写入权限

```bash
chmod go-w filename
```

```
[cesarserver@RockyLinux permissions]$ chmod go-w filename
[cesarserver@RockyLinux permissions]$ ls -l filename
-r-xr-x-x-. 1 cesarserver cesarserver 0 Nov 19 15:50 filename
```

> 图 2.23: 移除组和和其他的写入权限

此命令移除组和和其他的写入权限。

## 示例 3：设置执行权限

```bash
chmod u=rwx,gx=rx,o=r filename
```

```
[cesarserver@RockyLinux permissions]$ chmod u=rwx,gx=rx,o=r filename
[cesarserver@RockyLinux permissions]$ ls -l filename
-rwxr-xr-x-. 1 cesarserver cesarserver 0 Nov 19 15:50 filename
```

> 图 2.24: 设置执行权限

此命令为用户设置读、写、执行权限；为组设置读和执行权限；为其他人设置只读权限。

`chmod +x script_name`: 此命令允许我们执行该脚本。

## 为移除所有人的写入权限

`touch somefile.txt`: 我们正在创建一个新文件。

`chmod o-w somefile.txt`: 移除所有人的写入权限。

```bash
[cesarserver@RockyLinux ~]$ touch somefile.txt
[cesarserver@RockyLinux ~]$ chmod o-w somefile.txt
```

> 图 2.25: 移除所有人的写入权限

此命令确保其他人无法修改该文件。

## 为所有人设置只读权限

`touch readonlyfile.txt`: 我们正在创建一个新文件。

`chmod 444 readonlyfile.txt`: 我们正在添加只读权限

`ls -l`: 我们正在验证刚才设置的权限。

```
[cesarserver@RockyLinux ~]$ touch readonlyfile.txt
[cesarserver@RockyLinux ~]$ chmod 444 readonlyfile.txt
[cesarserver@RockyLinux ~]$ ls -l readonlyfile.txt
-r--r--r-- - 1 cesarserver cesarserver 0 Nov 19 17:38 readonlyfile.txt
```
