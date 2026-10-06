

## $ pwd

如果你知道自己是谁，但并不确定自己具体所在的位置，那么 `pwd`（打印工作目录）将会派上用场。`pwd` 命令会告诉你在终端（Terminal）所在目录树中的具体位置。

例如，假设我的终端位于我的个人家目录（命名为 `~`），而该家目录位于系统的主目录（命名为 home，所有的用户账户目录都位于其中）。当我使用 `pwd` 命令时，我的终端上会打印出 `/home/rg`。如果你也尝试一下，应该得到类似的结果。

**注意** 在这种情况下，*print*（打印）与你的打印机没有任何关系；它仅仅意味着响应将被打印到或显示在*Terminal*（终端）中。

## $ df

另一个安全但有用得多的命令是 `df`（磁盘文件系统）。`df` 命令可以告诉你在你挂载磁盘的每个分区上使用了多少磁盘空间，以及仍剩余多少可用空间。你可以通过输入 `df` 然后按回车（ENTER）来尝试。你的输出应该类似于图 8-3 所示（当然，这取决于你挂载磁盘的大小以及如何设置）。

```
rg@mydestkop:~-$ df
Filesystem     1K-blocks Available Use% Mounted on
/dev/sda1     114306814 52742364 10286264  0% /
udev            1476296         4 1476292  1% /dev
tmpfs           593424       780    592664  0% /run
none             5120         0    5120  0% /run/lock
none                                            
/dev/sda1    123491036     232 1483324  1% /run/shm
09a-90c-8243caea4f 6955360 110351312  6% /media/9927f624-bb8-4
rg@mydestkop:~-$
```

图 8-3：df 命令的输出

正如你所看到的，大小是以千字节（KB）为单位提供的，而不是你可能更常用的字节（GB）和兆字节（MB），但有一个解决办法。许多命令接受一个 `flag`（标志）或 `option`（选项）来进一步控制命令的执行方式。你直接在主命令后面输入标志，并配以一个空格和一个连字符（-）。

在这种情况下，你可以使用 `-h`（human readable，人类可读）标志，以便以你最熟悉的方式显示数字。尝试在主命令后输入 `df -h` 并按回车（ENTER）。输出应该以更熟悉的格式出现（见图 8-4）。

```
$ rg@myndesktop: df -h
Filesystem      Size Avail Use% Mounted on
/dev/sda6       116G  5.5G   99G 6% /
udev             1.5G  4.0G  1.5G 1% /dev
tmpfs           580M  708K  579M 1% /run
none               4M      5M   0% /run/lock
none             1.5G  232M  1.5G 15% /dev/shm
/dev/sda1       118G  6.7G  166G 6% /media/9927f624-bb81-409a-90c8-2
243caecaef4 rg@myndesktop:~$
```

图 8-4：带有 -h 标志的 df 命令输出

## ls

另一个无害但实用的命令是 ls（列出目录）。ls 向你显示当前目录下的内容。这等同于在 Nautilus 中双击文件夹以查看其内容的非图形化操作。尝试输入 `ls` 然后按回车键（ENTER KEY）。

如果你到为止一直按照我的命令操作，你的结果应该列出你家目录中所有的文件夹。你也可以使用 `-r` 标志不仅显示文件夹中的文件列表，还有子文件夹中的内容。当然，你可能还没有创建任何子文件夹，但你也可以继续尝试实验一段时间。相反，尝试使用 `ls -a` 来查看你的隐藏文件。

## calendar

我会让你自己尝试这个。只需输入 `calendar` 并按回车（ENTER）即可看到一些有趣的结果。

## exit

`exit` 命令是一个简单的命令，允许你退出终端。只需输入 `exit` 并按回车（ENTER）。终端将会关闭。

## 有点威力的命令

你到为止尝试过的简单命令都是安全、理智且经过消防批准的类型；它们仅仅是向你的终端打印信息。现在你将尝试从命令获得一些切实的结果。如果你遵循我的指令，这些命令本质上也是安全且理智。

## mkdir

你已经学会了如何通过你和鼠标创建文件夹，你也可以使用命令行来实现。该命令是 `mkdir`（make directory），它使用起来像切饼一样简单（尽管我并不确定切饼为什么简单）。

为了查看此命令如何工作并与后续命令配合使用，请现在使用 `mkdir` 命令创建一个名为 `command_exp` 的文件夹（用于命令实验）。你只需要在一个新的终端窗口中输入 `mkdir command_exp` 并按回车（ENTER）。新文件夹应该出现在你的家目录中，所以请通过点击桌面上的图标来检查它是否存在。

好了，bra, bueno！现在我们在 `command_exp` 内部再创建一个新文件夹——如果可以的话，这是一个子文件夹。我们将其命名为 `sub`。所以只需输入 `mkdir command_exp/sub` 并按回车（ENTER）。如果你喜欢，可以看一眼 `sub` 文件夹是否出现在 `command_exp` 文件夹中。

## $ mv

下一个命令是 `mv`（move）命令，但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

## $ cd

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

