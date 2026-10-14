
```
-rw-r--r-- 1 larry system 101 Jun 5 10:03 file1
-rw-r--r-- 1 larry system 171 Jun 5 10:03 file2
-rw-r--r-- 1 larry system 130 Jun 5 10:06 file3
drwxr-xr-x 2 larry system 32 Jun 5 10:07 project
-rw-r--r-- 1 larry system 0 Jun 5 11:03 record1
-rw-r--r-- 1 larry system 0 Jun 5 11:03 record6
drwxr-xr-x 2 larry system 32 Jun 5 10:31 reports
$
```

目录中每个条目的第一个字符串显示该文件或目录的权限。例如，第四个条目 `drwxr-xr-x` 表示以下含义：

- 这是一个目录（`d` 表示法）
- 所有者可以查看、写入和搜索它（`rwx` 序列）
- 组可以查看和搜索它，但不能写入（第一个 `r-x` 序列）
- 其他所有人可以查看和搜索它，但不能写入（第二个 `r-x` 序列）

第三个字段显示文件所有者（本例中为 `larry`），第四个字段显示文件所属的组（本例中为 `system`）。

要列出单个目录的权限，请使用 `ls -ld` 命令：

```
$ ls -ld reports
drwxr-xr-x 2 larry system 32 Jun 5 10:31 reports
$
```

综合起来，文件或目录的所有权限统称为其权限代码。如图 5-1 所示，权限代码由四个部分组成：

- 单个字符显示文件类型。短划线（`-`）表示普通文件，`d` 表示目录，`l` 表示符号链接。任何其他字符表示 I/O（输入/输出）设备。
- 一个 3 字符的权限字段显示用户（所有者）权限，可以是读取、写入和执行权限的任意组合。
- 另一个 3 字符的权限字段显示组权限。
- 另一个 3 字符的权限字段显示其他所有用户的权限。

### 图 5-1：文件和目录权限字段

![](img/47f3b48f0999ddf70574ce85cbaaf942_100_0.png)

当你创建文件或目录时，系统会自动提供一个预定的权限代码。以下是一个典型的文件权限代码：

```
-rw-r--r--
```

此文件权限代码指定所有者具有读和写权限，而组和其他所有人具有读权限。文件类型表示之后某些位置的破折号（`-`）表示指定的用户类别对该操作没有权限。

以下是一个典型的目录权限代码：

```
drwxr-xr-x
```

此目录权限代码指定所有者具有读、写和搜索权限，而组和其他所有人具有读和搜索权限。

系统提供的默认权限代码使你免于每次创建文件或目录时都要显式指定它们。如果你想创建自己的默认权限代码，你必须使用 `umask` 命令更改你的用户掩码。有关 `umask` 命令的解释，请参阅第 5.5 节中对该命令的描述。

## 5.4 设置文件和目录权限（`chmod`）

你更改权限的能力使你能够在很大程度上控制你的数据的使用方式。使用 `chmod`（change mode）命令来设置或更改文件和目录的权限。

例如，你显然允许自己读取、修改和执行一个文件。你通常允许你的组成员读取一个文件。根据你的工作性质和你的组成员构成，你经常让他们修改或执行它。你通常禁止所有其他系统用户访问文件。

> Note
>
> 你必须是文件或目录的所有者（或具有超级用户权限）才能更改其权限。这意味着你的用户名必须在该文件 `ls -l` 列表的第三个字段中。

必须认识到，无论你对文件和目录访问施加了什么限制，超级用户始终可以覆盖它们。例如，如果你使用 `chmod` 命令指定只有你才能访问 `report20` 文件，超级用户仍然可以访问此文件。有关此主题的更多信息，请参阅第 5.7 节。

有两种方法可以指定 `chmod` 命令设置的权限：

- 你可以用字母和操作符号指定权限。
- 你可以用八进制数字指定权限。

以下各节描述了如何使用字母和操作符号以及八进制数字指定权限。

