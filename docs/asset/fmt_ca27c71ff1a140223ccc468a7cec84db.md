
```
echo -e "What is your favorite color?--> \c"
read REPLY
if [ "$REPLY" = "red" -o "$REPLY" = "blue" ]
then
    echo "The answer is red or blue."
else
    echo "The answer is not red nor blue."
fi
```

如果用户执行程序并在提示时回答 `Blue`，会显示什么？

- a. The answer is red or blue.
- b. The answer is neither red nor blue.
- c. 代码将导致错误。
- d. The answer is red or blue. The answer is not red nor blue.

# 动手操作项目

这些项目应按照给定顺序完成。本章介绍的动手操作项目总共需要三小时完成。该实验的要求包括：

- 一台根据动手操作项目 2-2 安装了 `Fedora 13` 的计算机。

## 项目 7-1

在这个动手操作项目中，使用 `shell` 将 `stdout` 和 `stderr` 重定向到文件，并从文件获取 `stdin`。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，并使用 `root` 用户名和 `secret` 密码登录终端。
2. 在命令提示符下，输入 `touch sample1 sample2` 并按回车创建两个名为 `sample1` 和 `sample2` 的新文件。在命令提示符下输入 `ls -l` 验证它们的创建。
3. 在命令提示符下，输入 `ls sample2 sample3` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
4. 在命令提示符下，输入 `ls sample2 sample3 > file` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
5. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？
6. 在命令提示符下，输入 `ls sample1 sample2 sample3 > file` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
   ![](img/bafa5678973f896b93838a140b8f7840_362_0.png)
7. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？为什么保留了之前的内容？
8. 在命令提示符下，输入 `ls sample2 sample3 > file2` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
9. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？
10. 在命令提示符下，输入 `cat file2` 并按回车。`file2` 的内容是什么？
11. 在命令提示符下，输入 `ls sample2 sample3 >& file2` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
12. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？
13. 在命令提示符下，输入 `ls sample3 >& file2` 并按回车。屏幕上显示 `stdout` 吗？`stderr` 吗？
14. 在命令提示符下，输入 `cat file2` 并按回车。`file2` 的内容是什么？
15. 在命令提示符下，输入 `date > file` 并按回车。
16. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？
17. 在命令提示符下，输入 `date >> file` 并按回车。
18. 在命令提示符下，输入 `cat file` 并按回车。`file` 的内容是什么？你能看出每个 `date` 命令是什么运行的吗？
19. 在命令提示符下，输入 `date > /etc/hosts` 并按回车。你收到了什么错误消息？为什么？
20. 在命令提示符下，输入 `date > /etc/hosts` 并按回车。发生了什么？为什么？
21. 输入 `exit` 并按回车退出 `shell`。

## 项目 7-2

在这个动手操作项目中，你使用管道和重定向元字符重定向 `stdout` 和 `stdin`。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，并使用 `root` 用户名和 `secret` 密码登录终端。
2. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf` 并按回车查看配置。接下来在命令提示符下输入 `cat /etc/httpd/conf/httpd.conf | less` 并按回车逐页执行相同任务。解释上命令中 `|` 元字符的作用。这与 `less /etc/conf/httpd.conf` 命令有什么不同？
3. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep Keep` 并按回车。显示了多少行？为什么 `grep` 命令不需要指定文件名？
4. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep 2>&1` 并按回车。解释屏幕上的输出。
5. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep 2>&1 | sort -r` 并按回车。解释屏幕上的输出。
6. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep 2>&1 | sort -r | tee file` 并按回车。解释屏幕上的输出。接下来在命令提示符下输入 `cat file` 并按回车。内容是什么？`tee` 在上面的管道中起什么作用？
7. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep 2>&1 | sort -r | tee file | wc -l` 并按回车。解释屏幕上的输出。接下来在命令提示符下输入 `cat file` 并按回车。内容是什么？为什么？
8. 在命令提示符下，输入 `cat /etc/httpd/conf/httpd.conf | grep | sed #/d | sed /Max=/100/150` 并按回车。解释屏幕上的输出。可以使用 `grep` 和 `tr` 命令代替 `sed` 获取此输出吗？哪种更简单？
9. 在命令提示符下，输入 `cat /etc/hosts`。接下来输入 `cat /etc/hosts | awk '/localhost/ {print $1, $3}'` 并按回车。解释屏幕上的输出。
10. 输入 `exit` 并按回车退出 `shell`。

## 项目 7-3

在这个动手操作项目中，你创建并使用别名，查看并更改 `shell` 变量。此外，使用用户定义变量并在启动时自动加载变量。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，并使用 `root` 用户名和 `secret` 密码登录终端。
2. 在命令提示符下，输入 `set | less` 并按回车查看内存中加载的 `BASH` 环境变量。使用方向键滚动。完成后，按 `q` 退出 `less` 界面。
3. 在命令提示符下，输入 `env | less` 并按回车查看内存中加载的导出 `BASH` `shell` 变量。使用方向键滚动。这个列表比第 2 步生成的列表大还是小？为什么？完成后，按 `q` 退出 `less` 界面。
4. 在命令提示符下，输入 `PS1="Hello There:"` 并按回车。发生了什么？为什么？接下来在命令提示符下输入 `echo PS1` 并按回车验证 `PS1` 变量的新值。
5. 在命令提示符下，输入 `exit` 并按回车退出 `shell`。什么提示符你收到了吗？为什么？你如何能确保“Hello There;”提示在每次登录时都出现？
6. 在命令提示符下，输入 `vi .bash_profile` 并按回车。在文件底部添加以下行。完成后，保存并退出 `vi` 编辑器。

```
echo -e "Would you like a hello prompt? (y/n) -->\c"
read ANSWER
if [ $ANSWER = "y" ]
then
    PS1="Hello There: "
fi
```
