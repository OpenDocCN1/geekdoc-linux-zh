
2. Better, though, is to grab a copy of the information going down a stream in the middle:

```
% ls -l | awk '{ print $5 "t" $9 }' | sort -rn | tee bigfiles | head
12556 keyline.pie
8729 owl.c
1024 Mail/
582 tetme
512 temp/
```

This shows only the five largest files on the screen, but the bigfiles actually has a list of all files, sorted by size:

```
% cat bigfiles
12556 keyline.pie
8729 owl.c
1024 Mail/
582 tetme
512 temp/
512 src/
512 bin/
512 Oil/
512 News/
512 Infolder/
512 Archives/
207 sample
199 sample
126 awkscript
```

The tee command is a classic UNIX utility, as stated before, it seems useful but a bit limited in purpose. As you're learning through all the examples in this book, however, from lots of commands do big, powerful commands grow.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_206_0.png)

# Summary

In this hour, you have had a chance to build on the knowledge you are picking up about UNIX, with your introduction to an exciting and powerful UNIX utility, awk.

# Workshop

This Workshop poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Questions

- 1. Expand on the plumbing metaphor with UNIX. What program enables you to split the flow into multiple files? What enables you to fit multiple commands into a pipeline? What enables you to put something into the file?

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_206_1.png)

- 2. Will the following two commands do the same thing?

```
who | awk '{print $1}' | grep taylor
who | grep taylor | awk '{print $1}'
```

- 3. Will this command do the same as that in the second question?

```
who | awk '{ if $1 == "tailor") print $0 }'
```

- 4. Create a simple awk script that will sort lines in a file by the number of words on the line. Pay attention to the NF record in awk itself.

# Preview of the Next Hour

Starting with the next hour, you learn about another powerful and popular program in the entire UNIX system, a program so helpful that versions of it exist even on DOS and the Macintosh today. It fills in the missing piece of your UNIX knowledge and, if what's been covered so far focuses on the plumbing analogy, this command finally moves you beyond considering UNIX as a typewriter (a tty). What's the program? It's the vi screen-oriented editor. It's another program that deserves a book or two, but in two hours, you learn the basics of vi and enough additional commands to let you work with the program easily and efficiently.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_207_0.png)

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_208_0.png)

# Hour 11

# An Introduction to the vi Editor

If you like primitive tools, you've already figured out that you can use a combination of << and cat to add lines to a file, and you can use sed and file redirection to modify the contents of a file. These tools are rough and awkward, and when it's time to either create new files or to modify existing files, you need a screen-oriented editor. In UNIX, the screen editor of choice is vi.

There are a number of editors that may be included with your UNIX system, including ed, vi, and emacs. The latter two use the entire screen, a big advantage, and both are powerful editors. You learn about both in these hours. I focus on vi, however, because I believe it's easier and perhaps more important, it's guaranteed to always be part of UNIX, whereas most vendors omit emacs, forcing you to find it yourself.

The next three hours focus on full-screen editing tools for UNIX. This is the first of two hours in which you learn how to use vi to create and modify files. The first hour covers the basics, including how to move around in the file; how to insert and delete characters, words, and lines; and how to search for specific patterns in the text. The next hour gives an introduction to key mapping, default files, and the ways to use the rest of UNIX while within vi. In the last hour, you learn to use an alternate UNIX editor called emacs.

In this hour, you learn:

- How to start and quit vi
- Simple cursor motion in vi
- How to move by words and pages
- How to insert text into the file
- How to delete text
- How to search within a file
- How to have vi start out right
- The colon commands in vi

In some ways, an editor is like another operating system living within UNIX; it is so complex that you will need two hours to master it. If you're used to graphical editors, you'll be unhappy that vi doesn't use a mouse. Once you spend some time with vi, you'll get used to it. In this hour, you learn the basics.

# Goals for This Hour

In some ways, an editor is like another operating system living within UNIX; it is so complex that you will need two hours to master it. If you're used to graphical editors, you'll be unhappy that vi doesn't use a mouse. Once you spend some time with vi, you'll get used to it. In this hour, you learn the basics.

# Task 11: To Start and Quit

You may have noticed that vi has two modes. The first is insert mode, where you add text directly into the file. The second is command mode, where you enter commands to manipulate the text. To switch between these modes, use the Escape key.

In some ways, an editor is like another operating system living within UNIX; it is so complex that you will need two hours to master it. If you're used to graphical editors, you'll be unhappy that vi doesn't use a mouse. Once you spend some time with vi, you'll get used to it. In this hour, you learn the basics.

# An Introduction to the Editor

Before you start vi for the first time, you must learn about two aspects of its behavior. The first is insert mode, where you add text directly into the file. The second is command mode, where you enter commands to manipulate the text. To switch between these modes, use the Escape key.

In some ways, an editor is like another operating system living within UNIX; it is so complex that you will need two hours to master it. If you're used to graphical editors, you'll be unhappy that vi doesn't use a mouse. Once you spend some time with vi, you'll get used to it. In this hour, you learn the basics.

Where did vi get its name? It was written by Bill Joy while he was at the University of California. It was named because it stands for "visual editor".

In some ways, an editor is like another operating system living within UNIX; it is so complex that you will need two hours to master it. If you're used to graphical editors, you'll be unhappy that vi doesn't use a mouse. Once you spend some time with vi, you'll get used to it. In this hour, you learn the basics.

# ACTION

- 1. To begin, enter vi at the prompt. If all is working well, the screen will clear, the first character on each line will become a tilde, and the cursor will be sitting at the top-left corner of the screen:

```
% vi
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_211_0.png)

> I'm going to show you only the portion of the screen that is relevant to the command being discussed for vi, rather than show you the entire screen each time. When the full screen is required to explain something, it'll show up. A smooth edge will indicate the edge of the screen, and a jagged edge will indicate that the rest of the display has been omitted.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_211_1.png)

Type a colon character. Doing so moves the cursor to the bottom of the screen and replaces the last tilde with the colon:

```
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
:
```
