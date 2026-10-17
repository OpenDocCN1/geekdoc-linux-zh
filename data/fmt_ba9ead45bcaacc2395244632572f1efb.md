
```
D:\WINNT\system> cat -n setup.inf

1 [setup]
2     help = setup.hlp
3
4 ; Place any programs here that should be run at the end of setup.
5 ; These apps will be run in order of their appearance here.
6 [run]
7
8 [dialog]
9     caption   = "Windows Setup"
10    exit      = "Exit Windows Setup"
11    title     = "Installing Windows 3.1"
12    options   = "In addition to installing Windows 3.1, you can:"
13    printwait = "Please wait while Setup configures your printer(s)..."

20 [data]
21	; Disk space required
22	; <type of setup>» <Full install space> <Min install space>
23
24	upd2x386full = 10000000,6144000	; 10.0 Mb,  6.144 Mb
25	upd2x286full = 9000000,6144000	; 9.0 Mb,  6.144 Mb
26	upd3x386full = 5500000,5000000	; 5.5 Mb,  5.0 Mb
27	upd3x286full = 5500000,5000000	; 5.5 Mb,  5.0 Mb
28
29	new386full	 = 10000000,6144000	; 10.0 Mb,  6.144 Mb
30	new286full	 = 9000000,6144000	; 9.0 Mb,  6.144 Mb
31
32	netadmin		 = 16000000		; 16.0 Mb
33	netadminupd	 = 16000000		; 16.0 Mb
34	upd2x386net	 = 300000		;  .3 Mb
35	upd3x386net	 = 300000		;  .3 Mb
36	upd2x286net	 = 300000		;  .3 Mb
37	upd3x286net	 = 300000		;  .3 Mb
38	new386net	 = 300000,300000	;  .3 Mb,  .3 Mb
39	new286net	 = 300000,300000	;  .3 Mb,  .3 Mb
40
41
42
43	; Defaults used in setting up and names of a few files
44	startup	 = WIN.COM
```

#### `chmod`

`chmod` - 使用符号或绝对（有时称为数字）模式更改指定文件的权限。符号模式将在下文描述。

受影响对象符号：
- `u` 影响用户。
- `g` 影响组。
- `o` 影响其他人。
- `a` 影响所有用户。

要执行的操作：
- `+` 添加权限。
- `-` 移除权限。
- `=` 替换权限。

指定的权限：
- `r` 读权限。
- `w` 写权限。
- `x` 执行权限。
- `u` 复制用户权限。
- `g` 复制组权限。
- `o` 复制其他人权限。

以下示例同时使用了两种模式。使用绝对或数字模式，文件 `cat1.exe` 的权限从 666 更改为 777。使用符号模式，然后为所有用户移除执行权限：

```
D:\> ls -l catl.exe
-rw-rw-rw-    1 Administ Administ     71323 Feb 20 11:34 catl.exe

D:\> chmod 777 catl.exe

D:\> ls -l catl.exe

-rwxrwxrwx     1 Administ Administ     71323 Feb 20 11:34 catl.exe

D:\> chmod a-x catl.exe

D:\> ls -l catl.exe

-rw-rw-rw-    1 Administ Administ     71323 Feb 20 11:34 catl.exe
```

#### `cp`

`cp` - 复制文件和目录。

以下是某些常用选项：
- `-i` 交互式复制，系统会提示你确认是否覆盖现有文件。
- `-f` 如果发生文件名冲突，强制用正在复制的文件覆盖现有文件。
- `-p` 复制时保留权限。
- `-R` 递归复制，包括子树。

以下示例展示了使用 `cp` 命令将 `cat1.exe` 复制到 `cat2.exe`，然后列出所有以 `cat` 开头的文件：

```
D:\> cp cat1.exe cat2.exe

D:\> ls -l cat*

-rw-rw-rw-  1 Administ  Administ  71323 Feb 20 11:34 cat1.exe
-rw-rw-rw-  1 Administ  Administ  71323 Feb 20 11:47 cat2.exe
```

#### `find`

`find` - 递归遍历目录结构查找列出的文件。

以下是某些常用选项：
- `-f` 指定 `find` 要遍历的文件层级结构。
- `-s` 遇到符号链接时，使用链接引用的文件，而不是链接本身。
- `-x` 不下降到具有与开始下降的文件不同的设备号的目录。
- `-print` 将路径名打印到标准输出。
- `-size n` 如果文件大小为 n，则为真。

#### `grep`

`grep` - 搜索文本并显示结果。

以下示例展示了使用 `grep` 在文件 `setup.inf` 中查找 "shell" 出现的所有位置：

```
D:\> grep shell setup.inf

[shell]
00000000="shell versions below 3.01",unsupported net
00030100="shell versions below 3.21",novell301
00032100="shell versions 3.21 and above",novell321
00032600="shell versions 3.26 and above",novell326
    #win.shell, 0:
    #win.shell, 0:
[win.shell]
    shell.dll
    system.ini, Boot,    "oldshell"          ,"shell"
```

#### `ls`

![](img/75f39fc91296b889c0653851accdfd46_1340_0.png)

`ls` - 列出目录的内容。

一些常用选项：
- `-a` 列出所有条目。
- `-c` 使用文件的最后修改时间来确定文件列出的顺序。
- `-d` 仅列出目录名，而不列出其内容。
- `-g` 在输出中包含组信息。
- `-i` 在报告的第一列中打印 inode 号。
- `-q` 非打印字符用“?”表示。
- `-r` 反转文件打印的顺序。
- `-s` 以块为单位显示大小，而不是字节。
- `-t` 按保存时间排序列出，最近的排在前面。
- `-u` 使用最后访问时间而不是最后修改时间来确定文件打印的顺序。
- `-A` 与 `-a` 相同，但不列出当前目录和父目录。
- `-C` 产生多列输出。
- `-F` 目录后跟“/”，可执行文件后跟“*”，符号链接后跟“@”。
- `-L` 列出链接指向的文件或目录。
- `-R` 递归列出子目录。

我在接下来的几页中包含了几个示例。

![](img/75f39fc91296b889c0653851accdfd46_1341_0.png)
