
18. 以 root 身份注销，输入

    exit

19. 关闭终端窗口。

## 目标 5—操作文件和目录

在本目标中，您将学习如何执行以下操作来处理文件：

- 复制、移动和重命名文件和目录
- 创建目录
- 删除文件和目录
- 链接文件

### 复制、移动和重命名文件和目录

要复制和移动文件和目录，您需要了解以下操作：

- 使用 mv 移动和重命名文件
- 使用 cp 复制文件

#### 使用 mv 移动和重命名文件

您可以使用 mv（move）命令将一个或多个文件移动到另一个目录，如下所示：

```bash
mv *.txt /tmp
```

您也可以使用 mv 命令重命名文件，如下所示：

```bash
mv recipe new_recipe
```

表 7-15 显示了可与 mv 一起使用的选项。

![](img/9129877170834ca9d5fdac5319bf5f12_228_0.png)

| Option | Description |
|---|---|
| `-i` | 在移动或重命名文件前询问确认。这可防止具有相同名称的现有文件被覆盖。 |
| `-u` | 仅移动比同名目标文件更新的文件。 |

**表 7-15**

#### 使用 cp 复制文件

您可以使用 cp（copy）命令复制文件和目录。使用 cp 的语法为：

```bash
cp source destination
```

使用 cp 命令时，需要记住以下几点：

- cp 命令会在未确认的情况下覆盖现有文件。
- 您可以通过使用选项 `-i` 来避免自动覆盖。此选项要求在覆盖前进行确认。
- 如果您只想复制目录的内容（而不复制目录本身），则目标目录必须已存在。例如，使用不同名称对目录进行备份复制。

例如，要将 /tmp/quarterly-1/ 目录及其所有子目录复制到 /tmp/expenses/ 目录（该目录已存在），请输入以下内容：

```bash
cp -R /tmp/quarterly-1/ /tmp/expenses
```

结果是 /tmp/expenses/quarterly-1/ 目录。

要将 proposals/ 目录的内容（其中包含的所有文件，包括隐藏文件和子目录）复制到 proposals_old/ 目录（该目录必须已存在），请输入以下内容：

```bash
geeko@da10:~ > ls -a proposals
. .. hidden quarterly-1 quarterly-2 quarterly-3
quarterly-4
geeko@da10:~ > cp -r proposals/. proposals_old
geeko@da10:~ > ls -a proposals_old
. .. hidden quarterly-1 quarterly-2 quarterly-3
quarterly-4
```

要避免复制隐藏文件，请输入以下内容：

```bash
geeko@da10:~ > cp -r proposals/* proposals_old
geeko@da10:~ > ls -a proposals_old
. .. quarterly-1 quarterly-2 quarterly-3 quarterly-4
```

表 7-16 显示了可与 cp 一起使用的选项。

| Option | Description |
|---|---|
| `-a, --archive` | 复制目录和子目录（与 -R 比较）；符号链接、文件权限、所有者和时间戳不会更改。 |
| `--help` | 显示 cp 的选项。 |
| `-i, --interactive` | 覆盖前询问。 |
| `-R, -r, --recursive` | 递归复制目录（目录及其任何子目录）。 |
| `-s, --symbolic-link` | 创建符号链接而不是复制。 |
| `-l, --link` | 链接文件而不是复制它们。 |
| `-u, --update` | 仅当源文件比目标文件更新或目标文件不存在时才复制文件。 |

表 7-16

## 创建目录

您可以使用 *mkdir*（*创建目录*）命令创建新目录（例如 mkdir proposal）。选项 `-p` 可让您创建完整路径，如下所示：

```bash
mkdir -p proposal/january
```

## 删除文件和目录

在本节中，您将学习如何执行以下操作：

- 使用 `rmdir` 删除空目录
- 使用 `rm` 删除文件和目录

### 使用 rmdir 删除空目录

您可以使用 `rmdir`（*删除目录*）命令删除指定的目录或目录（例如 rmdir proposal）。在删除之前，目录必须为空。

### 使用 rm 删除文件和目录

您可以使用 `rm`（*删除*）命令在未被要求确认的情况下删除文件，如下所示：

```bash
rm part*
```

此示例删除当前目录中以 **part** 开头的所有文件。如果用户没有足够的权限删除文件，则文件保持不变并显示错误消息。

