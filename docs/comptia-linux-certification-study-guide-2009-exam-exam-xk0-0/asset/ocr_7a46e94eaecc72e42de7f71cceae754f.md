# 158  CHAPTER 6: Using BASH

For example, you’ve been using the `ls` command to list the contents of a directory. By default – if not instructed otherwise – the `ls` command will show the contents of only the current directory, limited to just file and directory names, with color-coded file types, formatted in rows, sorted alphabetically. Each of those options can be changed by passing the appropriate option flag. The general format of a BASH command is

```
``` 
command -option(s) parameter(s)
```
```

For the `ls` command that looks like this:

```
``` 
ls -l /etc
```
```

Using the `l` option (as in *“long”*) shows not just the file names, but lots of other interesting information, such as the size, owner, creation or last modified date, and access information. Options can be stacked, so showing the same information sorted by date looks like this:

```
``` 
ls -l -S /etc
```
```

or you can run the options together after a single `-` like this:

```
``` 
ls -lS /etc
```
```

# **Exam Warning**

Pay careful attention to capitalization. Unlike the various Microsoft products, all flavors of UNIX (Linux, BSD, and even OSX) distinguish between upper and lower case, in commands, options, and file names. In the preceding example, `ls -s` shows file sizes, where `ls -S` sorts by size. Likewise, `FILE1`, `File1`, and `file1` are three different files; and `l s` is a valid command, but “LS” is not.

You can even list multiple directories by using the recursive option (`-R`) and/or listing multiple directories as parameters:

```
``` 
ls -R /etc /home
```
```

Most commands have so many options that there aren’t enough letters to assign, so you can often use a long-hand notation, which is a double-dash (`--`) and an entire word. This requires more typing, but is often easier to remember. The command to show all the available options for `ls` uses this:

```
``` 
ls --help
```
```

Don’t be intimidated by the long list of available options; many of them are intended to make `ls` work better within small programs called *scripts*. You