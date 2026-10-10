```
```
[christine@localhost ~]$ cd ../../etc
[christine@localhost etc]$ pwd
/etc
[christine@localhost etc]$
```
```

Of course, in a case like this, you actually have to do more typing rather than just typing the absolute directory reference, `/etc`. Thus, use a relative directory reference only if it makes sense to do so.

> **NOTE**
> 
> It’s helpful to have a long informative shell CLI prompt, as used in this chapter section. However, for clarity purposes, a simple `$` prompt is used in the rest of the book’s examples.

Now that you know how to traverse the directory system and confirm your present working directory, you can start to explore what’s contained within the various directories. The next section takes you through the process of looking at files within the directory structure.

# Listing Files and Directories

To see what files are available on the system, use the `list` command (`ls`). This section describes the `ls` command and options available to format the information it can display.

# Displaying a basic listing

The `ls` command at its most basic form displays the files and directories located in your current directory:

```
```
$ ls
 Desktop    Downloads   my_script   Public      test_file
 Documents  Music       Pictures    Templates   Videos
$
```
```

Notice that the `ls` command produces the listing in alphabetical order (in columns rather than rows). If you’re using a terminal emulator that