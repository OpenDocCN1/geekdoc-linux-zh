
Throughout this book, you’ve been practicing running a single command. Unix doesn’t really care if you’re running a built-in command that came with the system, a program you installed later, or a script your best friend wrote—it’s all the same to Unix. Code Listing 9.1 shows some options on running a command.

## To run a command:

- `ls`

At the shell prompt, type the command and press Enter

## To run a specific command:

- `/home/jdoe/scripts/ls`

It’s certainly possible that you would want to write a script that would list the files in your directory in a special way—for example, a script to list the files and to save the listing into a new file for later reference. (You might name it something else but could certainly call it `ls` if you want to.) To run the specific script, enter the whole path to the script (so Unix doesn’t just run the first one it finds in your path). See Chapter 8 for more about path statements.

## Tips

- You can combine commands on the same line, as you’ve seen earlier in this book. Just use a `;` to separate the commands, and you’re set. For example, you could do `ls; pwd` to list files and show the current directory.

```
[jdoe@frazz Project]$ ls
keep keeper.jpg kept kidder.txt kiddo
+ kidnews kidneypie kids kidupdate
[jdoe@frazz Project]$ /bin/ls
keep keeper.jpg kept kidder.txt kiddo
+ kidnews kidneypie kids kidupdate
[jdoe@frazz Project]$ /home/jdoe/scripts/ls
keep keeper.jpg kept kidder.txt kiddo
+ kidnews kidneypie kids kidupdate
You listed these files.
[jdoe@frazz Project]$ ls ; pwd
keep keeper.jpg kept kidder.txt kiddo
+ kidnews kidneypie kids kidupdate
/home/jdoe/Project
[jdoe@frazz Project]$
```

Code Listing 9.1 To run a script, command, or program, just enter the name or the path and the name at the shell prompt.

- If you use a `&&` to combine commands, the system will run both in sequence but run the second only if the first succeeds. For example, you could use `mv todolist todolist.done && touch todolist` to move your to-do list to a different file and create a new to-do list. If the first command fails (for example, because you don’t have permission to create a new file), the second command won’t run.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_203_0.png)

**Figure 9.1** 要安排一次性任务，只需指定时间和要运行的任务即可。

## 使用 at 安排一次性任务

有时，你可能需要安排任务在指定的时间运行一次。例如，你可以安排一封发给自己的电子邮件，提醒你参加员工会议。或者，你可以为同事安排会议提醒，其中包含会议议程。你可以使用 `at` 来安排这些和其他一次性任务，`at` 让你指定任务（或任务）应运行的时间。**Figure 9.1** 演示了安排关于那次重要员工会议的电子邮件。

### 使用 at 安排一次性任务：

1. `at 12:01 1 Jan 2004`

    首先，使用 `at` 加上时间说明来指定你希望任务运行的时间（Figure 9.1）。在此示例中，我们指定了时间、月份、日期和年份，尽管你可以创建各种其他时间说明，例如：

    - `at noon tomorrow`
    - `at 01/01/99`
    - `at 3:42am`
    - `at now + 3 weeks`
    - `at teatime`

    是的，`teatime` 是一个有效选项。顺便说一下，它是下午 4 点。

2. `mail -s "Staff Meeting at 8:30am" ejr < /agenda`

    指定任务。在这种情况下，它向用户（`ejr`）发送电子邮件，指定主题为 "Staff Meeting at 8:30am"，并发送名为 `agenda` 的文件的内容。有关使用 `mail` 的完整信息，请参阅第 11 章。

3. `Ctrl D`

    表示你已完成发出命令。

### 使用 at 安排顺序一次性任务：

1. `at midnight`

    使用 `at` 加上时间说明来指定你希望顺序任务运行的时间（Code Listing 9.2）。你可以像前一个示例中所示使用各种时间说明。

2. `tar -icf ~/bigdog.tar ~/HereKittyKitty`

    输入你希望运行的第一个任务。此任务将目录 `~/HereKittyKitty` 中的所有文件收集到一个名为 `~/bigdog.tar` 的单个文件中。第 13 章将告诉你更多关于使用 `tar` 进行归档的信息。

3. `gzip ~/bigdog.tar`

    输入下一个要运行的任务。这会压缩 `~/bigdog.tar` 文件，使其更易于存储和发送电子邮件。

4. `mutt -a bigdog.tar.gz -s "Read this by lunch time!" deb < /dev/null`

    指定序列中的下一个任务。在这里，我们使用 `mutt` 的命令行邮件选项来附加文件、指定主题并将整个内容发送给 Deb。有关使用 `mutt` 发送电子邮件的更多信息，请参阅第 11 章。

5. `Ctrl D`

    Ta-daaaa！使用此键组合来完成序列。

```
[ejr@hobbes ejr]$ at midnight
at> tar -icf ~/bigdog.tar ~/HereKittyKitty
at> gzip ~/bigdog.tar
at> mutt -a bigdog.tar.gz -s "Read this by lunch time!" deb < /dev/null
at>
at> <EOT>
warning: commands will be executed using
 - /bin/sh
job 12 at 2003-08-28 00:00
[ejr@hobbes ejr]$
```

Code Listing 9.2 要安排顺序一次性任务，只需指定时间并按你希望它们运行的顺序列出任务即可。

### 删除已安排的任务：
