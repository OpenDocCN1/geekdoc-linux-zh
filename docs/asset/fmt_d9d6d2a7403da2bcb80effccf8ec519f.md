
为了查找这些目录中的每一个信息，可以使用 `find` 的 `-exec` 选项。遗憾的是，我不能直接输入命令：`-exec` 选项必须配合 `{}` 使用（`{}` 会被匹配到的文件名替换），并在命令末尾使用 `\;`。（如果漏掉 `\`，shell 会把 `;` 解释为命令的结束）。你必须确保 `{}` 和 `\;` 之间有一个空格。

```
% find -type d -exec ls -ld {} {}
drwxr-xr 1024 Dec 10 14:13
drwxr-xr 532 Dec 6 18:31 /OWL
drwxr-xr 512 Dec 2 21:18 /Doc
drwxr-xr 512 Nov 7 11:52 /OWL/WordMap
drwxr-xr 512 Dec 10 13:30 /.elm
drwxr-xr 512 Dec 21 10:30 /Archives
drwxr-xr 512 Dec 3 02:03 /InfoWorld
drwxr-xr 512 Sep 30 10:38 /InfoWorld/PIMS
drwxr-xr 1024 Dec 9 11:42 /Mail
drwxr-xr 512 Oct 6 09:38 /News
drwxr-xr 512 Dec 10 13:58 /bin
drwxr-xr 512 Oct 13 10:45 /src
drwxr-xr 512 Nov 8 22:20 /temp
```

### `find` 删除核心文件

`find` 命令通常用于删除超过几天的核心文件（core files）。正如你记得的，这些核心文件是程序意外崩溃时运行程序内存镜像的副本。它们可能非常巨大，偶尔修剪一下是明智的：

```
% find -name core -ctime -4 -exec /bin/rm -f {} \;
```

这条命令没有输出，因为我没有在命令末尾使用 `-print`。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_409_0.png)

## 搜索信息和文件

`find` 命令是 UNIX 中强大的命令。它可以帮助你根据所有者、文件名和其他属性查找文件。该命令最笨拙的部分是 `-exec` 选项所需的元素元素，而这正是 `xargs` 命令非常有帮助的地方。

### 任务 19.2：结合 xargs 使用 find

你可以使用 `find` 搜索文件，使用 `grep` 在文件内部进行搜索，但如果你想组合使用呢？这就是 `xargs` 大显身手的地方。

#### 1. 几天前

输出很有趣，但它没有包含任何文件名！

#### 2. 使用 `-l` 标志

第二种更聪明的策略是使用 `-l` 标志，让 `grep` 只指定匹配到的文件名：

```
% find -type f -exec grep -l i mapping {} \; \
./OWL/WordMap/msw-to-txt.c
./elm/aliases.text
./Mail/mark
./News/usetnam.alt
./bin/my_new_cmd: Permission denied
./src/fixit.c
./temp/attach.msg
```

#### 3. 使用 `xargs` 提高效率

这是朝着正确方向的一步，但这种方法的问题是，每匹配到一个文件就会调用一次 `grep`，这是一种非常消耗资源的策略。相反，你使用 `xargs` 读取 `find` 的输出并构建 `grep` 调用（记住，每看到一个文件，`grep` 程序都会检查它），一次性指定大量文件。这样一来，即使检查了 200 或 300 个文件，`grep` 也只会被调用四五次。默认情况下，`xargs` 总是跟踪文件名列表直到指定命令的末尾，因此使用它非常简单：

```
% find -type f -print | xargs grep -l i mapping
./OWL/WordMap/msw-to-txt.c
./elm/aliases.text
./Mail/mark
./News/usetnam.alt
./bin/my_new_cmd: Permission denied
./src/fixit.c
./temp/attach.msg
```

这得到了相同的输出，但速度快得多。

#### 4. 显示匹配行

这种方法的妙处在于，由于 `grep` 接收了多个文件，当 `grep` 显示匹配行时，它会自动包含包含任何匹配项的文件名。移除 `-l` 标志的结果正是我想要的：

```
% find -type f -print | xargs grep -i m mapping
./OWL/WordMap/msw-to-txt.c:typedef struct mappings {
./OWL/WordMap/msw-to-txt.c:int entry character-mapping[] = {
long-mappings = FALSE;
./OWL/WordMap/msw-to-txt.c:int c
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_411_0.png)

## 与他人交流

```
% mesg n
% is -l `tty`
crw-x--- 1 taylor 21, 71 Dec 8 10:34 /dev/ttyAo*
```

#### 检查终端写权限

在任何时候，你都可以通过输入不带任何标志的 `mesg` 来检查你当前的终端写权限。输出非常简洁，但它能告诉你是你想知道的信息：

```
% mesg
nis n
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_416_0.png)

要查看你 tty 的设置，请在 `tty` 命令上使用反引号（backquotes），如前面的示例所示。

不要向任何人透露这个秘密。一旦你给别人的终端开启了写权限，你就可以像处理 UNIX 中的任何其他文件一样，轻松将命令的输出重定向到他们的 tty 设备。事实上，这就是 `write` 命令的工作原理：它打开对方的 tty 进行写入，你输入的每行也会被写入对方的屏幕上。记住这一点是为了让你明白为什么你的 `/dev/tty` 行权限如此重要，而不是为了让你肆意妄为开始折磨你的 UNIX 用户！

### 任务 20.2：使用 write 向其他用户写入

现在你已经允许他人写入你的终端，也可以防止他们写入，现在是时候了解如何向他们的终端写入，以及利用这项功能可以做什么了。与他人直接交互的命令是 `write` 命令。这是一个相对简单的命令。当你启动 `write` 时，你需要指定想要交流的其他用户，`write` 将仅为你启动，然后它会“呼叫”（pages）对方，让他们知道你想要与其交流。

一旦进入程序，只要你按下回车键，你发送的每一行都会立即到达对方那里。然而，在他们系统中使用 `write` 响应之前，你无法向他们发送任何消息。网络礼仪建议先连接，然后等待对方与你建立连接。然后你们就可以对话了！

要与某人连接，你只需要在 `write` 后指定该人的用户名。如果用户登录了多次，`write` 会尝试选择最近使用的线路，但并不总是成功。使用 `w` 命令是一个好策略。只需查看每个连接的空闲时间（idle time），即可识别该人实际上在使用哪条线路。一旦确定了连接，你就可以使用用户名和所需的 tty 线路来调用 `write`。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_416_1.png)

## 操作

1. 我总是先确保我已经开启了 `mesg`，以确保他人可以写入我的终端。否则，另一端的家伙试图跟我说话时会非常沮丧的！

```
% mesg
is y
```

2. 查看朋友是否在系统上的最佳方法是使用 `who` 命令并将输出通过给 `grep` 程序。

```
% who grep marv
marv ttyAx Dec 8 10:30
```

他登录在 tty 线路 `/dev/ttyAx`（只需在 `who` 显示的线路前加上 `/dev/`）。我可以使用 `-l` 来查看他是否开启了消息接收：

```
% is -l /dev/ttyAx
crw-rw---- Dec 21, 71 10:33 /dev/ttyAx*
```

3. 邀请他加入 `write` 会话，我只需输入以下：

```
% write marv
```

他在屏幕上看到的是如下：

> Message from taylor@netcom.com on ttyAo at 10:38 ... --

4. 现在我必须等他回复，这应该只需要几秒钟。他输入 `write taylor`，然后我看到：

Message from marv@netcom.com on ttyAx at 10:40 ...

我们都连接成功了。礼仪建议我等他的初始问候，它会出现在我的屏幕上，没有任何开场白：

Hi Dave! -o

我可以向他输入内容，他也可以向我输入内容。当我结束交流时，我按下 `^d` 结束，他也同样这样做：

Okay, I'll talk with you tomorrow. --oo

See ya! --oo

^d

EOF

按一次回车键我就能回到系统提示符 `%`。
