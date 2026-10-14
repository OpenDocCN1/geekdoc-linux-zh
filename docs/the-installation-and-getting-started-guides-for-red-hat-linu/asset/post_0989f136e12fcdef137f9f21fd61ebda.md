
. /etc/bashrc
fi

See Figure 16-8 for an example in Pico.

![](img/46f4935125ba89e12897afbe9d77a097_712_0.png)

## Figure 16-8: Adding an alias for the ls command to the .bashrc file

Double-check for any typos then, when you're satisfied with the changes, exit by pressing the [Ctrl] and [X] keys. You'll see, at the bottom of your editor screen, a message reading:

```
Save modified buffer (ANSWERING "No" WILL DESTROY CHANGES)?
Press [Y] for "yes."
```

Now, another message will appear at the bottom:

```
File Name to write: .bashrc
Simply pressing [Enter] will save your changes to your
.bashrc file.
```

You won't be able to see your changes take effect until you close your xterm window and open a new xterm. Once you do that, you'll see your modifications take effect.

Here's a short list of some popular options with ls. Remember, you can view the full list by reading the ls man page (man ls).

- **-a — all.** Lists all the files in the directory, including the hidden files (.filename). The .. and . at the top of your list refer to the parent directory and the current directory, respectively.
- **-l — long.** Lists details about contents, including permissions {modes}, owner, group, size, creation date, whether the file is linked to somewhere else on the system and where its link points.
- **-F — file type.** Adds a symbol to the end of each listing. These symbols include / to indicate a directory; @ to indicate a symbolic link to another file; * to indicate an executable file.
- **-r — reverse.** Lists the contents of the directory from back to front.
- **-R — recursive.** This recursive option lists the contents of all directories (below the current directory) recursively.
- **-S — size.** Sorts files by their size.

A little later in this chapter, when we introduce you to pipes and I/O redirection, you'll discover that there are other ways to view the contents of a directory.

- **Summary:** To see the contents of a directory, type ls at a shell prompt; typing ls -a will display all the contents of a directory; typing ls -a — color will display all the contents categorized by color.

## The Getting Started Guide for Red Hat Linux 6.0

## A Larger Picture of the Filesystem

Every operating system has a method of storing its files and directories so that it can keep track of additions, modifications and other changes. In Linux, every file is stored on the system with a unique name, in directories which can also hold other files directories — or, subdirectories. You might think of the system as a tree-like structure, in which directories “branch off.” Those directories may contain — or be the “parent” of — other directories which may hold files or directories of their own. There wouldn’t be a tree without a root, and the same is true for the Linux filesystem. No matter how far away the branches, everything is connected to the root, which is represented as a single forward slash (/). It might seem confusing to have several references to “root” - the root account, the root account’s login directory and the root directory (/), but think of it this way: The root login, who is the system administrator, is just as important to keeping things together in the system as the system’s root (/).

- Tip: Even though there are other Linux distributions, your Red Hat Linux system is likely to be compatible with them. The reason is because of the Filesystem Hierarchy Standard (also known as FHS). These guidelines help to standardize the way system programs and files are stored on all Linux systems. You can read more about the FHS at its website: http://www.pathname.com/fhs/

As long as we’re logged into our user account — which will help prevent disastrous mistakes — let’s take a look around. The first stop on this tour ought to be the root directory, which will give us a larger picture of where things are. At the shell prompt, then, let’s type:

```
cd /
```

We’ll see a prompt which looks like:

```
[billy@localhost /]
```

Now, let’s see which directories “branch off” root by typing:

```
ls
```
