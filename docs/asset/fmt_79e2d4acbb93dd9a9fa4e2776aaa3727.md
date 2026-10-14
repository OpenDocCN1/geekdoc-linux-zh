
- 1 点击显示终端窗口。
- 2 终端窗口出现。
- 此区域显示命令行，你可以在其中输入命令。在输入命令之前，你可能需要点击此区域。
注意：有关你可以输入的命令列表，请参阅第 234 页。
- 当你完成命令行使用后，点击 X 关闭窗口。

232

## 我为什么想使用命令行？

- 某些任务只能在命令行中执行，例如停止文件打印。
- 在命令行中执行许多许多任务（如移动文件）会快得多。
- 如果你在 Linux 上遇到问题，可以使用命令行来修复问题。
- 有些人喜欢只显示文本的屏幕工作。

![](img/e2eac216eed4c6806c742998f1420a0c_244_0.png)

Red Hat Linux release 6.1 (Cartman)

Kernel 2.2.12-20.el.i686

Red Hat Linux release 6.1 (Cartman)

Kernel 2.2.12-20.el.i686

```
localhost: smith
Password:
```

```
localhost: smith
Password:
Last login: Mon Oct 25 14:45:29 on localhost
smith@ca~$
```

- 1 按住 Ctrl+Alt 并按 F1 全屏显示命令行。
- 2 输入用户名并按回车。
- 3 输入密码并按回车。注意：密码不会显示在屏幕上。
- 4 显示你可以登录的行。
- 3 命令行出现。完成命令行使用后，输入 `exit` 并按回车退出命令行。
- 5 按住 Ctrl+Alt 并按 F7 返回桌面。

## 常用 Linux 命令

![](img/e2eac216eed4c6806c742998f1420a0c_245_0.png)

![](img/e2eac216eed4c6806c742998f1420a0c_245_1.png)

### CD

更改当前目录。
- 1 输入 `cd` 后跟想要更改的目录位置和名称。按回车。注意：如果不输入位置，Linux 将切换到主目录。

![](img/e2eac216eed4c6806c742998f1420a0c_245_2.png)

### CHMOD

更改文件的读、写和执行权限。
- 1 输入 `chmod` 后跟 `u`、`g` 或 `a`（用户、组或其他）指定你想更改权限的对象。
- 2 输入 `+` 或 `-` 允许或拒绝权限。
- 3 输入 `r`、`w` 或 `x`（读、写或执行）指定你想允许或拒绝的权限类型。
- 4 输入你想更改的文件位置和名称。按回车。

![](img/e2eac216eed4c6806c742998f1420a0c_245_3.png)

![](img/e2eac216eed4c6806c742998f1420a0c_245_4.png)

### CLEAR

清除屏幕。
- 1 输入 `clear` 并按回车。

![](img/e2eac216eed4c6806c742998f1420a0c_245_5.png)

### CP

创建文件的精确副本并将其存放在新位置。
- 1 输入 `cp` 后跟想要复制的文件位置和名称。
- 2 输入想要放置副本的目录位置和名称。按回车。

## 使用命令行

![](img/e2eac216eed4c6806c742998f1420a0c_246_0.png)

![](img/e2eac216eed4c6806c742998f1420a0c_246_1.png)

### DATE

显示当前日期和时间。
- 1 输入 `date` 并按回车。

### EXIT

关闭终端窗口或注销当前用户。
- 1 输入 `exit` 并按回车。

![](img/e2eac216eed4c6806c742998f1420a0c_246_2.png)

![](img/e2eac216eed4c6806c742998f1420a0c_246_3.png)

![](img/e2eac216eed4c6806c742998f1420a0c_246_4.png)

![](img/e2eac216eed4c6806c742998f1420a0c_246_5.png)

### FILE

识别文件类型。
- 1 输入 `file` 后跟要识别的文件位置和名称。按回车。

### FIND

查找文件。
- 1 输入 `find -name` 后跟要查找的文件名。按回车。

![](img/e2eac216eed4c6806c742998f1420a0c_246_6.png)

235

## 常用 Linux 命令

```
Terminal
File Edit Settings Help
[root@localhost /root# gunzip /root/sales_pian.gz]
```

```
Terminal
File Edit Settings Help
[root@localhost /root# kill 8311]
```

### GUNZIP

解压缩文件以便操作。文件压缩是为了减小大小。
- 解压 `.gz` 扩展的文件，输入 `gunzip` 然后输入文件的位置和名称。按回车。
- 解压 `.zip` 扩展的文件，输入 `gunzip -S` 然后输入文件的位置和名称。按回车。

### KILL

关闭程序。这在程序停止响应时非常有用。
- 1 输入 `kill` 后跟要关闭的程序的进程 ID (PID)。按回车。
注意：你可以使用第 238 页所示的 `ps` 命令确定程序的 PID 数字。

```
Terminal
File Edit Settings Help
[root@localhost /root# less /usr/doc/emacs-20.4/READMEME]
```

```
Terminal
File Edit Settings Help
[root@localhost /root# ls business_letter mckenzie new_projects schedule core meetings nmail deadlines miscellaneous operating_costs.gnumeric
root@localhost /root#]
```

### LESS

显示文本文件的内容并允许你滚动文件。
- 输入 `less` 后跟想要显示的文件位置和名称。按回车。
- 要重新读取命令行，按 G 键。

### LS

列出当前目录下的文件和子目录。
- 1 输入 `ls` 并按回车。
注意：如果你想显示每个文件和子目录的信息，输入 `ls -la`

![](img/e2eac216eed4c6806c742998f1420a0c_247_0.png)

![](img/e2eac216eed4c6806c742998f1420a0c_247_1.png)

236

# 使用命令行

![](img/e2eac216eed4c6806c742998f1420a0c_248_0.png)

![](img/e2eac216eed4c6806c742998f1420a0c_248_1.png)

### MAN

显示命令的帮助信息。
- 输入 `man` 后跟你想要获取信息的命令名称。然后按 `Enter` 键。
- 若要重绘命令行，按 `Q` 键。

### MKDIR

创建一个新目录。
- 输入 `mkdir` 后跟你想要创建的目录的路径和名称。然后按 `Enter` 键。

![](img/e2eac216eed4c6806c742998f1420a0c_248_2.png)

![](img/e2eac216eed4c6806c742998f1420a0c_248_3.png)

### MV

将文件移动到新位置。
- 输入 `mv` 后跟你想要移动的文件路径和名称。
- 输入你想要放置文件的目录的路径和名称。然后按 `Enter` 键。

### PASSWD

更改你的密码。
- 输入 `passwd` 然后按 `Enter` 键。
注意：如果你是以普通用户登录的，Linux 将要求你输入当前密码。然后按 `Enter` 键。
- 输入新密码，然后按 `Enter` 键。
- 再次输入新密码以确认密码，然后按 `Enter` 键。

## 常用 Linux 命令

![](img/e2eac216eed4c6806c742998f1420a0c_249_0.png)

### PICO

启动一个允许你创建和编辑文本文件的程序。
- 输入 `pico` 然后按 `Enter` 键。
- 若要重新设计命令行，按住 `Ctrl` 键并按下 `X` 键。

![](img/e2eac216eed4c6806c742998f1420a0c_249_1.png)

![](img/e2eac216eed4c6806c742998f1420a0c_249_2.png)

| PID TTY | TIME | CMD |
| --- | --- | --- |
| 740 pts/2 | 00:00:00 | bash |
| 808 pts/2 | 00:00:00 | netscape-commun |
