
## 16.1 Project Description

In day-to-day use, the one program that does use just about everything in the book is the shell. And indeed, there are Unix programming books that write a small but working shell to illustrate the principles involved.

Real shells are large and messy creatures. They must deal with many portability issues, such as we've outlined throughout the book, and above and beyond that, they often have to work around bugs in different versions of Unix. Furthermore, to be useful, shells do many things that don't involve the system call API, such as maintaining shell variables, a history of saved commands, and so on. Providing a complete tour of a full-featured shell such as Bash, ksh93, or zsh would take a separate volume.

Instead, we suggest the following list of steps for writing your own shell, either as a (large) exercise to cement your understanding or perhaps as a cooperative project if you're in school.

1. Design your command "language" so that it will be easy to interpret with simple code. While compiler and interpreter technology is valuable when writing a production shell, it's likely to be overkill for you at this stage. Consider the following points:
    - Are you going to use i18n facilities?
    - What commands must be built in to the shell?
    - To be useful, your shell will need a command search path mechanism, analogous to $PATH of the regular shell. How will you set it?
    - What I/O redirections do you wish to support? Files only? Pipes too? Do you wish to be able to redirect more than file descriptors 0, 1, and 2?
    - Decide how quoting will work: single and double quotes? Or only one kind? How do you quote a quote? How does quoting interact with I/O redirections?
    - How will you handle putting commands in the background? What about waiting for a command in the background to finish?
    - Decide whether you will have shell variables.
    - What kind of wildcarding or other expansions will you support? How do they interact with quoting? With shell variables?
    - You should plan for at least an if and a while statement. Design a syntax. We will call these block statements.
    - Decide whether or not you wish to allow I/O redirection for a block statement. If yes, what will the syntax look like?
    - Decide how, if at all, your shell language should handle signals.
    - Design a testing and debugging framework before you start to code.
    - If you're going to use `i18n` facilities, do so from the outset. Retrofitting them in is painful.
    - For the real work, start simply. The initial version should read one line at a time and break it into words to use as separate arguments. Don't do any quoting, I/O redirection, or anything else. Don't even try to create a new process to run the entered program. How are you going to test what you have so far?
    - Add quoting so that individual "words" can contain whitespace. Does the quoting code implement your design?
    - Make your built-in commands work. (See Section 4.6, "Creating Files," page 106, and Section 8.4.1, "Changing Directory: `chdir()` and `fchdir()`," page 256, for at least two necessary built-in commands.) How are you going to test them?
    - Initially, use a fixed search path, such as "/bin;/usr/bin;/usr/local/bin". Add process creation with `fork()` and execution with `exec()` (see Chapter 9, "Process Management and Pipes," page 283). Starting out, the shell should wait for each new program to finish.
    - Add backgrounding and, as a separate command, waiting for process completion (see Chapter 9, "Process Management and Pipes," page 283).
    - Add a user-settable search path (see Section 2.4, "The Environment," page 40).
2. Add I/O redirection for files (see Section 9.4, “File Descriptor Management,” page 320).
3. Add shell variables. Test their interaction with quoting.
4. Add wildcard and any other expansions (see Section 12.7, “Metacharacter Expansions,” page 461). Test their interaction with shell variables. Test their interaction with quoting.
5. Add pipelines (see Section 9.3, “Basic Interprocess Communication: Pipes and FIFOs,” page 315). At this point, real complexity starts to settle in. You may need to take a hard look at how you’re managing data that represents commands to be run.

You could stop here with a legitimate feeling of accomplishment if you get a working shell that can do everything mentioned so far.

6. If you’re up for a further challenge, add if and/or while statements.
7. Add signal handling (see Chapter 10, “Signals,” page 347).
8. If you’d like to use your shell for real work, explore the GNU Readline library (type 'info readline' on a GNU/Linux system or see the source for the Bash shell). This library lets you add either Emacs-style or vi-style command-line editing to interactive programs.

> Keep two things constantly in mind: always be able to test what you’re doing; and “no arbitrary limits!”