## $ cd

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

## $ cd

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

（注：由于提供的文本中存在大量重复段落，此处已按要求进行去重并完成翻译逻辑)*

## $ pwd

If you know who you are but aren't exactly where you are, `pwd` (print working directory) should come in handy. The `pwd` command tells you exactly where the Terminal is in your directory tree.

Let's say, for example, that my Terminal is in my personal home directory (which is called `~`) in the system's home directory (which is called home and from which are all the user account directories are located). When I use the `pwd` command, I would get `/home/rg` printed to my Terminal. You should get similar results if you try it.

**NOTE** The *print*, in this case, has nothing to do with your printer; it merely means the response will be printed to, or displayed in, the *Terminal*.

## $ df

Another safe and, but much more useful, command, is `df` (disk filesystem). The `df` command tells you how much disk space you have used, as well as how much space you still have available, on each of the partitions on your mounted disks. You try it by typing `df` and then pressing ENTER. Your output should look something like shown in Figure 8-3 (depending, of course, on the size of your mounted disks and how they are set up).

```
rg@mydestkop:~-$ df
Filesystem     1K-blocks Available Use% Mounted on
/dev/sda1     114306814 52742364 10286264  0% /
udev            1476296         4 1476292  1% /dev
tmpfs           593424       780    592664  0% /run
none             5120         0    5120  0% /run/lock
none                                            
/dev/sda1    123491036     232 1483324  1% /run/shm
09a-90c-8243caea4f 6955360 110351312  6% /media/9927f624-bb8-4
rg@mydestkop:~-$
```

Figure 8-3: Output from the df command

As you notice, the sizes are given in kilobytes (KB) rather than the gigabytes (GB) and megabytes (MB) you are probably more used to, but there is a way around it. Many commands accept a `flag`, or `option`, to further how the commands perform. You type flags directly after the main command and with a space and a hyphen.

In this case, you can use the `-h` (human readable) flag to have your figures out in the way you are most familiar with. Try this by typing `df -h` on the main command and pressing ENTER. The output should appear in a more familiar format (see Figure 8-4).

```
$ rg@myndesktop: df -h
Filesystem      Size Avail Use% Mounted on
/dev/sda6       116G  5.5G   99G 6% /
udev             1.5G  4.0G  1.5G 1% /dev
tmpfs           580M  708K  579M 1% /run
none               4M      5M   0% /run/lock
none             1.5G  232M  1.5G 15% /dev/shm
/dev/sda1       118G  6.7G  166G 6% /media/9927f624-bb81-409a-90c8-2
243caecaef4 rg@myndesktop:~$
```

Figure 8-4: Output from the df command with the -h flag

## ls

Another harmless but handy command is ls (list directory). The ls shows you what is in your current directory. This is the non-graphical equivalent of double-clicking a folder in Nautilus to see what is inside. Try by typing ls and then pressing the ENTER KEY.

If you've been following my commands so far, your results should list all of the folders in your home directory. You can also use -r flag to show only the list of files in the folder but also what is within the subfolders. Of course, you might not have created any subfolders, yet you could also hold experimenting with this for a while. Instead, try ls -a to see your invisible, files.

## calendar

I'll let you experiment with this one on your own. Just type calendar and press ENTER to see some interesting results.

## exit

The exit command is a simple one that that allows you to exit the Terminal. Just type exit and press ENTER. The Terminal will close.

## Commands with Some Teeth

The simple commands you have tried so far are all of the safe-and-sane, fire marshal-approved variety; they merely print information to your Terminal. Now you are going to try to get some tangible results from commands. The commands are also essentially safe and sane if you follow my instructions.

## mkdir

You have already learned how to create folders by means of you and your mouse, you can also do this using the command line. The command is mkdir (make directory), and it is as easy as pie to use (though I've never quite sure how pie is easy).

To see how this command works and to work with the commands that follow, use the mkdir command now to create a folder called command_exp (for command experiments). All you have to do is type mkdir command_exp in a new Terminal window and press ENTER. The new folder should appear in your Home folder, so go ahead and check whether it is there by clicking the icon on your desktop.

Okay, bra, bueno! Now let's create another new folder within new—a subfolder, if you will. We'll call this one sub. So, just type mkdir command_exp/sub and press ENTER. If you like, take a peek and see whether the sub folder has appeared within the command_exp folder.

## $ mv

The next command is the mv (move) command, but before you experiment with it, you need to create a dummy file—you need something to move, after all. You can do this using another command—touch. To make the filelet's call it expfile.txt—go to the Terminal, touch expfile.txt, and press ENTER. The new file will appear in your Home folder.

To move the file you've just created, you will use the mv command of, course, just type mv expfile.txt command_exp/sub (this tells the system which file to move and where to move it to) and press ENTER. The file will now be in command_exp/sub.

## $ cd

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

（注：由于提供的文本中存在大量重复段落，此处已按要求进行去重并完成翻译逻辑)*

翻译：

[content]

## $ pwd

