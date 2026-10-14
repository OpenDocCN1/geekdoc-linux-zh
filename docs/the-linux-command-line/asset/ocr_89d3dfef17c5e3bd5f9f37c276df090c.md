|  |  |  |
|---|---|---|
|  |  | rather than alphabetic values. |
| -r | --reverse | Sort in reverse order. Results are in descending rather than ascending order. |
| -k | --key=field1[,field2] | Sort based on a key field located from field1 to field2 rather than the entire line. See discussion below. |
| -m | --merge | Treat each each argument as the name of a presorted file. Merge multiple files into a single sorted result without performing any additional sorting. |
| -o | --output=file | Send sorted output to file rather than standard output. |
| -t | --field-separator=char | Define the field separator character. By default fields are separated by spaces or tabs. |

Although most of the options above are pretty self-explanatory, some are not. First, let’s look at the -n option, used for numeric sorting. With this option, it is possible to sort values based on numeric values. We can demonstrate this by sorting the results of the du command to determine the largest users of disk space. Normally, the du command lists the results of a summary in pathname order:

```
[me@linuxbox ~]$ du -s /usr/share/* | head
252	/usr/share/aclocal
96	/usr/share/acpi-support
8	/usr/share/adduser
196	/usr/share/alacarte
344	/usr/share/alsa
8	/usr/share/alsa-base
12488	/usr/share/anthy
8	/usr/share/apmd
21440	/usr/share/app-install
48	/usr/share/application-registry
```

In this example, we pipe the results into head to limit the results to the first ten lines. We can produce a numerically sorted list to show the ten largest consumers of space this way: