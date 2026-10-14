
| Shortcut Result |
|---|---|
| cd - | Changes the working directory to the previous working directory. |
| cd ~user_name | Changes the working directory to the home directory of user_name. For example, typing cd ~bob will change the directory to the home directory of user “bob.” |

## Summing Up

This chapter explained how the shell treats the directory structure of the system. We learned about absolute and relative pathnames and the basic commands that we use to move around that structure. In the next chapter, we will use this knowledge to go on a tour of a modern Linux system.

## 3

## EXPLORING THE SYSTEM

![](img/314a0280bc10c5c0d45be132de172677_49_0.png)

Now that we know how to move around the file system, it's time for a guided tour of our Linux system. Before we start, however, we're going to learn some more commands that will be useful along the way.

- **ls** List directory contents
- **file** Determine file type
- **less** View file contents

### More Fun with ls

The ls command is probably the most used command, and for good reason. With it, we can see directory contents and determine a variety of important file and directory attributes. As we have seen, we can simply enter ls to get a list of files and subdirectories contained in the current working directory.

```
[me@linuxbox ~]$ ls
Desktop  Documents  Music  Pictures  Public  Templates  Videos
```

Besides the current working directory, we can specify the directory to list, like so:

```
me@linuxbox ~]$ ls /usr
bin  games  include  lib  local  sbin  share  src
```

We can even specify multiple directories. In the following example, we list both the user’s home directory (symbolized by the ~ character) and the /usr directory:

```
[me@linuxbox ~]$ ls ~ /usr
/home/me:
Desktop  Documents  Music  Pictures  Public  Templates  Videos
/usr:
bin  games  include  lib  local  sbin  share  src
```

We can also change the format of the output to reveal more detail.

```
[me@linuxbox ~]$ ls -l
total 56
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Desktop
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Documents
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Music
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Pictures
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Public
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Templates
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Videos
```

By adding -l to the command, we changed the output to the long format.

### Options and Arguments

This brings us to a very important point about how most commands work. Commands are often followed by one or more *options* that modify their behavior and, further, by one or more *arguments*, the items upon which the command acts. So, most commands look kind of like this:

```
command -options arguments
```

Most commands use options, which consist of a single character preceded by a dash, for example, -l. Many commands, however, including those from the GNU Project, also support *long options*, consisting of a word preceded by two dashes. Also, many commands

allow multiple short options to be strung together. In the following example, the ls command is given two options, which are the l option to produce long format output, and the t option to sort the result by the file's modification time.

```
[me@linuxbox ~]$ ls -lt
```

We'll add the long option --reverse to reverse the order of the sort.

```
[me@linuxbox ~]$ ls -lt --reverse
```

# NOTE

> *Command options, like filenames in Linux, are case sensitive.*

The ls command has a large number of possible options, the most common of which are listed in Table 3-1.

Table 3-1: Common ls Options

| Option | Long option | Description |
|---|---|---|
| -a | --all | List all files, even those with names that begin with a period, which are normally not listed (that is, hidden). |
| -A | --almost-all | Like the -a option except it does not list . (current directory) and .. (parent directory). |
| -d | --directory | Ordinarily, if a directory is specified, ls will list the contents of the directory, not the directory itself. Use this option in conjunction with the -l option to see details about the directory rather than its contents. |
| -F | --classify | This option will append an indicator character to the end of each listed name. For example, it will append a forward slash (/) if the name is a directory. |
| -h | --human-readable | In long format listings, display file sizes in human-readable format rather than in bytes. |
