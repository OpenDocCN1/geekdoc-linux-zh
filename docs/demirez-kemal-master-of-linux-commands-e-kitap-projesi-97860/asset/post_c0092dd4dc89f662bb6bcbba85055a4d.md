
# Less

Once again, to read the contents of a file, another command you can use is less command. With this command as the more command we display output with long files to easy to read. Using the up and down arrow keys to scroll through the pages. With space key, goes to next page, with b key goes to the previous page. To exit q key used is same as we mentioned before.

# Head-Tail

While viewing the file contents to see the first ten rows head command, to view the last ten rows tail command is used. The use of these parameters is the case if you want to see a certain number of rows you must specify them with -n parameter. For example, to see the first five lines head -n 5, see the last five lines tail -n command can be used.

```
root@kemal:~# head -n 5 /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/sbin/nologin
bin:x:2:2:bin:/usr/sbin:/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:6:6534:sync:/bin/sync
root@kemal:~# tail -n 5 /etc/passwd
saned:x:129:139:/var/lib:/bin/false
usbmux:x:130:46:usbm:/var/lib/usbm:/bin/false
xfss:x:131:140:/var/lib/xfss:/bin/false
debum:x:132:142:Gnome Display Manager:/var/lib/gdm3:/bin/false
zeynep:x:1000:1001:/home/zeynep:/bin/bash
root@kemal:~#
```

# Tee

To print expressions both standard output (ie, terminal/console) and you want to write to a file specified as well, you must use the tee command. If the file does not exist, it will be created and written into. When the writing is finished, exit Ctrl + D so you return to the command line.

```
root@kemal:~zeyno# tee hacker
Linux users
Linux users
Network
Network
Computer
Computer
root@kemal:~zeyno# ls
hacker linuxcmd list test test-1 test-2
root@kemal:~zeyno# cat hacker
Linux users
Network
Computer
root@kemal:~zeyno# _
```

As you can see, first it created the file named hacker hacker command, then gave out output we wrote expressions from the terminal as well as wrote to files.

# Tac

To view toward the beginning of the end of the contents of a text file, we can use the tac command.

```
root@kemal:~zeyno# cat hacker
Linux users
Network
Computer
root@kemal:~zeyno# tac hacker
Computer
Network
Linux users
root@kemal:~zeyno#
```

# Rev

As an interesting command is rev command, you can display each line on the screen reversed.

```
root@kemal:~/zeyno# cat hacker
Linux users
Network
Computer
root@kemal:~zeyno# rev hacker
sresu xunil
krowteN
retupmoC
root@kemal:~zeyno# _
```

# Sort

To reflect the Text file/document output to terminal in alphabetical order, the sort command is used. If it is used as sort -r, reflects in reverse alphabetical order.

```
root@kemal:~zeyno# sort hacker
Computer
Linux users
Network
root@kemal:~zeyno# sort -r hacker
Network
Linux users
Computer
root@kemal:~zeyno# _
```

# We

In a file line, character or the number of words you're wondering, you can use wc (wordcount) command. With -l the line, with -c the character and with -w parameter, the number of words can be learned. If you use without parameters as as wc, it shows all.

```
root@kemal:~/zeyno# wc hacker
3 49 hacker
root@kemal:~/zeyno# _
```

# nl

Previously, numbering the printing process we did it with cat -n lines, we can also do it with nl command. For example, in the context of hacker file to enumerate rows, nl hacker command is used.

```
root@kemal:~/zeyno# cat hacker
Linux users
Network
Computer
root@kemal:~/zeyno# nl hacker
1 Linux users
2 Network
3 Computer
root@kemal:~/zeyno# _
```

Content with a text file in a long line as enumerate as well as to see a few lines at the beginning, nl [TextFile] | head -n [number] command can be used

```
root@kemal:~/zeyno# nl hacker | head -n 2
1 Linux users
2 Network
root@kemal:~/zeyno# _
```

Similarly, to list a few lines from the end, tail command is used instead of head.

# Pr

To divide the contents of the page document, we use the pr command. For example, to view a file called list and divide the content of our page, we can use pr command. Therefore, if you print it, you will get a smoother output.

