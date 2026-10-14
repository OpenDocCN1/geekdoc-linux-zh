
As we can see, local variables are defined by preceding the variable name with the word local. This creates a variable that is local to the shell function in which it is defined. Once outside the shell function, the variable no longer exists. When we run this script, we see these results:

```
[me@linuxbox ~]$ local-vars
global:  foo = 0
funct_1:  foo = 1
global:  foo = 0
funct_2:  foo = 2
global:  foo = 0
```

We see that the assignment of values to the local variable foo within both shell functions has no effect on the value of foo defined outside the functions.

This feature allows shell functions to be written so that they remain independent of each other and of the script in which they appear. This is valuable because it helps prevent one part of a program from interfering with another. It also allows shell functions to be written so that they can be portable. That is, they may be cut and pasted from script to script, as needed.

## Keep Scripts Running

While developing our program, it is useful to keep the program in a runnable state. By doing this, and testing frequently, we can detect errors early in the development process. This will make debugging problems much easier. For example, if we run the program, make a small change, then run the program again and find a problem, it's likely that the most recent change is the source of the problem. By adding the empty functions, called stubs in programmer-speak, we can verify the logical flow of our program at an early stage. When constructing a stub, it's a good idea to include something that provides feedback to the programmer, which shows the logical flow is being carried out. If we look at the output of our script now:

```
[me@linuxbox ~]$ sys_info_page
<html>
```

```
<head>
    <title>System Information Report For twin2</title>
</head>
<body>
    <h1>System Information Report For linuxbox</h1>
    <p>Generated 03/19/2018 04:02:10 PM EDT, by me</p>
</body>
</html>
```

we see that there are some blank lines in our output after the timestamp, but we can’t be sure of the cause. If we change the functions to include some feedback:

```
report_uptime () {
    echo "Function report_uptime executed."
    return
}

report_disk_space () {
    echo "Function report_disk_space executed."
    return
}

report_home_space () {
    echo "Function report_home_space executed."
    return
}
```

and run the script again:

```
[me@linuxbox ~]$ sys_info_page
<html>
    <head>
        <title>System Information Report For linuxbox</title>
    </head>
    <body>
        <h1>System Information Report For linuxbox</h1>
        <p>Generated 03/20/2018 05:17:26 AM EDT, by me</p>
        Function report_uptime executed.
        Function report_disk_space executed.
        Function report_home_space executed.
    </body>
</html>
```

we now see that, in fact, our three functions are being executed.

With our function framework in place and working, it's time to flesh out some of the function code. First, here's the report_uptime function:

```
report_uptime () {
    cat <<- _EOF_
        <h2>System Uptime</h2>
        <pre>$(uptime)</pre>
    _EOF_
    return
}
```

It's pretty straightforward. We use a here document to output a section header and the output of the uptime command, surrounded by <pre> tags to preserve the formatting of the command. The report_disk_space function is similar.

```
report_disk_space () {
    cat <<- _EOF_
        <h2>Disk Space Utilization</h2>
        <pre>$(df -h)</pre>
    _EOF_
    return
}
```

This function uses the df -h command to determine the amount of disk space. Lastly, we'll build the report_home_space function.

```
report_home_space () {
    cat <<- _EOF_
        <h2>Home Space Utilization</h2>
        <pre>$(du -sh /home/*)</pre>
    _EOF_
    return
}
```

We use the du command with the -sh options to perform this task. This, however, is not a complete solution to the problem. While it will work on some systems (Ubuntu, for example), it will not work on others. The reason is that many systems set the permissions of home directories to prevent them from being world-readable, which is a reasonable security measure. On these systems, the report_home_space
