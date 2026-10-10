
## Contents

- * Chapter 1, *What is Linux?*: What is Linux, how did it come into existence, advantages and disadvantages, what does the future hold for Linux, who should use it, installing your computer.
- * Chapter 2, *Quickstart*: Getting started, connecting to the system, basic commands, where to find help.
- * Chapter 3, *About files and the file system*: The filesystem, important files and directories, managing files and directories, protecting your data.
- * Chapter 4, *Processes*: Understanding and managing processes, boot and shutdown procedures, postponing tasks, repetitive tasks.
- * Chapter 5, *I/O redirection*: What are standard input, output and error and how are these features used from the command line.
- * Chapter 6, *Text editors*: Why you should learn to work with an editor, discussion of the most common editors.
- * Chapter 7, *Home sweet /home*: Configuring your graphical, text and audio environment, settings for the non-native English speaking Linux user, tips for adding extra software.
- * Chapter 8, *Printers and printing*: Converting files to a printable format, getting them out of the printer, hints for solving print problems.
- * Chapter 9, *Fundamental Backup Techniques*: Preparing data to be backed up, discussion of various tools, remote backup.
- * Chapter 10, *Networking*: Overview of Linux networking tools and user applications, with a short discussion of the underlying service daemon programs and secure networking.
- * Chapter 11, *Sound and Video*: Sound and video, including Voice over IP and sound recording is discussed in this chapter.
- * Appendix A, *Where to go from here?*: Which books to read and sites to visit when you have finished reading this one.
- * Appendix B, *DOS versus Linux commands*: A comparison.
- * Appendix C, *Shell Features*: If you ever get stuck, these tables might be an outcome. Also a good argument when your boss insists that YOU should use HIS favorite shell.

## Chapter 1

### What is Linux?

#### Abstract

We will start with an overview of how Linux became the operating system it is today. We will discuss past and future development and take a closer look at the advantages and disadvantages of this system. We will talk about distributions, about Open Source in general and try to explain a little something about GNU.

This chapter answers questions like:

- * What is Linux?
- * Where and how did Linux start?
- * Isn't Linux that system where everything is done in text mode?
- * Does Linux have a future or is it just hype?
- * What are the advantages of using Linux?
- * What are the disadvantages?
- * What kinds of Linux are there and how do I choose the one that fits me?
- * What are the Open Source and GNU movements?

### 1.1 History

#### 1.1.1 UNIX

In order to understand the popularity of Linux, we need to travel back in time, about 30 years ago...

Imagine computers as big as houses, even stadiums. While the sizes of those computers posed substantial problems, there was one thing that made this even worse: every computer had a different operating system. Software was always customized to serve a specific purpose, and software for one given system didn't run on another system. Being able to work with one system didn't automatically mean that you could work with another. It was difficult, both for the users and the system administrators.

Computers were extremely expensive then, and sacrifices had to be made even after the original purchase just to get the users to understand how they worked. The total cost per unit of computing power was enormous.

Technologically the world was not quite that advanced, so they had to live with the size for another decade. In 1969, a team of developers in the Bell Labs laboratories started working on a solution for the software problem, to address these compatibility issues. They developed a new operating system, which was

1. Simple and elegant.
2. Written in the C programming language instead of in assembly code.
3. Able to recycle code.

The Bell Labs developers named their project "UNIX."

The code recycling features were very important. Until then, all commercially available computer systems were written in a code specifically developed for one system. UNIX on the other hand needed only a small piece of that special code, which is now commonly named the kernel. This kernel is the only piece of code that needs to be adapted for every specific system and forms the base of the UNIX system. The operating system and all other functions were built around this kernel and written in a higher programming language, C. This language was especially developed for creating the UNIX system. Using this new technique, it was much easier to develop an operating system that could run on many different types of hardware.

The software vendors were quick to adapt, since they could sell ten times more software almost effortlessly. Weird new situations came in existence: imagine for instance computers from different vendors communicating in the same network, or users working on different systems without the need for extra education to use another computer. UNIX did a great deal to help users become compatible with different systems.

Throughout the next couple of decades the development of UNIX continued. More things became possible to do and more hardware and software vendors added support for UNIX to their products.

UNIX was initially found only in very large environments with mainframes and minicomputers (note that a PC is a “micro” computer). You had to work at a university, for the government or for large financial corporations in order to get your hands on a UNIX system.

But smaller computers were being developed, and by the end of the 80's, many people had home computers. By that time, there were several versions of UNIX available for the PC architecture, but none of them were truly free and more important: they were all terribly slow, so most people ran MS DOS or Windows 3.1 on their home PCs.

#### 1.1.2 Linux and Linus

By the beginning of the 90s home PCs were finally powerful enough to run a full blown UNIX. Linus Torvalds, a young man studying computer science at the university of Helsinki, thought it would be a good idea to have some sort of freely available academic version of UNIX, and promptly started to code.

He started to ask questions, looking for answers and solutions that would help him get UNIX on his PC. Below is one of his first posts in comp.os.minix, dating from 1991:

> From: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)
> Newsgroups: comp.os.minix
> Subject: Gcc-1.40 and a posix-question
> Message-ID: <1991Jul3.10050.98868@klaava.Helsinki.FI>
> Date: 3 Jul 91 10:00:50 GMT
>
> Hello netlanders,
>
> Due to a project I'm working on (in minix), I'm interested in the posix standard definition. Could somebody please point me to a (preferably) machine-readable format of the latest posix rules? Ftp-sites would be nice.

From the start, it was Linus' goal to have a free system that was completely compliant with the original UNIX. That is why he asked for POSIX standards, POSIX still being the standard for UNIX.

In those days plug-and-play wasn't invented yet, but so many people were interested in having a UNIX system of their own, that this was only a small obstacle. New drivers became available for all kinds of new hardware, at a continuously rising speed. Almost as soon as a new piece of hardware became available, someone bought it and submitted it to the Linux test, as the system was gradually being called, releasing more free code for an ever wider range of hardware. These coders didn't stop at their PCs; every piece of hardware they could find was useful for Linux.

Back then, those people were called "nerds" or "freaks", but it didn't matter to them, as long as the supported hardware list grew longer and longer. Thanks to these people, Linux is now not only ideal to run on new PCs, but is also the system of choice for old and exotic hardware that would be useless if Linux didn't exist.
