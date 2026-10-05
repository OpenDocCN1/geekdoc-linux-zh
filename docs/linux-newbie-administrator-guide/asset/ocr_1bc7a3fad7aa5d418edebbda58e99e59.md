# 3.3 Job scheduling with "at", "batch", and cron

3.3.1 How do I execute a command at a specific time (using "at"or "batch")? [p 46]
3.3.2 How do I set up cron? [p 47]

# 3.4 Swap space [p 48]

3.4.1 Swap partitions [p 49]
3.4.2 Swap files [p 49]

# 3.5 Shell

3.5.1 What's a shell and do I want an to use a different one? [p 50]
3.5.2 How do I write a simple shell script? [p 51]

# 3.6 Simple programming

3.6.1 How do I write a simple Python program? [p 52]
3.6.2 How do I write a simple GUI program (using tcl)? [p 52]
3.6.3 How do I write a simple perl script? [p 53]
3.6.4 How do I compile a simple C program? [p 54]

# 3.7 How do I install a program downloaded from the Internet? [p 54]

# Basic Operations FAQ

# 3.1 Basics

# 3.1.1 Filenames

Linux is case-sensitive. For example: my_fileE, my_file, and my_FILE are three different files. Your username and password login are case-sensitive (This follows the tradition since both UNIX and "c" programming language are case-sensitive). Naming conventions for files and directories are identical.

Filenames under Linux can be up to 256 characters long and they normally contain letters, numbers, ". (dots), underscores and "" (dashes). Other characters are possible but not recommended. In particular, it is not recommended to use special metacharacters: "*" (asterisk), "?" (question mark), " " (space), \$ (dollar sign), & (ampersand), any brackets, etc. This is because metacharacters have special meaning to the Linux shell. It is possible to have space inside the filename, but we don't recommend it either--use underscore instead.

It is not possible all to have '/' (slash) as a part of the filename because '/' is used to represent the top of the directory tree, and as a separator in the pathnames (as the same as \ is in DOS).