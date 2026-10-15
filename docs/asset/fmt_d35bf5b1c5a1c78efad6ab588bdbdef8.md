
# 62 • 第 16 章 • 交互式 Shell

```text
-rw-xr-r--  1 gilberg staff      42 Jul 10 2000 ErrFile
-rw-xr-r--  1 gilberg staff     111 Jul 11 2000 IFS.scr
-rw-xr-r--  1 gilberg staff       0 Jun 11 2000 MidRaven
-rw-xr-r--  1 gilberg staff      36 Jul 31 13:42 who.scr.bak
-rw-xr-r--  1 gilberg staff      36 Jul 31 13:45 who.scrBak
-rw-xr-r--  1 gilberg staff     112 Jul  5 2000 xxforLoop.scr
% cat temp.file
-rw-xr-r--  1 gilberg staff     111 Jul 11 2000 IFS.scr
-rw-xr-r--  1 gilberg staff      925 Jul 10 2000 addCol.scr
-rw-xr-r--  1 gilberg staff     129 Jul  7 2000 backup.scr
-rw-xr-r--  1 gilberg staff     225 Jun 18 2000 variableNum.scr
-rw-xr-r--  1 gilberg staff     171 Jul 29 14:12 whileRead.scr
```

## 16.3 变量

变量是内存中一个可以存储值的位置。shell 允许你在变量中存储值。图 16.3 显示了变量的分类：用户定义的和预定义的。

### 用户定义变量

用户定义变量由用户创建。图 16.3 显示了如何操作。

### 预定义变量

预定义变量分为内部变量或环境变量。图 16.3 显示了一些示例。

## 16.7 访问变量的值

要访问变量的值，必须在变量名前加上美元符号 `$`。会话 16.7 显示了如何操作。

## 16.8 在字符串中使用值

变量的值可以使用于字符串的任何位置。例如，你可以在字符串的开头、中间或末尾使用该值。会话 16.8 展示了这三种情况。

## 16.9 将路径存储在变量中

假设你经常需要访问特定目录。为了防止输入长目录路径时出错并节省时间，你可以简单将路径存储在变量中（会话 16.10）。

## 16.1 空变量

如果我们访问一个未设置的变量（即其中没有存储值），我们将得到一个所谓的空值（null）。我们也可以通过给变量赋值空字符串（`""`）或不赋值任何内容来显式地为变量设置空值。

## 会话 16 空变量——续上

```shell
% set z = "" #另一个空赋值
% echo "(x: $x) (y: $y) (z: $z)"
(x: 1) (y: ) (z:)
% set x = "" #通过赋值为空值来清除 'x'
% echo "(x contains: $x)"
(x contains:)
% set x = 1
% echo "(x contains: $x)"
(x contains: 1)
```

## 取消变量

在会话 16.11 中，我们演示了可以通过给变量赋值空值来清除变量。虽然这种方法有效，但最好使用 `unset` 命令（会话 16.12）。

## 会话 16.12 取消变量

使用 `unset` 和空赋值之间存在细微的差异。两者都会将变量设置为空值。然而，`unset` 还会将变量名从活动变量列表中移除。如果你在取消变量设置后尝试 `echo` 它，将得到错误信息“Undefined variable”（未定义的变量）。

## 存储文件名

我们可以在变量中存储文件名。可以使用通配符。然而，我们应该注意 Shell 是如何处理通配符的。Shell 将包含通配符的文件名存储在变量中，而不对其进行扩展。当该值被使用时，扩展才会发生。会话 16.13 演示了脚本如何处理存储的文件名通配符。

## 会话 16.13 存储文件名

| `%ls` | | |
| :--- | :--- | :--- |
| `file1` | `file2` | `file3.bak` |
| `set filename = "file*"` | `#显示内容` | |
| `echo filename contains: $filename` | | |
| `filename contains:` | | |
| `echo $filename` | | |
| `file1` | `file2` | `file3.bak` |
| `set filename = "file?"` | | |
| `echo $filename` | | |
| `file1` | `file2` | |

### 会话 16.13 分析

在第一个示例中，我们创建了一个变量并将星号值存储在其中。然后我们打印变量值，以证明它包含了通配符命令。（注意变量名包含在引号字符串中，因此它不会被扩展）。当我们使用 `echo` 命令使用该变量时，Shell 会扩展通配符并打印出三个匹配的文件。在第二个示例中，我们使用了问号通配符。在这种情况下，列出了前两个文件，因为它们的名称只有五个字符。第三个文件超过了五个字符，因此不匹配通配符模式。

## 存储文件内容

我们还可以将文件内容存储在变量中进行处理，例如解析单词。存储文件需要两个步骤：

- 1. 使用 `cat` 工具在标准输出上创建文件的副本。
- 2. 使用命令替换（反引号），将标准输出内容转换为字符串。

现在，该字符串可以存储在变量中。整个过程在会话 16.14 中通过一条命令完成。

## 会话 16.14 将文件存储在字符串中

| `cat storeAsVar.txt file` | 说明 |
| :--- | :--- |
| 这是一个 | |
| 用于显示将文件存储在变量中的结果 | |
| ``set x = `storeAsVar.txt` `` | |
| `echo $x` | 这是一个用于显示将文件存储在变量中的结果。 |

会话 16.14 分析：我们首先使用 `cat` 显示了一个三行文件。为了演示文件存储在变量中的完整效果，我们在文件中使用了额外的空格。然后，为了证明文件已存储在变量中，我们使用 `echo` 将其写入监视器。在这三条命令中，我们首先显示了文件的内容，接着将其转换为字符串，然后使用 `echo` 命令将其转换回文件（监视器实际上是一个文件）。这演示了 `echo` 和命令替换是互反的——一个将文件转换为字符串，另一个将字符串转换为文件。我们还仔细地 `echo` 了输出。注意变量不包含文件中任何额外的空格。它包含由单个空格分隔的文件。所有的额外空格都被移除了。

## 在变量中存储命令

我们还可以在变量中存储命令。例如，`ls` 命令可以存储在变量中。我们在会话 16.15 中演示这一点。

## 16.15 执行命令

```shell
% set x = "ls"
% $x
file3.bak fileOut.rpt
file.scr file2.bak file4Report
file1 file6List.dat
```

在变量中存储命令仅适用于简单命令。如果命令是复杂的（例如，管道 `list` 命令的结果），变量将无效。对于复杂命令，我们需要 `eval` 命令，我们将在后书中讨论。

## 导出变量

我们在第 5 章中提到，Shell 可以创建另一个 Shell。新的 Shell称为子 Shell 或子 Shell。创建另一个 Shell 的过程称为派生（forking）。图 16.8 演示了派生过程。通过进入 `csh` 执行一个新的 Shell。此命令创建一个子 Shell 并等待命令。要离开子 Shell，执行 `exit`，这会删除子 Shell 并返回父 Shell。

```shell
% date
Thu Dec 20 19:48 PST 2000
% csh
```

（`img/6ecdc42ec4060ea72b32fdafff220_705.png`）

现在需要理解的是变量不会自动导出到 Shell。这在会话 16.16 中进行了演示。

## 16.16 变量未导出

```shell
% set name = George
% echo $name
George
% csh
% echo $name # 在子 Shell
Undefined variable
```

如果我们想让变量在子 Shell 中可用，必须告诉当前 Shell 我们要导出它。导出变量与非导出变量分开维护。导出变量使用 `setenv` 命令创建；非导出变量使用 `set` 命令创建。`setenv` 命令的格式如下。注意一次只能声明一个导出变量。

```text
setenv value
```
