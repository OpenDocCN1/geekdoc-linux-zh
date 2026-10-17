
11. `________________________` 是视频适配器卡硬件的抽象表示，程序可以使用它们而不是直接与视频适配器卡硬件通信。

12. 一个(n) `________________________` 安装包含很少的工作站软件包，但包含多个服务器服务。

13. `___________` 启动是指引导加载程序允许用户在 Linux 和另一个操作系统（如 Windows）之间进行选择。

14. 用户登录到终端后，她收到一个称为 `___________` 的用户界面，然后该界面接受用户输入并将此输入传递给内核进行处理。

15. Linux 命令最常见的文档形式是 `___________` 页。

### 第 4 章

## 探索 Linux 文件系统

完成本章后，你将能够：

- 使用相对和绝对路径名理解并导航 Linux 目录结构
- 描述各种类型的 Linux 文件
- 查看文件名和文件类型
- 使用 shell 通配符指定多个文件名
- 显示文本文件和二进制文件的内容
- 使用 `grep` 搜索文本文件中的正则表达式
- 识别当今常用的文本编辑器
- 使用 `vi` 编辑器操作文本文件

理解 Linux 文件系统的结构和命令对于有效地使用 Linux 操作数据至关重要。在本章的第一部分中，你将通过更改在文件系统树中的位置并列出不同类型的文件名来探索 Linux 文件系统层级结构。接下来，你将查看用于指定多个文件名的 shell 通配符元字符，并使用标准 Linux 命令查看文件内容。然后，你将学习用于在文件中搜索文本的正则表达式元字符，并了解 `vi` 文本编辑器及其等效工具。

### Linux 目录结构

使用 Linux 操作系统的基础是了解 Linux 如何在硬盘上存储文件。典型的 Linux 系统可能在硬盘上拥有成千上万的数据文件和程序文件；因此，需要一个结构来组织这些文件，以便更容易地找到和操作数据以及运行程序。回顾前一章的内容，Linux 使用逻辑目录树将文件组织到不同的目录（也称为文件夹）中。当用户在某个目录中存储文件时，它们会物理存储在一台计算机内部硬盘的某个分区上的文件系统中。大多数人熟悉图 4-1 中所示的 Windows 操作系统目录树结构；硬盘分区上的每个文件系统都由一个驱动器字母（如 `C:` 或 `D:`）引用，并拥有一个根目录（由 `\` 字符指示），其中包含共同形成层次树状的子目录。

在目录树中正确描述目录很重要；文件或目录的绝对路径名是从根目录开始的特定文件或目录的完整路径名。根据图 4-1，`color` 目录的绝对路径名是 `C:\windows\color`，而 `sue` 目录的绝对路径名是 `D:\home\sue`。换句话说，我们将 `C:\windows\color` 称为 `C:` 驱动器根目录下 `windows` 目录下的 `color` 目录。类似地，我们将 `D:\home\sue` 称为 `D` 驱动器根目录下 `home` 目录下的 `sue` 目录。

Linux 使用类似的目录结构；然而，没有驱动器字母。只有一个根（使用 `/` 字符表示），而硬盘分区上的不同文件系统被挂载到这个目录树的不同目录中，使得文件系统对用户是透明的。与图 4-1 中所示的 Windows 示例目录树等效的 Linux 示例目录树如图 4-2 所示。

根据图 4-2，`color` 目录的绝对路径名是 `/windows/color`，而 `sue` 目录的绝对路径名是 `/home/sue`。换句话说，我们将 `/windows/color` 目录称为系统根（`/` 字符）下 `/windows` 目录下的 `color` 目录。类似地，我们将 `/home/sue` 目录称为系统根下 `home` 目录下的 `sue` 目录。

![](img/09bf13b782f71165e17bb3839040c96a_133_0.png)

![](img/09bf13b782f71165e17bb3839040c96a_133_1.png)

#### 更改目录

当用户登录到他的 Linux 系统时，他会被放置在他的主目录中，这是每个用户存储个人文件的独特位置。普通用户通常拥有一个位于 `/home` 目录之下、以其用户账户命名的主目录，例如 `/home/sue`。然而，`root` 用户在系统根目录（`/root`）下拥有一个名为 `root` 的主目录，如图 4-2 所示。你可以通过观察 shell 提示符末尾的名称或在命令行提示符下输入 `pwd`（print working directory，打印当前工作目录）命令并按 Enter 键来确认你当前所在的系统目录。如果你以 `root` 用户身份登录，终端屏幕上将显示以下输出：

```
[root@server1 root]# pwd
/root