Once it’s done, do a post-mortem analysis of the project. How would you do it differently the second time?

Good luck!

## 16.2 Suggested Reading

1. *The UNIX Programming Environment*, by Brian W. Kernighan and Rob Pike. Prentice-Hall, Englewood Cliffs, New Jersey, USA, 1984. ISBN: 0-13-937699-2.

This is the classic book on Unix programming, describing the entire gestalt of the Unix environment, from interactive use, to shell programming, to programming with the <stdio.h> functions and the lower-level system calls, to program development with make, yacc, and lex, and documentation with nroff and troff. Although the book shows its age, it is still eminently worth reading, and we highly recommend it.

2. *The Art of UNIX Programming*, by Eric S. Raymond. Addison-Wesley, Reading, Massachusetts, USA, 2004. ISBN: 0-13-142901-9.

This is a higher-level book that focuses on the design issues in Unix programming: how Unix programs work and how to design your own programs to fit comfortably into a Linux/Unix environment.

While we don’t always agree with much of what the author has to say, the book does have considerable important material and is worth reading.

# Part IV

# Appendixes

- Appendix A Teach Yourself Programming in Ten Years page 649
- Appendix B Caldera Ancient UNIX License page 655
- Appendix C GNU General Public License page 657

![](img/766b5597246d532412fad21b1c59ccec_681_0.png)

# Teach Yourself Programming in Ten Years

> “Experience, n: Something you don’t get until just after you need it.” 
> —Olivier—

This chapter is written by and Copyright © 2001 by Peter Norvig. Reprinted by permission. The original article, including hyperlinks, is at http://www.norvig.com/21-days.html. We have included it because we believe that it conveys an important message. The above quote is one of our long-time favorites, and as it applies to the point of this appendix, we’ve included it too.

## Why Is Everyone in Such a Rush?

Walk into any bookstore, and you’ll see how to Teach Yourself Java in 7 Days alongside endless variations offering to teach Visual Basic, Windows, the Internet, and so on in a few days or hours. I did the following power search at Amazon.com:

`pubdate: after 1992 and title: days and (title: learn or title: teach yourself)`

and got back 248 hits. The first 78 were computer books (number 79 was Learn Bengali in 30 days). I replaced “days” with “hours” and got remarkably similar results: 253 more books, with 77 computer books followed by Teach Yourself Grammar and Style in 24 Hours at number 78. Out of the top 200 total, 96% were computer books.

The conclusion is that either people are in a big rush to learn about computers, or that computers are somehow fabulously easier to learn than anything else. There are no books on how to learn Beethoven, or Quantum Physics, or even Dog Grooming in a few days.

Let’s analyze what a title like Learn Pascal in Three Days could mean:

- **Learn:** In 3 days you won’t have time to write several significant programs, and learn from your successes and failures with them. You won’t have time to work with an experienced programmer and understand what it is like to live in that environment. In short, you won’t have time to learn much. So they can only be talking about a superficial familiarity, not a deep understanding. As Alexander Pope said, a little learning is a dangerous thing.
- **Pascal:** In 3 days you might be able to learn the syntax of Pascal (if you already knew a similar language), but you couldn’t learn much about how to use the syntax. In short, if you were, say, a Basic programmer, you could learn to write programs in the style of Basic using Pascal syntax, but you couldn’t learn what Pascal is actually good (and bad) for. So what’s the point? Alan Perlis once said: “A language that doesn’t affect the way you think about programming, is not worth knowing.” One possible point is that you have to learn a tiny bit of Pascal (or more likely, something like Visual Basic or JavaScript) because you need to interface with an existing tool to accomplish a specific task. But then you’re not learning how to program; you’re learning to accomplish that task.
- **In Three Days:** Unfortunately, this is not enough, as the next section shows.

## Teach Yourself Programming in Ten Years

Researchers (Hayes, Bloom) have shown it takes about ten years to develop expertise in any of a wide variety of areas, including chess playing, music composition, painting, piano playing, swimming, tennis, and research in neuropsychology and topology. There
