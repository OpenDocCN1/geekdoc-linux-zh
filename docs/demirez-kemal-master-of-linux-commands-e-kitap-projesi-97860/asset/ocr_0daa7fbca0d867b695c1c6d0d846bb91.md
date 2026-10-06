After this little reminder, let us continue with our other examples. To print files names starting with t capital from the directory we are in, we can use the echo t* command.

```
root@kemal:~/zeyno# echo t*
test test-1 test-2
root@kemal:~/zeyno#
```

If you want to list the files with the last letter of d in the names, you can use the echo *d command.

```
root@kemal:~/zeyno# ls
luxcmd list test-1 test-2
root@kemal:~/zeyno# echo *d
luxcmd
root@kemal:~/zeyno#
```

By examining the following example, find out why that is. For your homework

```
root@kemal:~# echo /usr/*/share
/usr/local/share
root@kemal:~# echo Number{1..5}
Number_1 Number_2 Number_3 Number_4 Number_5
root@kemal:~# echo {Z,A}
Z Y X W V U T S R P O N L K J I H G F E D C B A Z
root@kemal:~# echo a{A{1,2},B{3}}b
a1b a2b a3b a4b
```

When using the terminal command, if there is a phrase in this statement between reverse quotes ('') it is perceived as a by the shell. As an example, when echo ls command is given, naturally ls (string) is printed on the screen. However, if you use the command as echo 'ls', then the ls sent to the terminal will be perceived as command by the shell, and rotating the command to print the expression on the display command output. (i.e. all strings in the output of the ls command will be given as a parameter to echo command, and therefore these statements to be printed to the screen as well)