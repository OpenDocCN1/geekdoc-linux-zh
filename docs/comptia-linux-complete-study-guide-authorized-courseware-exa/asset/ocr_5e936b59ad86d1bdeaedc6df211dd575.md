**Search recursively** The -r or --recursive option searches in the specified directory and all subdirectories rather than simply the specified directory. You can use rgrep rather than specify this option.

**Use an extended regular expression** The grep command interprets regexp as a basic regular expression by default. To use an extended regular expression, you can pass the -E or --extended-regexp option. Alternatively, you can call egrep rather than grep; this variant command uses extended regular expressions by default.

A simple example of grep uses a regular expression with no special components:

```
$ grep -r eth0 /etc/*
```

This example finds all the files in /etc that contain the string eth0 (the identifier for the first Ethernet device). Because the example includes the -r option, it searches recursively, so files in subdirectories of /etc are examined as well as those in /etc itself. For each matching text file, the line that contains the string is printed.

![](bbox=[0.14, 0.41, 0.25, 0.49])

> Some files in /etc can’t be read by ordinary users. Thus, if you type this command as a non-root user, you’ll see some error messages relating to grep’s inability to open files.

Ramping up a bit, suppose you want to locate all the files in /etc that contain the string eth0 or eth1. You can enter the following command, which uses a bracket expression to specify both variant devices:

```
$ grep eth[01] /etc/*
```

A still more complex example searches all files in /etc that contain the hostname twain.example.com or bronto.pangaee.edu and, later on the same line, the number 127. This task requires using several of the regular expression features. Expressed using extended regular expression notation, the command looks like this:

```
$ grep -E "(twain\.example\.com|bronto\.pangaee\.edu)\.[12]7" /etc/*
```

This command illustrates another feature you may need to use: shell quoting. Because the shell uses certain characters, such as the vertical bar and the asterisk, for its own purposes, you must enclose certain regular expressions in quotes lest the shell attempt to parse the regular expression as shell commands.

You can use grep in conjunction with commands that produce a lot of output in order to sift through that output for the material that’s important to you. (Several examples throughout this book use this technique.) For example, suppose you want to find the process ID (PID) of a running xterm. You can use a pipe to send the result of a ps command (described in Chapter 2) through grep:

```
# ps ax | grep xterm
```