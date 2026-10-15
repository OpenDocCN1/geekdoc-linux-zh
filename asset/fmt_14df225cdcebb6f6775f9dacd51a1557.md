
如果设置了权限，则显示该字符，否则显示“-”。

权限字符分组为（“rwx rwx rwx”）：

- `字符 1 到 3`—表示文件所有者的权限。
- `字符 4 到 6`—表示拥有组的权限。
- `字符 7 到 9`—表示所有其他用户的权限——未被前述权限涵盖的用户。

每个文件（和目录）只能属于一个用户和一个组。在前面的示例中，文件所有者的名称（geeko）在 `ls` 输出中显示在文件权限旁边。拥有组的名称（users）显示在文件所有者旁边。

您也可以从 Nautilus 文件管理器查看权限、所有者和组。在 Nautilus 中，右键单击要查看的文件图标，从菜单中选择 `属性`，然后选择 `权限` 选项卡。参见图 9-11。

![](img/9129877170834ca9d5fdac5319bf5f12_305_0.png)

图 9-11

从此对话框中，您可以通过选择适当的选项更改所有者、组和其他用户的读和写权限。

您可以通过从 `文件组` 下拉列表中选择组来将文件或目录的组所有权修改为您所属的其他组。只有 root 可以更改文件的所有者或将拥有组更改为用户所属组之外的组。

### 使用 chmod 更改文件权限

您可以使用 `chmod` 命令添加（“+”）或删除（“−”）权限。文件所有者和 root 都可以使用此命令。

可用于更改权限的选项如下：

- `u`—更改所有者（用户）的权限。
- `g`—更改组的权限。
- `o`—更改其他用户的权限。
- `a`—更改所有权限（所有者、组和其他用户）。

表 9-2 显示了使用 `chmod` 命令的示例。

| 示例 | 结果 |
|---|---|
| `chmod u+x` | 所有者被授予执行文件的权限。 |
| `chmod g=rw` | 所有组成员都可以读和写。 |
| `chmod u=rwx` | 所有者获得所有权限。 |
| `chmod u=rwx,g=rw,o=r` | 所有者获得所有权限，组获得读和写权限，所有其他用户获得读权限。 |
| `chmod +x` | 所有用户（所有者、组、其他用户）获得可执行权限（取决于 umask）。 |
| `chmod a+x` | 所有用户（所有者、组、其他用户）获得可执行权限（a 表示全部）。 |

表 9-2

在以下示例中，用户 geeko 使用 `chmod` 允许组 users 的其他成员写入 `hello.txt` 文件：

```
geeko@da10:~ > ls -la hello.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:40 hello.txt
geeko@da10:~ > chmod g+w hello.txt
geeko@da10:~ > ls -la hello.txt
-rw-rw-r-- 1 geeko users 0 2006-04-06 12:40 hello.txt
```

使用选项 `-R`（递归）和指定的目录，您可以更改其下所有目录和文件及子目录的访问权限。除了使用字母（rwx）之外，您还可以使用数字组以八进制方式表示权限字母。

Linux 系统中的每个文件和目录都有一个分配给它的数字权限值。该值有三位数字。

第一位数字表示分配给文件或目录所有者的权限。第二位数字表示分配给文件或目录相关组的权限。第三位数字表示分配给其他用户的权限。

每个数字是分配给它的以下三个值的总和：

- 读：4
- 写：2
- 执行：1

例如，假设文件名为 `myfile.txt` 的文件分配了 754 权限。

这意味着文件所有者具有读、写和执行权限（4+2+1），文件相关组具有读和执行权限（4+1），其他用户具有读权限（4）。

通过使用数字等价，您可以按表 9-3 所示相加数字。

| 所有者 | 组 | 其他 |
|---|---|---|
| rwx | r-x |  |
| 4+2+1 (4+2+1=7) | 4+1 (4+1=5) | 4 (4) |

表 9-3

表 9-4 显示了使用数字代替字母的示例。

| 示例 | 结果 |
|---|---|
| `chmod 754 hello.txt` | 所有者获得所有权限，组获得读和执行权限，所有其他用户获得读权限（rwx r-x r--）。 |
| `chmod 777 hello.txt` | 所有用户（用户、组、其他用户）获得所有权限（rwx rwx rwx）。 |

表 9-4

### 使用 chown 和 chgrp 更改文件所有权

用户 root 可以使用以下语法使用 `chown` 命令更改文件的用户和组归属：

```
chown new_user.new_group file
```

要更改所有者但不更改组，可以使用以下命令语法：

```
chown new_user file
```

要更改组但不更改用户，可以使用以下命令语法：

```
chown .new_group file
```

您也可以使用以下语法使用 `chgrp` 命令更改文件的组归属：

```
chgrp new_group file
```

普通用户可以使用以下语法使用 `chown` 命令将他拥有的文件分配给新组：

```
chown .new_group file
```

用户只有在他是新组的成员时，才能更改他拥有的文件的组归属。

在下面的示例中，root 使用 `chown` 将 `hello.txt` 文件的所有权从 geeko 更改为用户 tux：

```text
da10:/tmp # ls -la hello.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:43 hello.txt
da10:/tmp # chown tux:users hello.txt
da10:/tmp # ls -la hello.txt
-rw-r--r-- 1 tux users 0 2006-04-06 12:43 hello.txt
da10:/tmp #
```

在下面的示例中，使用 `chown` 将 `list.txt` 文件的访问权限限制为 advanced 组的成员：

```text
da10:/tmp # ls -la list.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:43 list.txt
da10:/tmp # chown :advanced list.txt
da10:/tmp # ls -la list.txt
-rw-r--r-- 1 geeko advanced 0 2006-04-06 12:43 list.txt
da10:/tmp #
```

当然，root 和文件所有者仍然拥有访问文件的权限。尽管组已更改，但所有者权限保持不变。

![](img/9129877170834ca9d5fdac5319bf5f12_308_0.png)

## 练习 9-2：管理文件权限和所有权

在本练习中，你创建具有不同权限的目录。

首先，创建一个 `/files/` 目录，其中包含两个子目录（`private/` 和 `public/`）。

更改 `private/` 目录的权限，使只有 root 具有读、写和执行权限，并更改 `public/` 的权限，使每个人对该目录都有权限。

然后，切换到用户 geeko。尝试在这些目录中的每一个内创建一个 geeko 文件。

更改 `/files/public/geeko` 文件的权限，使 users 组具有写权限，而其他用户没有任何权限。

## 完成此练习的详细步骤

Part I: Create a Private and a Public Directory

Part II: Try to Create a File as a Normal User in Both Directories

## Part I: Create a Private and a Public Directory

要创建私有和公共目录，请执行以下操作：

- 1. 打开一个终端窗口。
- 2. 使用密码 n0v3ll 切换到 root (`su -`)。
- 3. 通过输入创建 `/files/` 目录

```text
mkdir /files
```

- 4. 通过输入更改到 `/files/` 目录

```
cd /files
```

- 5. 通过输入在 `/files/` 下创建 private 和 public 子目录

```
mkdir private public
```

- 6. 通过输入更改 `private/` 目录的权限，使只有 root 具有读、写和执行权限

```
chmod 700 private
```

- 7. 通过输入更改 `public/` 目录的权限，使每个人对该目录都有权限

```
chmod 777 public
```

- 8. 通过输入验证更改

```
ls -l
```

## Part II: Try to Create a File as a Normal User in Both Directories

要尝试以普通用户身份在两个目录中创建文件，请执行以下操作：
