
# 66 | Master of Linux Commands

phrase is added from the last line in the file. Let us explain what we mean with some examples.

```
root@kemal:~/zeyno# touch test-2
root@kemal:~/zeyno# ls
test test-1 test-2
root@kemal:~/zeyno# cat > test-2
Ali
Veli
root@kemal:~/zeyno# cat test-2
Ali
Veli
root@kemal:~/zeyno# >> test-2
Ayşe
Fatma
root@kemal:~/zeyno# cat test-2
Ali
Veli
Ayşe
Fatma
root@kemal:~/zeyno# cat > test-2
111
222
root@kemal:~/zeyno# cat test-2
111
222
```

Let us explain what we are doing:

- *touch test-2* we create a new text file.
- *cat > test-2* we gave the command, and then type the expressions we want and finished with Ctrl + D.
- *cat test-2* we look at the file content.
- *cat >> test-2* we've written some new expressions and we finished with the file CTRL + D.

- *cat test-2* We saw what we type last is added to the file content.
- *cat > test-2* (Please note that we use > only once) we add our new content in our file.
- *cat test-2* When we checked again with the content of our files, we found that the old content is deleted and the content we enter the final written.

We learn that we can read the file content with cat command. If we use cat command with -A the tab in the text shows spaces with ^, and shows ends of the line with $.

```
root@kemal:~/zeyno# cat >> test
Debian Whezy
root@kemal:~/zeyno# cat -A test
Kali Linux 2.0 (Kali Sana)
^IDebian^IWhezy$
root@kemal:~/zeyno# _
```

To change lowercase letters to uppercase letters in a text file that we want to see the contents or to do the opposite, we can use cat and tr command together. For example, to change lowercase letters to uppercase letters in test file, we can use cat test | tr 'a-z' 'A-Z'.

```
root@kemal:~/zeyno# cat test
Kali Linux 2.0 (Kali Sana)
Debian Whezy
root@kemal:~/zeyno# cat test | tr 'a-z' 'A-Z'
KALI LINUX 2.0 (KALI SANA)
DEBIAN WHEEZY
root@kemal:~/zeyno# _
```

# 68 | Master of Linux Commands

Here, I want to talk briefly about that we will use again in time, about | sign in and piping (pipe). As seen in the example above, with the pipe transaction a output command is given as input command. When we examine the example, reading the contents of test file is given as input to tr command and tr command in accordance with the parameters used in the file content with its trade. Piping process is made by "|". Yes, let us keep to our examples.

We talked about that we can read the contents of the text file with cat command to the terminal. Now, for example, with the passwd file content with cat /etc/passwd command

```
root@kemal:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/usr/sbin/nologin
sys:x:3:3:dev:/usr/sbin/nologin
sync:x:4:6534:sync:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
```

The file content shown as it is. If we want to see the content with the rows, we must use cat -n /etc/passwd command.

```
root@kemal:~$ cat -n /etc/passwd
1 root:x:0:0:root:/root:/bin/bash
2 demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
3 bin:x:2:2:bin:/usr/sbin/nologin
4 sysys:x:3:3:dev:/usr/sbin/nologin
5 sync:x:4:6534:sync:/bin/sync
6 games:x:5:60:games:/usr/games:/usr/sbin/nologin
7 lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
8 mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
9 news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
10 uuc:x:10:10:uuc:/bin:/usr/sbin/nologin
11 proxy:x:12:13:proxy:/bin:/usr/sbin/nologin
12 www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
13 backup:x:34:34:backup:/var/backup:/usr/sbin/nologin
14 list:x:38:38:Mailing List:/var/list:/usr/sbin/nologin
15 irc:x:39:39:irc:/var/run/irc:/usr/sbin/nologin
```

# Echo

Normally with this command, any desired statements sent as output to the terminal screen. Besides this can be used to create a file and write any string into it. Now let's create a new file as well as we want to write into the file using the echo command.

```
root@kemal:~/zeyo# echo "master of linux" > linuxcmd
root@kemal:~/zeyo# ls
linuxcmd test-1 test-2
root@kemal:~/zeyo# cat linuxcmd
master of linux
```

As you see with echo "master of linux" > linuxcmd file, we created linuxcmd that did not exist before. Previously an empty file can be written in this way. But if the file is not empty, we can use >> operator as we did before

```
root@kemal:~/zeyno# cat linuxcmd
master of linux
root@kemal:~/zeyno# echo "forever linux" >> linuxcmd
root@kemal:~/zeyno# cat linuxcmd
master of linux
forever linux
```

Using operators command output redirection could lead to a file. By the way, let's also do a small example of this. For example, lets ls -l output to list that we create. Which means the contents of the command output is written in the file named list. To do this, use the ls -l command is sufficient.

# 70 | Master of Linux Commands

```
root@kemal:~/zeyo# ls -l > list
root@kemal:~/zeyo# cat list
-rw-r-- 1 root root 30 Jan 58 linuxcmd
-rw-r-- 1 root root 0 Jan 04 list
-rw-r-- 1 root root 42 Jun 34 test
-rw-r-- 1 root root 26 Jun 56 test-1
-rw-r-- 1 root root 8 Jun 23 test-2
root@kemal:~/zeyo#
```

Now let's give an example about how we use echo command in another way and have additional information. First, let's look at the contents of the directory with the ls command that we were in, and then use the echo command, let's check if the output is the same in both commands.

```
root@kemal:~/zeyo# ls
list test-1 test-2
root@kemal:~/zeyo# echo *
list test-1 test-2
```

As you can see the output of the two commands are the same. The reason is that, before starting the echo command shell, with * character and in /zeyo directory all file names to the command line get, and give them as each to parameters. This means, with fact that echo * command screen (*) character was supposed to pop up, but it was not. So that means asterisk character is not sent as a parameter to echo.

```
root@kemal:~/zeyo# echo "linux commands"
linux commands
root@kemal:~/zeyo# echo *
linuxcmd list test-1 test-2
```

After this little reminder, let us continue with our other examples. To print file names starting with t capital from the directory we are in, we can use the echo t* command.

```
root@kemal:~/zeyno# echo t*
test test-1 test-2
```

If you want to list the files with the last letter of d in the names, you can use the echo *d command.

```
root@kemal:~/zeyno# ls
list test-1 test-2
root@kemal:~/zeyno# echo *d
list
```

By examining the following example, find out why that is. For your homework:

```
root@kemal:~# echo /usr/*/share
/usr/local/share
root@kemal:~# echo Number{1..5}

Number_1 Number_2 Number_3 Number_4 Number_5
root@kemal:~# echo {Z,A}
Z Y X W V U T S R P O N L K J I H G F E D C B A
root@kemal:~# echo a{A{1,2},B{3}}b
a1b a2b a3b a4b
```

When using the terminal command, if there is a phrase in this statement between reverse quotes ('') it is perceived as a string by the shell. As an example, when echo ls command is given, naturally ls (string) is printed on the screen. However, if you use the command as echo 'ls', then the ls output is printed on the screen and therefore the command output.

# 72 | Master of Linux Commands

```
root@kemal:~# echo ls
ls
root@kemal:~# echo `ls`
```

# More

To read files from the terminal, more is longer than the output. For example, when we give /etc/passwd, the output appears on the screen with pressing space key to scroll by page. To return to the previous page, the b key is used. When we want to exit, we can press q