![](img/9129877170834ca9d5fdac5319bf5f12_230_0.png)

> 使用 `rm` 命令删除的文件无法恢复。

表 7-17 显示了可与 `rm` 一起使用的选项。

| Option | Description |
|---|---|
| `-i` | 删除前询问确认。 |
| `-r` | *（递归）* 允许删除整个目录。 |
| `-f` | *（强制）* 默认情况下，如果应删除的文件为只读，`rm` 会要求确认。使用此选项可在未被要求确认的情况下删除文件。 |

表 7-17

![](img/9129877170834ca9d5fdac5319bf5f12_231_0.png)

## 练习 7-4：复制、移动和删除文件，创建和删除目录

在本练习中，使用 `cp` 和 `mv` 命令复制和移动文件，使用 `mkdir` 命令创建新目录，并使用 `rm` 和 `rmdir` 命令删除文件和目录。

### 完成此练习的详细步骤

- 第 I 部分：复制和移动文件和目录
- 第 II 部分：创建新目录
- 第 III 部分：删除文件和目录

### 第 I 部分：复制和移动文件和目录

要复制和移动文件和目录，请执行以下操作：

1. 打开一个终端窗口。
2. 通过输入以下内容将 `new_file`（在练习 *创建和查看文件* 中创建）重命名为 `my_file`：
   ```bash
   mv new_file my_file
   ```
3. 通过输入以下内容验证文件是否已重命名：
   ```bash
   ls -l
   ```
4. 通过输入以下内容复制 `my_file`：
   ```bash
   cp my_file my_file1
   ```
5. 通过输入以下内容验证 `my_file1` 是否已创建：
   ```bash
   ls -l my*
   ```
6. 通过输入以下内容将 `/usr/bin/rename` 和 `/usr/bin/tac` 文件复制到 `/tmp` 目录：
   ```bash
   cp /usr/bin/rename /usr/bin/tac /tmp
   ```
7. 通过输入以下内容验证文件是否已复制：
   ```bash
   ls -l /tmp
   ```
8. 通过输入以下内容将文件 `/tmp/tac` 移动到主目录：
   ```bash
   mv /tmp/tac ~
   ```
9. 通过输入以下内容验证移动：
   ```bash
   ls -l
   ```
10. 通过输入以下内容将 `/tmp/rename` 文件重命名为 `~/my_file2` 并移动它：
    ```bash
    mv /tmp/rename ~/my_file2
    ```
11. 通过输入以下内容验证文件 `my_file2` 是否存在：
    ```bash
    ls -l
    ```
12. 通过输入以下内容将完整的 /bin 目录复制到主目录，新目录名为 my_dir
    ```bash
    cp -r /bin ~/my_dir
    ```
13. 通过输入以下内容验证文件是否已复制
    ```bash
    ls -l ~/my_dir
    ```

### 第 II 部分：创建新目录

要创建新目录，请执行以下操作：

1. 通过输入以下内容在 my_dir 目录内创建名为 new_dir 的目录
    ```bash
    mkdir ~/my_dir/new_dir
    ```
2. 通过输入以下内容验证目录是否已创建
    ```bash
    ls ~/my_dir
    ```
3. 通过输入以下内容创建 gecko_dir/empty_dir 目录
    ```bash
    mkdir -p ~/gecko_dir/empty_dir
    ```
4. 通过输入以下内容验证 gecko_dir 是否已创建
    ```bash
    ls
    ```
5. 通过输入以下内容验证 empty_dir 是否已创建
    ```bash
    ls gecko_dir
    ```
6. 关闭终端窗口。

### 第 III 部分：删除文件和目录

要删除文件和目录，请执行以下操作：

1. 打开一个终端窗口。
2. 通过输入以下内容尝试删除 ~/gecko_dir 目录
    ```bash
    rmdir gecko_dir
    ```
    显示一条消息，指出目录无法删除，因为目录不为空。
3. 通过输入以下内容删除 ~/gecko_dir/empty_dir 目录
    ```bash
    rmdir gecko_dir/empty_dir
    ```
4. 通过输入以下内容验证 /empty_dir 目录是否已被删除
    ```bash
    ls gecko_dir
    ```
5. 通过输入以下内容删除 ~/gecko_dir 目录
    ```bash
    rmdir gecko_dir
    ```
