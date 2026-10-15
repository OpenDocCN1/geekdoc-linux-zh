# EXAMPLE 9.77 (CONTINUED)

```
4 ps -eaf
5 history
6 more /etc/passwd
7 cd
8 echo $USER
9 set
10 ls
```

# EXPLANATION

+   1. The history variable is set to 10. Only the last 10 lines of the history list will be displayed, even if there are many more.
+   2. The last 10 events from the history are displayed. Each command is numbered.

# EXAMPLE 9.78

```
1 > history -h   # print without line numbers
ls
vi file1
df
ps -eaf
history
more /etc/passwd
cd
echo $USER
set
history -n
2 > history -c
```

# EXPLANATION

+   1. With the h option, the history list is displayed without line numbers.
+   2. With the c option, the history list is cleared.

# EXAMPLE 9.79

```
> history -r   # print the history list in reverse
11 history -r
10 history -h
9 set
8 echo $USER
7 cd
6 more /etc/passwd
5 history
4 ps -eaf
3 df
2 vi file1
1 ls
```