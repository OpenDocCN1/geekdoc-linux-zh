
要移动你刚刚创建的文件，你自然将使用 `mv` 命令，只需输入 `mv expfile.txt command_exp/sub`（这告诉系统要移动哪个文件以及移动到哪里）并按回车（ENTER）。该文件现在位于 `command_exp/sub` 中。

## `$ cd`

另一个命令是 `cd`（change directory，切换目录），但在你尝试它之前，你需要创建一个虚拟文件——毕竟你需要一些东西可以移动。你可以使用另一个命令——`touch` 来完成。为了创建一个文件——我们称之为 `expfile.txt`——进入终端，输入 `touch expfile.txt` 并按回车（ENTER）。新文件将出现在你的家目录中。

## `$ pwd`

If you know who you are but aren't exactly where you are, `pwd` (print working directory) should come in handy. The `pwd` command tells you exactly where the Terminal is in your directory tree.

Let's say, for example, that my Terminal is in my personal home directory (which is called `~`) in the system's home directory (which is called home and from which are all the user account directories are located). When I use the `pwd` command, I would get `/home/rg` printed to my Terminal. You should get similar results if you try it.

**NOTE** The *print*, in this case, has nothing to do with your printer; it merely means the response will be printed to, or displayed in, the *Terminal*.

## `$ df`

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
243caecaef4 rg@myndestkop:~$
```

Figure 8-4: Output from the df command with the -h flag

## `ls`

Another harmless but handy command is `ls` (list directory). The `ls` shows you what is in your current directory. This is the non-graphical equivalent of double-clicking a folder in Nautilus to see what is inside. Try by typing `ls` and then pressing the ENTER KEY.
