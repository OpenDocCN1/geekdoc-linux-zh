of one blank line at a time. That is, if your file has 1 line of text, 10 blank lines, 1 line of text, 10 blank lines, and so on, -s shows the first line of text, a single blank line, the next line of text, a single blank line, and so forth. When you combine -s and -n, cat numbers only the lines that are printed—the 10 blank lines shown as one will count as 1 line for numbering.

This command prints information about your CPU, stripping out multiple blank lines and numbering the output:

```
cat -sn /proc/cpuinfo
```

You can also use cat to print the contents of several files at once, like this:

```
cat -S myFile.txt myOtherFile.txt
```

In that command, cat merges myFile.txt and myOtherFile.txt on the output, stripping out multiple blank lines. The important thing is that cat does not distinguish between the files in the output—there are no filenames printed, and no extra breaks between the 2. This allows you to treat the 2 as 1 or, by adding more files to the command line, to treat 20 files as 1.

# Changing Directories with cd

Changing directories is surely something that has no options, right? Not so. cd is actually more flexible than most people realize. Unlike most of the other commands here, cd is not a command in itself—it is built in to bash (or whichever shell interpreter you are using), but it is still used like a command.

The most basic usage of cd is this:

```
cd someDir
```

That command looks in the current directory for the someDir subdirectory, and then moves you into it. You can also specify an exact location for a directory, like this:

```
cd /home/paul/stuff/someDir
```

The first part of cd’s magic lies in the characters (- and ~, a dash and a tilde). The first means "switch to my previous directory," and the second means "switch to my home directory." This conversation with cd shows this in action:

```
[paul@caitlin ~]$ cd /usr/local
[paul@caitlin local]$ cd bin
[paul@caitlin bin]$ cd -
/usr/local
[paul@caitlin local]$ cd ~
[paul@caitlin ~]$
```