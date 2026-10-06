```
/usr/games/fortune
$
```

This example also demonstrates that, if the command is a built-in shell command, the hash command will identify it as such.

# The lc command

The lc command is a cute utility that can save you some typing on the command line. it stands for last command, and its job is to execute the last command that you ran on the command line, including any command line arguments. Here's a few examples of using the lc command:

```
$pwd
/home/rich/test
$ lc
/home/rich/test
$ ../test1
Your HOME directory exists
$ lc
Your HOME directory exists
$ ls -al
total 148
drw-xr-x 2 rich rich 4096 Jan 7 08:15
drw-xr-x 17 rich rich 4096 Jan 3 10:03 ..
-rwxr-r-- 1 rich rich 97 Jan 3 10:04 test1
-rwxr-r-- 1 rich rich 84 Jan 7 08:01 test2
$ lc
total 148
drw-xr-x 2 rich rich 4096 Jan 7 08:15
drw-xr-x 17 rich rich 4096 Jan 3 10:03 ..
-rwxr-r-- 1 rich rich 97 Jan 3 10:04 test1
-rwxr-r-- 1 rich rich 84 Jan 7 08:01 test2
$
```

The lc command works no matter the last command, whether it a built-in shell command, an application program, or a shell script. As you can see from the example, the lc command duplicates any command line arguments you supplied the original command.

# The ash shell files

Like the bash shell, the ash shell uses default files to control its start environment. The default files allow you to define shell environment variables and settings when using the ash shell in an interactive mode.

There are three files that ash shell uses:

+   - The /etc/profile file
- The $HOME/.profile file
- A file defined in the ENV environment variable