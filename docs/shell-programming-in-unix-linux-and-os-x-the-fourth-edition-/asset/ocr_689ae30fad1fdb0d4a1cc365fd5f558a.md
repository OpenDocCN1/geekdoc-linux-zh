The option `-c1-8,18-` specifies “extract characters 1 through 8 (the username) and also characters 18 through the end of the line (the login time).”

# The `-d` and `-f` Options

The cut command with its -c flag is useful when you need to extract data from a file or command, provided that file or command has a fixed format.

For example, you could use cut with the who command because you know that the usernames are always displayed in character positions 1–8, terminal in 10–16, and the login time in 18–29. Unfortunately, not all your data will be so well organized!

For instance, take a look at the /etc/passwd file:

```
```text
$ cat /etc/passwd
root:*:0:0:The Super User:/:/usr/bin/ksh
cron:*:1:1:Cron Daemon For periodic tasks:/:
bin:*:3:3:The owner of system files:/
uucp:*:5:5::/usr/spool/uucp:/usr/lib/uucp/uucico
asg:*:6:6:The Owner of Assignable Devices:/
steve:*:203:100::/users/steve:/usr/bin/ksh
otcher:*:4:4:Needed by secure program:/
$
```
```

`/etc/passwd` is the master file that contains the usernames of all users on your computer system. It also contains other information such as user ID, home directory, and the name of the program to start up when that particular user logs in.

Quite clearly, the data in this file does not line up anywhere near as neatly as the who’s output does. Therefore extracting a list of all the users of your system from this file cannot be done using the -c option to cut.

Upon closer inspection of the file, however, it’s clear that fields are separated by a colon character. Although each field may not be the same length from one line to the next, you can “count colons” to get the same field from each line.

The -d and -f options are used with cut when you have data that is delimited by a particular character, with -d specifying the field separator delimiter and -f the field or fields you want extracted. The invocation of the cut command becomes

```
```text
cut -dchar -ffields file
```
```

where `dchar` is the character that delimits each field of the data, and `fields` specifies the fields to be extracted from `file`. Field numbers start at 1, and the same type of formats can be used to specify field numbers as was used to specify character positions before (for example, `-fl,2,8,-fl-3,-f4-`).

To extract the names of all users from `/etc/passwd`, you could type the following:

```
```text
$ cut -d: -f1 /etc/passwd              Extract field 1
root
cron
bin
```
```