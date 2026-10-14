
## System Files

- `.rpm — a Red Hat Package Manager file`
- `.conf — a configuration file`
- `.a — an archive file`
- `.lock — a “lock” file; determines whether a program is in use`

## Programming and Scripting Files

- `.h — a C and C++ program language header file`
- `.c — a C program language source code file`
- `.cpp — a C++ program language source code file`
- `.o — a program object file`
- `.pl — a Perl script`
- `.tcl — a TCL script`
- `.so — a library file`

But file extensions are not always used, or used consistently. So what happens when a file doesn’t have an extension, or the file doesn’t seem to be what the extension says it’s supposed to be?

That’s when the file command can come in handy.

In 1, we created a file called saturday — without an extension. Using the file command, we can tell what the file is by typing:

```
file saturday
```

and we’ll see it’s a text file. Any file that’s designated a text file should be readable using cat, more, or less.

- Tip: To learn more about the file command, read the file man page by typing man file.

And speaking of reading files...

There are plenty of ways to read files in Linux. In the previous chapter, for example, we covered the pagers `more` and `less` — they’re called pagers because you can “page” through documents one screen at a time. We also learned how we can not only view but manipulate files with the `cat` command.

But there are even more options when it comes time to take a look at README files, man pages or documents you’ve created.

You have a number of tools to help you read text files, among them, the text editors `pico`, `emacs`, and `vim`, the pagers `more` and `less`, and the viewers `head`, `tail`, `cat`, and `grep`.

Let’s take a look at some of the features in these tools.

## The less Command

In Chapter 1, we were introduced to the pager `less`. `Less` is the pager that’s used to display man pages.

Let’s view the man page for `less` to see `less` in action.

```
man less
```

To move forward a screen, press [Space]; to move back a screen, press [B], and to quit, press [Q].

There are other powerful features in less, as well, including the ability to scroll horizontally and specify the number of lines to scroll.

## The more Command

Odd as it may seem, `more` offers less than `less` (actually, `less` was inspired by `more`).

Let’s take a look at the man page for `more`, but this time, we’ll open the page using `more` — by piping man’s output to `more`.

```
man more | more
```

## The Getting Started Guide for Red Hat Linux 6.0

It may not look too different at first, but there are fewer enhancements to more than to less. Probably the most striking difference at first is the lack of a way to go backwards in a document — although moving forward by pressing [Space] and quitting by pressing [Q] are the same.

## The head Command

You can use the head command if you just want to look at the beginning of a file. The command is:

```
head <filename>
```

Head can be useful, but because it’s limited to the first several lines, you won’t know how long the file actually is. By default, you can only read the first 10 lines of a file, although we can specify the number to see more by typing:

```
head -20 <filename>
```

Read head’s man page (man head) for more information. You’ll probably find that less or more are more helpful, because you can page through the file if you find that the information you’re looking for is further into the file than you originally thought.

## The tail Command

The reverse of head (obviously), is tail. With (tail), you can review the last 10 lines of a file.

## The cat Command

The command cat, short for concatenation, will dump the contents of the entire file on the screen. Using cat can be handy if the file is fairly short, such as when we created sneakers.txt. But if a file is fairly long, it will easily scroll past you on the screen, since cat displays the whole file.
