

# vi 编辑器简介

输入 q 并按下回车键（Return），你应该就会回到 shell 提示符：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_212_0.png)

- 2. 如果操作顺利没有问题，请跳到下一节指令 3。
如果操作没有成功，你将收到“未知终端类型”（unknown-terminal-type）的消息。
你可能会在屏幕上看到这些内容：

```
% vi
% "unknown": Unknown terminal type
I don't know what type of terminal you are on. All I have "unknown"
[using open mode]
```

或者，你可能会看到这些：
```
% vi
Visual needs addressable cursor or underline capability
```

不要惊慌。你可以解决这个问题。第一步是回到 shell 提示符。要做到这一点，请按照指令 1 中完全的方法完全操作：输入 `:q` 然后按下回车键。你应该会看到这些：
```
% "unknown": Unknown terminal type
I don't know what type of terminal you are on. All I have "unknown"
[using open mode]
```

这里的问题在于 vi 需要知道知道你正在使用的终端类型，但它无法自行确定。因此，你需要通过设置 `TERM` 环境变量来告诉操作系统。如果你知道你使用的是什么终端，请使用与终端关联的值；否则，使用默认的 `vt100`。

```
% setenv TERM vt100
```

如果你看到的是 $ 提示符，这意味着你正在使用 Bourne shell (sh) 或 Korn shell (ksh)，而不是 C shell (esh)，请尝试这个：

```bash
$ TERM=vt100 : export TERM
```

无论哪种方式，你现在都可以再次尝试运行 vi，它应该可以正常工作。

如果运行正常，如果你使用 csh，请将该命令（这两个命令中对你有效的那个）追加到你的 `.login` 文件中；如果你使用 sh 或 ksh，则追加到 `.profile` 中。你可以通过输入以下适用于你系统的任一命令来实现：

```bash
% echo setenv TERM vt100 >> .login
```

或者

```bash
$ echo "TERM=vt100; export TERM" >> .profile
```

这样一来，下次你登录时，系统将记住你正在使用的终端类型。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_213_0.png)

vi 和其他屏幕命令使用名为 `curses` 的 UNIX 软件包来控制屏幕。像大多数 UNIX 应用一样，curses 并不是为特定配置设计的；相反，它是为了设备无关设计的。因此，要在特定设备上运行，你需要给它一些额外信息——在这种情况下就是终端类型。
如果 `vt100` 不起作用，请向你的系统管理员反映问题，或联系你的 UNIX 供应商以查询具体的值应该是。如果你是通过调制调器或其他线路连接的，并且实际上使用的是终端模拟器或通信软件包，你也可以尝试将其作为 `TERM` 设置。如果失败了，请联系制作软件的公司，询问程序期望的终端类型。

- 3. 太棒了！你已经成功启动了 vi，看到了它的界面，甚至还输入了最重要的命令：退出命令。现在创建一个简单的文件并启动 vi，它会向你显示文件的内容：

```
% ls -l demo
% vi demo
```

| total 29 | 2 taylor | 512 Nov 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx------ | 2 taylor | 512 Dec 02:03 Infolist/ |
| drwx------ | 2 taylor | 1024 Dec 03:014 Mail/ |
| drwx------ | 2 taylor | 512 Oct 06:39 News/ |
| drwx------ | 4 taylor | 512 Dec 22:08 OWL/ |
| drwx-rw-- | 1 taylor | 126 Dec 3 16:34 awkscript |
| -rw-rw-- | 1 taylor | 165 Dec 3 16:42 bigfiles |
| drwx------ | 2 taylor | 512 Oct 13 10:45 bin/ |
| -rw-rw-- | 1 taylor | 0 Dec 3 22:26 demo |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_213_1.png)

| -rw-rw---- | 1 taylor | 12556 Nov 16 09:49 keylime.pie |
| -rw-rw---- | 1 taylor | 8729 Dec 2 21:19 owl.c |
| -rw-rw---- | 1 taylor | 199 Dec 3 16:11 sample |
| -rw-rw---- | 1 taylor | 207 Dec 3 16:11 sample2 |
| drwx- | 2 taylor | 512 Oct 13 10:45 src/ |
| drwrwx- | 2 taylor | 512 Nov 8 22:20 temp/ |
| -rw-rw---- | 1 taylor | 582 Nov 27 18:29 demo |