[root@server1 root]#
```

但是，如果你以用户 `sue` 身份登录，你会看到以下输出：

```
[sue@server1 sue]$ pwd
/home/sue

[sue@server1 sue]$
```

要更改目录，你可以发出带有指定目标目录参数的 `cd`（change directory，更改目录）命令。如果你不指定目标目录，`cd` 命令只是将你返回到你的主目录：

```
[root@server1 root]# cd /home/mary
[root@server1 mary]# pwd
/home/mary
```

```
[root@server1 mary]$ cd /etc 
[root@server1 etc]$ pwd 
/etc 
[root@server1 etc]$ cd 
[root@server1 root]$ pwd 
/root 
[root@server1 root]$_ 
```

`~` 元字符也可以用于指代当前用户的主目录。或者，你还可以在 `~` 元字符末尾附加一个用户名，使用该元字符来指定另一个用户的主目录：

```
[root@server1 root]$ cd ~mary 
[root@server1 mary]$ pwd 
/home/mary 
[root@server1 mary]$ cd ~ 
[root@server1 root]$ pwd 
/root 
[root@server1 root]$_ 
```

在之前讨论的许多示例中，`cd` 命令后指定的参数是目录的绝对路径名，这意味着系统拥有查找目标目录所需的所有信息，因为路径名从系统根（`/`）开始。然而，在大多数 Linux 命令中，你还可以使用相对路径名代替绝对路径名以减少输入。相对路径名是目标文件或目录相对于你在树中当前目录的路径名。要指定你当前目录下的一个目录，只需通过名称引用该目录（不要以 `/` 字符开始路径名）。要引用树中更接近根的一个目录（也称为父目录），只需使用两个点（`..`）。下面展示了一个使用相对路径名在目录树中移动的示例：

```
[root@server1 root]$ cd /home/mary 
[root@server1 mary]$ pwd 
/home/mary 
[root@server1 mary]$ cd .. 
[root@server1 home]$ pwd 
/home 
[root@server1 home]$ cd mary 
[root@server1 mary]$ pwd 
/home/mary 
[root@server1 mary]$_ 
```

在上面的示例中，我们使用 `..` 向上移动一个父目录，然后使用单词 `mary` 来指定相对于我们在树中当前位置的 `mary` 子目录；但是，你也可以在目录树中上下移动多层：

```
[root@server1 root]# cd /home/mary
[root@server1 mary]$ pwd
/home/mary
[root@server1 mary]$ cd ../..
[root@server1 /]$ pwd
/
[root@server1 /]$ cd home/mary
[root@server1 mary]$ pwd
/home/mary
[root@server1 mary]$
```

![](img/09bf13b782f71165e17bb3839040c96a_135_0.png)

你也可以使用一个点（`.`）来指代当前目录。虽然在使用 `cd` 命令时这并不方便，但你将在本书后面使用一个点。

虽然当指定某个文件或目录的位置时，使用绝对路径名作为命令的参数很直接，但如果当前目录距离根目录较远，相对路径名可以为你节省大量输入并减少出错的可能性。例如，假设当前目录是 `/home/sue/projects/acme/plans`，你需要将其更改为 `/home/sue/projects/acme` 目录。使用绝对路径名，你需要输入 `cd /home/sue/projects/acme`；然而，使用相对路径名，你只需要输入 `cd ..` 就能完成同样的任务，因为 `/home/sue/projects/acme` 目录是目录树中当前位置的一个父目录之上。