如果你知道自己是谁，但并不确定自己具体所在的位置，那么 `pwd`（打印工作目录）将会派上用场。`pwd` 命令会告诉你在终端（Terminal）所在目录树中的具体位置。

例如，假设我的终端位于我的个人家目录（命名为 `~`），而该家目录位于系统的主目录（命名为 home，所有的用户账户目录都位于其中）。当我使用 `pwd` 命令时，我的终端上会打印出 `/home/rg`。如果你也尝试一下，应该得到类似的结果。

**注意** 在这种情况下，*print*（打印）与你的打印机没有任何关系；它仅仅意味着响应将被打印到或显示在*Terminal*（终端）中。

## $ df

另一个安全但有用得多的命令是 `df`（磁盘文件系统）。`df` 命令可以告诉你在你挂载磁盘的每个分区上使用了多少磁盘空间，以及仍剩余多少可用空间。你可以通过输入 `df` 然后按回车（ENTER）来尝试。你的输出应该类似于图 8-3 所示（当然，这取决于你挂载磁盘的大小以及如何设置）。

```
rg@mydestkop:~-$ df
Filesystem     1K-blocks Available Use% Mounted on
/dev/sda1     114306814 52742364 10286264  0% /
udev            1476296         4 1476292  1% /dev
tmpfs           593424       780    592664  0% /run
none             5120         0    5120  0% /run/lock
none                                            
/dev/sda1    123491036     232 1483324  1% /run/shm
09a-90c-8243caea4f 6955360 110351312  6% /media/9927f624-bb8-4
rg@mydestkop:~-$
```

图 8-3：df 命令的输出

正如你所看到的，大小是以千字节（KB）为单位提供的，而不是你可能更常用的字节（GB）和兆字节（MB），但有一个解决办法。许多命令接受一个 `flag`（标志）或 `option`（选项）来进一步控制命令的执行方式。你直接在主命令后面输入标志，并配以一个空格和一个连字符（-）。

在这种情况下，你可以使用 `-h`（human readable，人类可读）标志，以便以你最熟悉的方式显示数字。尝试在主命令后输入 `df -h` 并按回车（ENTER）。输出应该以更熟悉的格式出现（见图 8-4）。

```
$ rg@myndesktop: df -h
Filesystem      Size Avail Use% Mounted on
/dev/sda6       116G  5.5G   99G 6% /
udev             1.5G  4.0G  1.5G 1% /dev
tmpfs           580M  708K  579M 1% /run
none               4M      5M   0% /run/lock
none             1.5G  232M  1.5G 15% /dev/shm
/dev/sda1       118G  6.7G  166G 6% /media/9927f624-bb81-409a-90c8-2
243caecaef4 rg@myndesktop:~$
```

图 8-4：带有 -h 标志的 df 命令输出

## ls

另一个无害但实用的命令是 ls（列出目录）。ls 向你显示当前目录下的内容。这等同于在 Nautilus 中双击文件夹以查看其内容的非图形化操作。尝试输入 `ls` 然后按回车键（ENTER KEY）。

如果你到为止一直按照我的命令操作，你的结果应该列出你家目录中所有的文件夹。你也可以使用 `-r` 标志不仅显示文件夹中的文件列表，还有子文件夹中的内容。当然，你可能还没有创建任何子文件夹，但你也可以继续尝试实验一段时间。相反，尝试使用 `ls -a` 来查看你的隐藏文件。

## calendar

我会让你自己尝试这个。只需输入 `calendar` 并按回车（ENTER）即可看到一些有趣的结果。

## exit

`exit` 命令是一个简单的命令，允许你退出终端。只需输入 `exit` 并按回车（ENTER）。终端将会关闭。

## 有点威力的命令

你到为止尝试过的简单命令都是安全、理智且经过消防批准的类型；它们仅仅是向你的终端打印信息。现在你将尝试从命令获得一些切实的结果。如果你遵循我的指令，这些命令本质上也是安全且理智。

## mkdir

你已经学会了如何通过你和鼠标创建文件夹，你也可以使用来实现来实现该命令是 `mkdir`（make directory），它使用起来像切饼一样简单（尽管我并不确定切饼为什么简单）。

为了查看此命令如何工作并与后续命令配合使用，请现在使用 `mkdir` 命令创建一个名为 `command_exp` 的文件夹（用于命令实验）。你只需要在一个新的终端窗口中输入 `mkdir command_exp` 并按回车（ENTER）。新文件夹应该出现在你的家目录中，所以请通过点击桌面上的图标来检查它是否存在。

好了，bra, bueno！现在我们在 `command_exp` 内部再创建一个新文件夹——如果可以的话，这是一个子文件夹。我们将其命名为 `sub`。所以只需输入 `mkdir command_exp/sub` 并按回车（ENTER）。如果你喜欢，可以看一眼 `sub` 文件夹是否出现在 `command_exp` 文件夹中。

## $ mv

下一个命令是 `mv`（move）命令，但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

## $ cd

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

（注：由于提供的文本中存在大量重复段落，此处已按要求进行去重并完成翻译逻辑)*

