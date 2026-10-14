
## 命令 `man`

### 语法：

```
man command
man -k expression
```

显示所提供命令的手册页（“man pages”）。`man -k` 搜索在 NAME 部分包含该表达式的手册页。一个 man 手册页通常包含以下部分：

- NAME 命令及用途
- SYNOPSIS 命令的语法
- DESCRIPTION 命令效果的描述
- FILES 被修改和/或需要的文件
- OPTIONS 选项（如果存在）
- EXAMPLE(S) 应用示例（很少见）
- BUGS 已知的错误（如果已知）
- SEE ALSO 相同上下文中的其他命令

### 练习：

*显示关于命令 xterm 的信息！*

## 命令 `passwd`

### 语法：

```
passwd
```

设置一个新密码。

密码应由字母、数字和特殊字符的组合构成，并且不应出现在任何字典或类似列表中。否则，密码可能会被系统化的搜索算法破解。

设置/更改密码的命令以及所需的约定（长度、数字/字母/特殊字符的数量）可能因系统而异。下面的示例是一个常见的示例，例如适用于 CIP Pool 的工作站（但不适用于 USM 的工作站）。

### 示例：

```
wegner@arber:~ > passwd
Changing password for wegner
Old password: myoldpasswd
Enter the new password
(minimum of 5, maximum of 8 characters)
Please use a combination
of upper and lower case letters and numbers.
New password: mynewpasswd
Re-enter new password: mynewpasswd
Password changed.
```

## 3 文件系统

### 逻辑、文件类型

> “在 UNIX 中，一切都是文件。”

可以找到以下*文件系统对象*：

- “普通”（文本）文件
- 可执行文件（二进制文件或 *shell 脚本*）
- 目录
- 设备文件
- *管道*
- 符号链接或硬*链接*（对文件的引用）

所有文件和文件系统对象都按层级结构组织在一个*文件树*中，且只有一个*根目录* ‘/’。

与 MS-Windows 文件系统不同，UNIX 文件系统不区分不同的驱动器。所有物理设备（硬盘、DVD、CDROM、USB、软盘）都通过文件树中某个目录（通常位于 /dev 内）下的特定文件来表示。

文件名由字母、数字和某些特殊字符的序列组成，并且不能包含*斜杠*（为了方便起见，也不应包含空格）。

避免使用可能被 *shell* 以特殊方式解释的字符。

在文件树中，可以通过*绝对路径名*或*相对路径名*来引用文件。绝对路径名由到达该文件所需的所有目录和文件名组成，并且始终以 /（根目录）开头。

在许多 shell 和应用程序中，波浪号（~）表示主目录。

## 命令 `pwd`

### 语法：

```
pwd
```

显示当前目录。

### 示例：

```
wegner@arber:~ > pwd
/home/wegner
wegner@arber:~ >
```

### 练习：

*显示当前目录！*

## 命令 cd

### 语法：

```
cd [directory]
```

切换到指定目录，如果没有提供参数则切换到主目录。

与 MS-DOS/Windows 一样，“..” 表示父目录，“.” 表示当前目录。

### 示例：

```
wegner@arber:~ > cd /home/puls
wegner@arber:/home/puls > pwd
/home/puls
wegner@arber:/home/puls > cd ..
wegner@arber:/home > pwd
/home
wegner@arber:/home > cd
wegner@arber:~ > pwd
/home/wegner
wegner@arber:~ >
```

### 练习：

*切换到目录 /usr/share/templates，然后再回到你的主目录！（-> 使用 TAB 键进行文件名补全）*

*使用 pwd 检查是否切换成功！*

## 文件名的搜索模式

原则上，*shell* 是一个处理输入命令解释的特定程序。如果这些命令的参数是文件名，则可以通过搜索模式同时指定多个文件，该模式由 shell 进行*展开*。无论如何，文件名展开都是在命令执行*之前*完成的。

| 表达式 | 含义 |
|---|---|
| * | “几乎”任意（包括空）字符串 |
| ? | 单个“几乎”任意字符 |
| [...] | 一组字符范围 |
| [!...] | 取反的字符范围 |

“几乎”任意：排除前导点（例如隐藏文件、../ 等）。

## 命令 `ls`

### 语法：

```
ls [-alR] [file/directory]
```

显示文件的名称（以及可选属性），或列出目录的内容。文件和目录名称可以是绝对的，也可以是相对的。