### 5.4.1 使用字母和操作符号指定权限

你可以使用字母和操作符号来更改文件和目录权限。

使用字母和操作符号时 `chmod` 命令的格式如下：

```
chmod userclass-operation-permission filename
```

`userclass-operation-permission` 条目实际上代表三个代码，指定你想要激活的用户类别、组、操作和权限代码。`filename` 条目是你要更改权限的文件或文件的名称。你也可以使用模式匹配字符来指定文件。有关更多信息，请参阅第 5.4.1.3 节。

用户类别、操作和权限定义如下：

- 使用一个或多个这些字母来表示 *userclass*：
  - `u` User（所有者）
  - `g` Group
  - `o` All others（除所有者和组之外）
  - `a` All（用户、组和其他所有人）
- 使用其中一个符号来表示 *operation*：
  - `+` Add permission
  - `-` Remove permission
  - `=` Assign permission regardless of previous setting
- 使用一个或多个这些字母来表示 *permission* 的类型：
  - `r` Read
  - `s` Set user or group ID
  - `w` Write
  - `x` Execute

#### 5.4.1.1 更改文件权限

在以下示例中，首先输入 `ls -l` 命令以显示 `file1` 文件的权限：

```
$ ls -l file1
-rw-r--r-- 1 larry system 101 Jun 5 10:03 file1
$
```

所有者（`larry`）具有读/写权限，而组和其他人只有读权限。

现在，使用标志 `go+w` 输入 `chmod` 命令。此命令通过给予它们对 `file1` 的写访问权限（`+w`）来扩展组（`g`）和其他人（`o`）的权限，除了它们已有的读访问权限之外：

```
$ chmod go+w file1
$
```

接下来，列出文件的新的权限：

```
$ ls -l file1
-rw-rw-rw- 1 larry system 101 Jun 5 10:03 file1
$
```

你已授予你的组和所有其他系统用户对 `file1` 的写权限。

#### 5.4.1.2 更改目录权限

更改目录权限的过程与更改文件权限相同。但是，要列出目录的信息，需要使用 `ls -ld` 命令：

```text
$ ls -ld project
drwxr-xr-x  2 larry  system  32 Jun 5 10:07 project
$
```

现在使用 `chmod g+w` 命令更改权限，使组（`g`）对目录 `project` 具有写权限（`+w`）：

```text
$ chmod g+w project
$ ls -ld project
drwxrwxr-x  2 larry  system  32 Jun 5 10:07 project
$
```

#### 5.4.1.3 使用模式匹配字符

如果要对目录中所有条目的权限进行相同的更改，可以将模式匹配字符（`*`）与 `chmod` 命令一起使用。有关模式匹配字符的信息，请参阅第 2 章。

在以下示例中，命令 `chmod g+x *` 为当前目录中的所有文件（`*`）授予组（`g`）执行（`x`）权限：

```text
$ chmod g+x *
$
```

现在输入 `ls -l` 命令，显示组现在对当前目录中的所有文件都具有执行（`x`）权限：

```text
$ ls -l
total 7
-rw-rwxrw-  1 larry  system  101 Jun 5 10:03 file1
-rw-r-xr--  1 larry  system  171 Jun 5 10:03 file2
-rw-r-xr--  1 larry  system  130 Jun 5 10:06 file3
drwxrwxr-x  2 larry  system   32 Jun 5 10:07 project
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record1
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record6
drwxr-xr-x  2 larry  system   32 Jun 5 10:31 reports
$
```

#### 5.4.1.4 设置绝对权限

绝对权限赋值（`=`）会重置一个或多个文件的所有权限，无论这些权限之前是如何设置的。

在示例 5-1 中，`ls -l` 命令列出了 `file3` 文件的权限。然后，`chmod a=rwx` 命令为所有用户（`a`）赋予所有三种权限（`rwx`）。

**示例 5-1：设置绝对权限**