```
root@kemal:~# pr list
2015-10-07 14:39 Sayfa 1 toplam 120
dwxr-rx-x 22 4096 7 14:39 ..
dwxr-rx-x 22 4096 22 11:18 ..
dwxr------ 1 4096 25 20:07 .aptitude
-rw-r-- 1 5095 6 22:01 .bash_history
-rw-r-- 1 3391 21 11:06 .bashrc
dwxr-rx-x 2 4096 22 10:10 Belziger
dwxr------ 2 4096 13 00:56 .cache
dwxr-xr-x 3 4096 17 02:58 config
2015-10-07 14:39 Sayfa 2
px:x:108:114::/home/ntp:/bin/false
stunnel:x:109:116::/run/tunnel4:/bin/false
uuid:x:110:117::/run/uuid:/bin/false
Debian-exim:x:111:118::/spool/exim4:/bin/false
statd:x:112:65534::/var/lib/nfs:/bin/false
```

# Paste

To placing the base between two or more file opposite columns, paste command is use. For example, has two files named as LIST and LISTB mutually the lines by side contained in these files, paste LISTB is used.

```
root@kemal:~/zeyno# cat LISTA
Ahmet
Mehmet
Ali
Veli
Zeyno
root@kemal:~/zeyno# cat LISTB
12345
54345
98768
76567
89087
root@kemal:~/zeyno# paste LISTB
Ahmet 12345
Mehmet 54345
Ali 98768
Veli 76567
Zeyno 89087
root@kemal:~/zeyno# _
```

If you want, you can combine the contents of these files and redirect to a new file. For example, when we use paste LISTB > LISTC command, the contents of two files side by side in mutual line at the same time creating a new file named LISTC will be saved into the file.

```
root@kemal:~/zeyno# paste LISTA LISTB > LISTC
root@kemal:~/zeyno# cat LISTC
Ahmet 12345
Mehmet 54345
Ali 98768
Veli 76567
Zeyno 89087
root@kemal:~/zeyno# _
```

# Grep

To search for an expression (string) in files or output of a command, we can use grep command. Before the example of our command, let's use some of the important parameters.

- -r: Reverses the behavior of the command line that does not contain the sought word.
- -i: Upper / lower case is not taken during a search.
- -n: Searches in the subdirectories of a given directory.
- -c: It displays the line number where the search word now.
- -l: The specified index indicates the number of times the word you are looking for.
- -l: Where appropriate template column lists file names.

Let's make a simple example. For example in /etc/passwd to list the zeynep, we can use either grep /etc/passwd or cat /etc/passwd | grep zeynep commands.

```
root@kemal:-# grep zeynep /etc/passwd
zeynep:x:1000:1001:/home/zeynep:/bin/bash
root@kemal:-# /etc/passwd | grep zeynep
zeynep:x:1000:1001:/home/zeynep:/bin/bash
root@kemal:-#
```

Now Let's cat LIST |grep -ni ali command. With this command: in LISTC file, upper / lower case without distinction, (-l) in expression lines, line number (n), we have also shown together.

```
root@kemal:~/zeyep# cat LISTC | grep -ni ali
3:Ali 98768
root@kemal:~/zeyep# _
```

Another example, let us examine grep -ri zeyno command. With this command, the zeyno directory as recursive (ie, including subdirectories), upper / lowercase distinction without parents expression of the files, we list lines that have vel expression. (because zeyno directory in the same directory, I used zeyno instead of /zeyno)

```
root@kemal:~# grep -ri veli zeyno
zyno/LISTA:Veli
zyno/LISTC:Veli      76567
root@kemal:~# _
```

The following example, grep -c Ali zeyno/LIST command, the LIST file under the zeyno directory, we want to learn how many times Ali stated (with -c parameter)

```
root@kemal:~# grep -c Ali LISTA/LIST
1
root@kemal:~# _
```

The last example that we have about this command, we listed the files containing the line through which we seek expression in the following example.

```
root@kemal:~# grep -l Ali zeyno/
LISTA
LISTC
root@kemal:~# _
```

# Cut

In the file we want to examine, to see some lines on specific areas, we use cut command. For example, to list the 1st and 7th field with /etc/passwd line of the file, we can use cut -d: f 1,7 /etc/passwd command.
