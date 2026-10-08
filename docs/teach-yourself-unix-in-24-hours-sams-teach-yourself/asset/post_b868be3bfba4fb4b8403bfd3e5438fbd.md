
![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_14_0.png)

## TIME SAVER

Time Savers inform you of tricks or elements that are easily missed by most computer users. You can skip them, but often Time Savers show you an easier way to do a task.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_14_1.png)

## CAUTION

A Caution deserves at least as much attention as a Time Saver because Cautions point out a problematic element of the topic being discussed. Ignoring the information contained in the Caution could have adverse effects on the task at hand. These are the most important special elements in this book.

## Tasks

This book offers another special element called a Task. These step-by-step exercises are designed to quickly walk you through the most important skills you can learn in UNIX. Each Task has three parts—Description, Action, and Summary.

## Workshops

The Workshop section at the end of each lesson provides Key Terms and Questions that reinforce concepts you learned in the lesson and help you apply them in new situations. You can skip this section, but it is advised that you go through the exercises to see how the concepts can be applied to other common tasks. The Key Terms also are compiled in one alphabetized list in the Glossary at the end of the book.

## Hour 1

### What Is This UNIX Stuff?

Welcome to Teach Yourself UNIX in 24 Hours! This hour starts toward becoming a UNIX expert. Your goal for the first hour is to introduce you to some UNIX history and teach you where to go for help online.

### Goals for This Hour

In the first hour, you learn

- The history of UNIX
- Why it's called UNIX
- What multiuser systems are all about
- The difference between UNIX and other operating systems
- About command-line interpreters and how users interact with UNIX
- How to use man pages, UNIX's online reference material
- Other ways to find help in UNIX

## What Is UNIX?

UNIX is a computer operating system, a control program that works with users to run programs, manage resources, and communicate with other computer systems. Several people can use a UNIX computer at the same time; hence UNIX is called a multiuser system. Any of these users can also run multiple programs at the time; hence UNIX is called multitasking. Because UNIX is such a patchwork—a patch of development—it's a lot more than just an operating system. UNIX has more than 250 individual commands. These range from simple commands—for copying a file, for example to the complex ones used in high-speed networking, file management, and software development.

Most notably, UNIX is a multichoice system. As an example, UNIX has three different primary command-line interfaces (in UNIX, the command-user interface is called a shell). The three choices are the Bourne shell, C shell, and Korn shell. Often, after you learn to accomplish a task with a particular command, you discover a second or third way to do that. This is simultaneously the strength of UNIX and one frustration for both new and current users.

Why is having all choice such a big deal? Think about Microsoft-DOS and the Apple Macintosh interfaces are so easy to use. Both are designed to give the user less power. But have dramatically different commands and precious overlap in commands: You can't copy to list your files in DOS, and you can't drag a Mac icon around to duplicate it in its own directory. The advantage to these interfaces is that, in either system, you can learn the one-and-only way to do a task and be confident that you're as sophisticated in doing it in its own directory. It's easy. It's quick to learn. It's exactly how the experts do it, too.

UNIX, by contrast, is much more like a spoken language, with commands acting as verbs, command options (which you learn later in this lesson) acting as adjectives, and the more complex commands acting akin to sentences. How do you do a specific task, then, completely different from how specific commands in UNIX have many versions, because of different UNIX vendors. (You've heard of these variations and vendors, I bet: UNIXWare from Solaris, Sun SCO from Santa Cruz, System V Release 4 (pronounced "system five release four") or, to sound like an ace, "ess-vee-four") and BSD UNIX (pronounced "bee-ess-dee") from University of California at Berkeley are the primary players. Each is a little different from the other.) Another contributor to the sprawl of modern UNIX is the energy of the programming community; plenty of UNIX users decide to write a new version of a command in order to solve slightly different problems, then spawning many versions of a command.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_16_0.png)

### What Is This UNIX Stuff?

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_17_0.png)

### JUST A Minute

I must admit that I, too, am guilty of rewriting a variety of UNIX commands, including those for an electronic mail system, a simple line-oriented editor, a text formatter, a programming language interpreter, calendar manager, and even slightly different versions of the file-listing command ls and the remove-files command rm. As a programmer, I found trying to duplicate the functionality of a particular command or utility was a wonderful way to learn about UNIX and programming.

The multichoice nature of UNIX, I promise to teach you the most popular UNIX commands, and if there are alternatives, I will teach you about those. The goal of this book is for you to learn UNIX and to be able work alongside long-time folk as a peer, sharing your expertise with them and continuing to learn about the system and commands from them and other sources.

### A Brief History of UNIX

To understand why the UNIX operating system has so many commands and why it's not only the premier multiuser system but also the most successful and the most powerful multiuser system for computers, you'll have to travel back in time. You'll need to learn how UNIX was designed, what were the goals of the original programmers, and what has happened to UNIX in the subsequent decades.

Unlike DOS, Windows, OS/2, the Macintosh, VMS, MVS, and just about any other operating system, UNIX was designed by a couple of programmers as a free project, and it evolved through the efforts of hundreds of programmers, each of whom was his or her own ideas of particular aspects of OS design and user interaction. In this regard, UNIX is not like other operating systems, needless to say!

It started back in the 1960s in the...

In 1970, Thompson's group requested and received a Digital PDP-11 system for the purpose of creating a system for editing and formatting text. It was an early that the first disk did not arrive at Bell Labs until months after the CPU showed. The first important program on UNIX was the text-formatting program roff, which—keep with me now—was inspired by McIlroy's BCPL on Multics, which had been inspired by an earlier program that ran off on the CTSS operating system.

The initial customer was the Patent Department inside Labs, a group that needed a system for preparing patent applications. There, UNIX was a dramatic success, and it didn't take long for others inside Bell Labs to begin claiming them for their UNIX computer systems.

In 1969...

What was missing in this earliest form of UNIX was pathnames. No slash (/) was present, and subdirectories were referenced through a confusing combination of file links that proved too complex, causing users to stop using subdirectories. Directories could be added while the system was running and had to be added to the preloaded configuration.

## The C Programming Language

That's where UNIX came from. What about C, the programming language that is integral to the system?