"demo" 17 行，846 个字符，你可以看到 vi 读取了指定的文件。在这个例子中，我的文件有 17 行，但我的屏幕可以容纳 25 行。最后，注意在底部，程序会显示文件名、文件行数以及总字符数。再次输入 `:q` 退出并返回命令行。现在当你输入冒号时，光标会移动到底部，像之前一样。你已经学会了 vi 中最基础的命令——`:q` 命令以及。从这里开始，你将学习如何在 vi 中使用光标。向左移动输入 `h`。向上移动输入 `k`。向下移动 `j`，向右移动输入 `l`。你可以通过退格键向左移动一个字符，并移动到行首。

- 1. 再次启动 vi，指定 demo：
```
% vi demo
```

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx- | 3 taylor | 512 Dec 3 02:03 Infoworld/ |
| drwx- | 2 taylor | 1024 Dec 3 01:43 Mail/ |
| drwx- | 2 taylor | 512 Oct 6:36 News/ |
| drwx- | 4 taylor | 512 Dec 22:08 OWL/ |
| -rw-rw- | 1 taylor | 126 Dec 3 16:34 awkscript |
| -rw-rw- | 1 taylor | 165 Dec 3 16:42 bigfiles |
| -rw-rw- | 2 taylor | 512 Oct 13 10:45 dev/ |
| -rw-rw- | 1 taylor | 0 Dec 3 22:26 demo |
| -rw-rw- | 1 taylor | 12556 Nov 16 09:49 keyline.py |
| -rw-rw- | 1 taylor | 8729 Dec 2 21:19 owl.c |
| -rw-rw- | 1 taylor | 198 Dec 3 16:11 sample |
| -rw-rw- | 1 taylor | 207 Dec 3 16:11 sample2 |
| drwx- | 2 taylor | 512 Oct 13 10:45 src/ |
| drwxrw- | 2 taylor | 512 Nov 8 22:20 temp/ |
| -rw-rw-- | 1 taylor | 582 Nov 27 18:29 demo |

"demo" 17 行，846 个字符，你应该看到光标位于第一行 `total` 的 `t` 上，或者在 `t` 字符下方。你可能有一个闪烁的光块，或者是不同颜色的光标。无论如何，那里都是你在文件的起始点。

- 2. 输入 `h` 尝试向左移动。光标留在原地，vi 提醒你不能在该行内进一步移动。尝试按 `k` 键向上移动；会发生同样的情况。现在输入 `j` 向移动一个字符：

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx- | 3 taylor | 512 Dec 3 02:03 Infoworld/ |
| drwx- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

现在光标位于文件第二行的目录指示上。

- 3. 使用四个光标控制键——`h`、`j`、`k` 和 `l` 键——在文件中移动一会儿，直到你对屏幕上的变化感到熟悉。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_215_0.png)

现在尝试使用退格键和回车键看看它们如何帮助你移动。

- 4. 移动到行中间：

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 2 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

在这里，我处于列表中第二个文件大小的中间数字。这里有几个光标移动键：`0`（零）键将光标移动到行首，`$` 将其移动到行尾。首先，我输入：

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 3 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

现在我输入 `$` 移动到行尾：

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 3 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

- 5. 如果你的键盘上有方向键，尝试看看它们是否和 `h`、`j`、`k` 和 `l` 键的作用一样。如果方向键没有移动你，它们可能将你切换到了插入模式。如果你输入字符并它们被添加到文件中，你需要按下 Escape 键（或 Esc，取决于你的键盘）返回命令模式。让我们通过退出此会话来结束。由于 vi 现在知道你修改了文件，它会尝试确保你不在不保存更改的情况下退出：

```
~~
:No write since last change (:quit! overrides)
```

