# Searching for and Extracting Data

A simple example of grep uses a regular expression with no special components:

```
$ grep -r eth0 /etc/*
```

This example finds all the files in /etc that contain the string eth0 the identifier for the Ethernet device on most distributions. Because the example includes the -r option, it searches recursively, so grep searches in subdirectories of /etc as well as in /etc itself. For each matching text file, the line that contains the string is printed.

Suppose that you want to locate all the files in /etc that contain the string eth0 or eth1. You can enter the following command, which uses a bracket expression to specify both variants:

```
$ grep [01] /etc/*
```

A more complex example searches just the /etc/passwd file for lines that contain the word games or mail1, and later on the same line, the word login. This task requires extended regular expression notation; the demanded command looks like this:

```
$ grep -E "(games|mail).*.login" /etc/passwd
```

The preceding command illustrates another feature that you may need to use: shell quoting. Because the shell uses special characters, such as the vertical bar (/) and the asterisk (*), for its own purposes, you must enclose regular expressions in quotes. Otherwise, the shell will incorrectly treat the regular expression as shell commands.

You can use grep in conjunction with commands that produce a lot of output to sift through that output for the material that's important to you.(Several examples throughout this book use this technique). To accomplish this, you need to use input and output redirection. This topic is covered (with additional grep examples) in the upcoming section, "Redirecting Input and Output."

# Using find

The find utility implements a brute-force approach to finding files. This program finds files by searching through the specified directory tree, checking filenames, file dates, and so on to locate the files that match the specified criteria. Because of this operation, find tends to be slow. It's flexible, however, and likely to succeed, assuming that the file for which you are searching exists. To find it, type name optionally by a directory tree pathname (sometimes-called starting point) and a series of options, some of which use specifications similar to regular expressions.

![](bbox=[0.772, 0.073, 0.947, 0.163])

Ordinary users can't read some files in /etc. If you type this command as a non-root user, you'll see error messages relating to grep's inability to open files.

If you type this command on your computer, it may find no matches because of your configuration. Try other ways of finding games and mail, such as pulse rpc.

![](bbox=[0.772, 0.483, 0.947, 0.573])

Certification Objective

In find, you must use a directory tree or a search criterion with find, and often both.

![](bbox=[0.772, 0.853, 0.947, 0.943])

![](bbox=[0.052, 0.953, 0.947, 0.973])