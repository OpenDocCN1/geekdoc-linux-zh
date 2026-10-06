# Chapter 3 Tools of the Trade

To sort the file instead by the third colon-delimited file (which contains what is known as your user ID), you would want an arithmetic sort, with the third field (-k3), and specifying the colon character as the field delimiter (-t :):

```
$ sort -k3 -t : /etc/passwd
root:x:0:The Super User:/usr/bin/ksh
cron::1:1:Cron Daemon for periodic tasks::/
bin::3:3:The system of files::/
uucp::5:5:/usr/spool/uucpublic:/lib/uucp/uucico
as*:6:6:The Owner of Assignable Devices::/
sysinfo*:10:10:Access to System Information::/usr/bin/sh
george*:75:75:/users/george:/usr/bin/sh
steve*:203:300:/users/steve:/usr/bin/ksh\mail*:301::/usr/mail::
```

Here we've bolded the third field of each class so that you can easily verify that the file sorted correctly by user ID.

# Other Options

Other options to sort enable you to skip characters in a field, specify the field to end the sort on, merged input files, and in “dictionary order” (only letters, numbers, and spaces are used for the comparison). For more details on these options, look under sort in your Unix User's Manual.

# uniq

The uniq command is used when you need to find or remove duplicate lines in a file.
The basic format of the command is

```
uniq in_file out_file
```

In this format, uniq copies in_file to out_file, removing any duplicate lines in the process. uniq's definition of duplicated lines is consecutive lines that match exactly.

If out_file is not specified, the results will be written to standard output. If in_file is also not specified, uniq acts as a filter and reads its input from standard input.

Here are some examples to see how uniq works. Suppose that you have a file called names with contents as:

```
$ cat names
Charlie
Tony
Emanuel
Lucy
```