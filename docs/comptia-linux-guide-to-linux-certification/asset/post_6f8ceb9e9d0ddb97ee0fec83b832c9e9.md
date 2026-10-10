
## Chapter 7 Working with the BASH Shell

From Ancient grudge break to new mutiny,
From forth the fatal loins of these two foes
In fair Verona, where we lay our scene,
Is now the two hours' traffic of our stage;
The fearful passage of their death-mark'd love,
Which if you with patient ears attend,
Two households, both alike in dignity,
What here shall miss, our toil shall strive to mend.
Where civil blood makes civil hands unclean.
Which, but their children's end, nought could remove,
Whole misadventured piteous overthrows

```bash
[root@server1 ~]# cat newfile
2015-08-20 08:06
A pair of star-cross'd lovers take their life;
And the continuance of their parents' rage.
Do with their death bury their parents' strife.
From Ancient grudge break to new mutiny,
From forth the fatal loins of these two foes
In fair Verona, where we lay our scene,
Is now the two hours' traffic of our stage;
The fearful passage of their death-mark'd love,
Which if you with patient ears attend,
Two households, both alike in dignity,
What here shall miss, our toil shall strive to mend.
Where civil blood makes civil hands unclean.
Which, but their children's end, nought could remove,
Whole misadventured piteous overthrows
[root@server1 ~]#
```

You can also combine redirection and piping, as long as input redirection occurs at the beginning of the pipe and output redirection occurs at the end of the pipe. An example of this is shown in the following output, which replaces all lowercase a characters with uppercase A characters in the prologue file used in the previous example, then sorts the file, numbers each line, and saves the output to a file called newprologue instead of sending the output to the terminal screen.

```bash
[root@server1 ~]# tr a A <prologue | sort | nl >newprologue
[root@server1 ~]# cat newprologue
1 A pair of star-cross'd lovers take their life;
2 And the continuance of their parents' rage,
3 Do with their death bury their parents' strife.
4 From Ancient grudge break to new mutiny,
5 From forth the fatal loins of these two foes
6 In fair Verona, where we lay our scene,
7 Is now the two hours' traffic of our stage;
8 The fearful passage of their death-mark'd love,
9 Which if you with patient ears attend,
10 Two households, both alike in dignity,
11 What here shall miss, our toil shall strive to mend.
12 Where civil blood makes civil hands unclean.
13 Which, but their children’s end, nought could remove,
14 Whole misadventured piteous overthrows
[root@server1 ~]#
```

## Command Input and Output

Many Linux commands can be used to provide large amounts of useful text information. As a result, Linux administrators often use the sed and awk filter commands in conjunction with pipes to manipulate text information obtained from these commands.

The sed command is typically used to search for a certain string of text, and replaces that text string with another text string using the syntax `s/search/replace/`. For example, the following output demonstrates how sed can be used to search for the string “the” and replace it with the string “THE” in the prologue file used earlier:

```bash
[root@server1 ~]# cat prologue | sed s/the/THE/
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of these two foes
A pair of star-cross'd lovers take THEIR life;
Whose misadventured piteous overthrows
Do with THEIR death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And THE continuance of their parents' rage,
Which, but THEIR children’s end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]#
```

Notice from the preceding output that sed only searched for and replaced the first occurrence of the string “the” in each line. To have sed globally replace all occurrences of the string “the” in each line, simply append a g to the search-and-replace expression:

```bash
[root@server1 ~]# cat prologue | sed s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of THESE two foes
A pair of star-cross'd lovers TAKE THEIR life;
Whose misadventured piteous overthrows
Do with THEIR death bury THEIR parents' strife.
And THE continuance of THEIR parents' rage,
Which, but THEIR children’s end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]#
```

You can also tell sed the specific lines to search by prefixing the search-and-replace expression. For example, to force sed to replace the string “the” with “THE” globally on lines that contain the string “love,” you can use the following command:

```bash
[root@server1 ~]# cat prologue | sed /love/s//the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with their death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]#
```

You can also force sed to perform a search-and-replace on certain lines only. To replace the string “the” with “THE” globally on lines 5 to 8, you can use the following command:

```bash
[root@server1 ~]# cat prologue | sed 5,8s//the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of THESE two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with THEIR death bury THEIR parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]#
```

You can also use sed to remove unwanted lines of text. To delete all the lines that contain the word “the,” you can use the following command:

```bash
[root@server1 ~]# cat prologue | sed /the/d
Whole misadventured piteous overthrows
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]#
```

Like sed, the awk command searches for patterns of text and performs some action on the text found. However, the awk command treats each line of text as a record in a database, and each word in a line as a database field. For example, the line “Hello, how are you?” has four fields: “Hello,” “how,” “are,” and “you?”. These fields can be referenced in the awk command using $1, $2, $3, and $4. For example, to display only the first and fourth words only on lines of the prologue file that contains the word “the,” you can use the following command:

```bash
[root@server1 ~]# cat prologue | awk '/the/ {print $1, $4}'
From fatal
A star-cross'd
Do death
The of
And of
Which, children's
Is two
[root@server1 ~]#
```

By default, the awk command uses space or tab characters as delimiters for each field in a line. Most configuration files on Linux systems, however, are delimited using colon (:) characters. To change the delimiter that awk uses, you can specify the -F option to the command. For example, the following example lists the last 10 lines of the colon-delimited file /etc/passwd and views only the 6th and 7th fields for lines that contain the word “bob” in the last 10 lines of the file:

```bash
[root@server1 ~]# tail /etc/passwd
news:x:9:13:News server user:/etc/news:/sbin/nologin
smolt:x:490:474:Smolt:/usr/share/smolt:/sbin/nologin
backuppc:x:489:473::/var/lib/BackupPC:/sbin/nologin
pulse:x:488:472:PulseAudio System Daemon:/var/run/pulse:/sbin/nologin
gdm:x:42:468::/var/lib/gdm:/sbin/nologin
hsqldb:x:96:96::/var/lib/hsqldb:/bin/login
jetty:x:487:467::/usr/share/jetty:/bin/sh
bozo:x:500:500:bozo the clown:/home/bozo:/bin/bash
bob:x:501:501:Bob Smith:/home/bob:/bin/bash
user1:x:502:502:sample user one:/home/user1:/bin/bash
[root@server1 ~]# tail /etc/passwd | awk -F : '/bob/ {print $6, $7}'
/home/bob /bin/bash
[root@server1 ~]#
```

![Both awk and sed allow you to specify regular expressions in the search pattern.](img/c27875544958897d817484d558c208c8_340_0.png)
