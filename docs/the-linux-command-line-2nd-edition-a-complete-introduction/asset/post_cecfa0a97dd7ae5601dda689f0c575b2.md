
keyboard:

```
[me@linuxbox ~]$ sort > foo.txt
c
b
a
[me@linuxbox ~]$ cat foo.txt
a
b
c
```

After entering the command, we type the letters "c", "b", and "a", followed once again by Ctrl-d to indicate end-of-file. We then view the resulting file and see that the lines now appear in sorted order.

Since sort can accept multiple files on the command line as arguments, it is possible to merge multiple files into a single sorted whole. For example, if we had three text files and wanted to combine them into a single sorted file, we could do something like this:

```
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

sort has several interesting options. Here is a partial list:

## Table 20-1: Common sort Options

| Option | Long Option | Description |
| -b | --ignore-leading-blanks | By default, sorting is performed on the entire line, starting with the first character in the line. This option causes sort to ignore leading spaces in lines and calculates sorting based on the first non-whitespace character on the line. |
| -f | --ignore-case | Makes sorting case-insensitive. |
| -n | --numeric-sort | Performs sorting based on the numeric evaluation of a string. Using this option allows sorting to be performed on numeric values rather than alphabetic values. |
| -r | --reverse | Sort in reverse order. Results are in descending rather than ascending order. |
| -k | --key=field1[,field2] | Sort based on a key field located from field1 to field2 rather than the entire line. See discussion below. |
| -m | --merge | Treat each argument as the name of a presorted file. Merge multiple files into a single sorted result without performing any additional sorting. |
| -o | --output=file | Send sorted output to file rather than standard output. |
| -t | --field-separator=char | Define the field-separator character. By default fields are separated by spaces or tabs. |

Although most of the options above are pretty self-explanatory, some are not. First, let’s look at the -n option, used for numeric sorting. With this option, it is possible to sort values based on numeric values. We can demonstrate this by sorting the results of the du command to determine the largest users of disk space. Normally, the du command lists the results of a summary in pathname order:

```
[me@linuxbox ~]$ du -s /usr/share/* | head
252       /usr/share/aclocal
96        /usr/share/acpi-support
8         /usr/share/adduser
196       /usr/share/alacarte
344       /usr/share/alsa
8         /usr/share/alsa-base
12488     /usr/share/anthy
8         /usr/share/apmd
21440     /usr/share/app-install
48        /usr/share/application-registry
```

In this example, we pipe the results into head to limit the results to the first ten lines. We can produce a numerically sorted list to show the ten largest consumers of space this way:

```
[me@linuxbox ~]$ du -s /usr/share/* | sort -nr | head
509940      /usr/share/locale-langpack
242660      /usr/share/doc
197560      /usr/share/fonts
179144      /usr/share/gnome
146764      /usr/share/myspell
144304      /usr/share/gimp
135880      /usr/share/dict
76508       /usr/share/icons
68072       /usr/share/apps
62844       /usr/share/foomatic
```

By using the -nr options, we produce a reverse numerical sort, with the largest values appearing first in the results. This sort works because the numerical values occur at the beginning of each line. But what if we want to sort a list based on some value found within the line? For example, the results of an ls -l:

```
[me@linuxbox ~]$ ls -l /usr/bin | head
total 152948
-rwxr-xr-x 1 root root     34824 2008-04-04 02:42 [
-rwxr-xr-x 1 root root    101556 2007-11-27 06:08 a2p
-rwxr-xr-x 1 root root     13036 2008-02-27 08:22 aconnect
-rwxr-xr-x 1 root root     10552 2007-08-15 10:34 acpi
-rwxr-xr-x 1 root root      3800 2008-04-14 03:51 acpi_fakekey
-rwxr-xr-x 1 root root     7536 2008-04-19 00:19 acpi_listen
-rwxr-xr-x 1 root root     3576 2008-04-29 07:57 addpart
-rwxr-xr-x 1 root root    20808 2008-01-03 18:02 addr2line
-rwxr-xr-x 1 root root    489704 2008-10-09 17:02 adept_batch
```

Ignoring, for the moment, that ls can sort its results by size, we could use sort to sort this list by file size, as well:

```
[me@linuxbox ~]$ ls -l /usr/bin | sort -nr -k 5 | head
-rwxr-xr-x 1 root root   8234216 2008-04-07 17:42 inkscape
-rwxr-xr-x 1 root root   8222692 2008-04-07 17:42 inksview
-rwxr-xr-x 1 root root   3746508 2008-03-07 23:45 gimp-2.4
-rwxr-xr-x 1 root root   3654020 2008-08-26 16:16 quanta
-rwxr-xr-x 1 root root   2928760 2008-09-10 14:31 gdbtui
-rwxr-xr-x 1 root root   2928756 2008-09-10 14:31 gdb
-rwxr-xr-x 1 root root   2602236 2008-10-10 12:56 net
-rwxr-xr-x 1 root root   2304684 2008-10-10 12:56 rpcclient
-rwxr-xr-x 1 root root   2241832 2008-04-04 05:56 aptitude
-rwxr-xr-x 1 root root   2202476 2008-10-10 12:56 smbacls
```
