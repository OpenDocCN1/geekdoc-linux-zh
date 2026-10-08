
What's the Problem? This lesson talks about getting or finding help for Unix. It does not cover how to solve any technical problems you may have, which is usually a job for a help desk technician. This chapter revolves around how to get assistance when learning Unix, not how to fix it if it is broken, which is beyond the scope of this text.

## Finding Help in Unix

It should come as absolutely no surprise that products such as Microsoft Windows have built-in help systems; perhaps you have even used them. Most common computer operating systems do detail help systems built right into them. Unix is no different, and although it seems to have been around as long if not longer than many other operating systems, it also has as detailed help system as any.

Unix was created without a thought to being user friendly; it was built for power, functionality, flexibility, and control. Because Unix is generally a command-line-driven system, there is commonly no mouse to point and click; therefore it doesn't know where to find it. However, the joke is on us: Once you know how to use the Unix help system, you only need to go to a shell prompt and type the correct command to access it. You don't need to point and click unless you are navigating in an X Window System environment.

If you know how to access the built-in help system in Unix, it can help you perform just about any command known in the system. You should be aware, that each version of Unix has its own version or form of help, and these forms may not be identical. For instance, SuSE Linux and Red Hat Linux have commands that do not match. This does not mean that the commands are not similar or that they will perform the same exact function. Sun Solaris–based Unix and FreeBSD have different commands as well, but most of the core functionality is the same. Although there may be differences in the names of commands, most commands are identical by design. If you can’t get a command to work, it may just mean that you are typing in the incorrect syntax for your particular system. This is another example of why you should use the system’s manual pages, or man pages for short. In such cases, the man pages are all you need to get the help you require.

Always remember, the power of Unix is found in the commands you use, so to have a way to constantly check whether something is wrong or whether the syntax for a specific command is correct is helpful, to say the least. Again, this can be done using the man pages.

## Using the Man Pages

Man pages are nothing more than compressed text files, located in /usr/share/doc. The information included is a command reference. Occasionally there are even known bug statements found within man pages. One thing is for certain—man pages are helpful if used properly.

As programs grew increasingly complex, they began to tap the man page format, so the info help format was created. These pages include a hierarchical structure, hypertext links for easy navigation between documents, and keyboard and mouse navigational tools. The first time you use info help (often when looking for help in the Emacs text editor), it can be a little overwhelming, but this format is not difficult to use once you have a feel for it.

> Want to Know More? To learn more about info help, type info info at the shell prompt. This will allow you to read the tutorial.

As we will learn in the following sections, there are also many resources on the Internet that include man pages. For example, man pages can be found on Google or the Linux Documentation Project.

## Getting Help

As just mentioned, you will eventually need some form of help in your Unix journey. Not all of your issues will be addressed in the man pages, but many of them will be. Help comes in different forms. For example, you may need help with a command as ls. The ls command is used to list the names of files that are found in your current directory. In the man pages, you may see the syntax on the use of ls but not necessarily understand what you need to do with. In other words, your problems may run deeper than the help provided in a man page. This is where time, practice, reading and learning save the day. The man pages are only for your reference; they will not do anything for you unless you are able to understand what they say and perform the appropriate actions.

Why use man pages instead of the Internet or any other resource? To answer this question, remember the purpose of the man page: It's there to help you, not to do the work for you. All the information you need for the command syntax is found within man page. If you want to look for further suggestions on use, then that's a different story. But why look outside the box when you have the answer inside the box? Check the man page before you move to any other resources.

In addition, there is no definitive source for Unix information on the Internet. There are scattered resources that can help you if you know the specific vendor of the product you are using (SuSE, AIX, SCO ACE, and so forth) and the vendor provides support documentation. You may also find some information if you are a master at searching the Internet, but chances that this information will be secondhand at best. Because Unix users have always relied upon the system's own internals for assistance, man pages are the best-known resource for you as a Unix student. These pages are anywhere Unix unless the files or links to them are damaged and in need of repair. To review, benefits of man pages include the following:

- Man pages are the quickest source for complete information on how to use the commands on your system.
- Man pages provide information on what programs do and how to use them.
- Man pages cover other related utilities that you might be interested in working with. The recommendations on these pages could also be of help to you.
- If you're a programmer or developer, man pages will also provide helpful programming information that you can use when coding and writing scripts.

To display a manual page, use the man command. By simply typing man followed by the command you want to look up, you will get the results you need.

```
>ls
```

```
NAME
ls - list directory contents
SYNOPSIS
ls [OPTION]... [FILE]
DESCRIPTION
List information about the FILES (the current directory by default).
(output removed)
```

In this example, the man pages showed you all the available syntax you can use with the ls command. You can use this information to get added details on the command.

As you can see, man pages do not enter a command for you, and they don't help you do a task—they are simply informative. When using man pages, what you are looking for is additional information about a command; that way, you can customize the command with the many different switches that can be applied to it.

As you use man pages, you may find them unwieldy and long. Never fear, because there are shortcuts to using the help system. These are in the form of apropos and whatis.

Commands You Need to Know

When you see a . . on your screen, there's more text to be read. What you need to do is press the Spacebar to see the additional text.

The man pages won't scroll automatically, so you may need to carry out this extra step. To stop this action, press q to quit the page and return to the command line.

## More Help

Now that you are familiar with the built-in help in Unix and how to use the man pages and the man command, we will look at some other ways to use man. We'll also explore the use of apropos and whatis, those programs can help you find additional assistance.

As mentioned earlier, the man command can often generate unwieldy results. This can be especially problematic if you just want to find a subset of the information on a man page. If this subset is all you need (for example, if you only want to find a summary description of a command), then you can use the following commands:

```
whatis
man -f
apropos
man -k
```

Using any of these followed by the command you are interested in (just like the ls example) will result in a shorter set of information being supplied back to you. Lets look at each of these commands in detail.

### whatis and man -f

The man command used with the -f switch is similar to the whatis command, as apropos is similar to the man command with the -k switch. The full power of most Unix commands can only be unleashed with the use of switches, so make sure you pay close attention to how they are used in this lesson and in the rest of the book.
