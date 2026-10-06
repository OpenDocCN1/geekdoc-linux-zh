# Chapter 3 Tools of the Trade

The option -c1-18- specifies "extract characters 1 through 8 (the username) and also characters 18 through the end of the line (the login time)."

# The -d and -f Options

The cut command with its -c flag is useful when you need to extract data from a file or command, provided that the file or command has a fixed format.

For example, you could use cut with the who command because you know that the usernames are always displayed in character positions 1–8, the terminal in 10–16, and the login time in 18–29. Unfortunately, not all data will be so well organized!

For instance, take a look at the /etc/passwd file:

```
$ cat /etc/passwd
root:0:0:The User:/usr/bin/ksh
cron*:1:1:Cron Daemon for periodic tasks:
bin*:3:3:The owner of system files:
uucp*:5:5:/usr/sbin:/usr/lib/uucp/uucico
asg*:6:6:The Owner of Assignable Devices:
steve*:20:100:/users/steve:/usr/bin/ksh
other*:4:4:Needed by secure program:
```

$ is the master file that contains the usernames of all users on your system. It also contains other information such as user ID, home directory, and the name of the program to start up when particular user logs in.

Quite clearly, the data in this file does not line up anywhere as neatly as the who’s output does. Extracting a list of all users from your system can be done using the -c option to cut.

Upon inspection of the file, it’s clear that fields are separated by a character. Each field may not be the same length from one line to the next, so you can "count columns" to get the same field from each line.
The -d and -f options are used with cut when you have data that is delimited by a particular character, with -d specifying the field delimiter and -f the fields you want to extract. The invocation of the cut command bema

```
cut -dchar -fields file
```

where char is the character that delimits each field of the data, and fields specifies the fields to be extracted from file. Fields start at 1, and the same type of formats are used to specify field numbers as used to specify character positions (for example, -f1,2,8, -f1-3, -f-4).

To extract the name of all users from /etc/passwd, you could use the following:

```
$ cut -d -f1 /etc/passwd
Extract field 1
root
cron
bin
```