
# What Is UNIX Stuff?

In 1969, the original UNIX had a very-low-level assembly language compiler available for writing programs; all the PDP-7 work was done in this primitive language. Just before the PDP-11 arrived, McIlroy ported a language called TMG to the PDP-7, which Thompson tried to use with a FORTRAN compiler. That didn't work, and instead he produced a language called B. Two years later, in 1971, Ritchie created the first version of a new programming language based on B, a language he called C. By 1973, the entire UNIX system had been rewritten in C for portability and speed.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_19_0.png)

# UNIX Becomes Popular

In the 1970s, AT&T hadn't yet split into the many regional operating companies known today, and the company was prohibited from selling the new UNIX system. Hoping for the best, Bell Labs distributed UNIX to colleges and universities for a nominal charge. These institutions were also buying the expensive and powerful PDP-11 computer systems—a perfect match. Before long, UNIX was the research and software-development operating system of choice.

The UNIX of today is not, however, the product of a couple of inspired programmers at Bell Labs. Many other organizations and institutions contributed significant additions to the system as it evolved from its early beginnings and grew into the monster it is today. Most important were the C shell, TCP/IP networking, vi editor, Berkeley File System, and sendmail-routing software from the Computer Science Research Group of the University of California at Berkeley. Also important were the early versions of UUCP and Usenet from the University of Maryland, Delaware, and from Duke University. After dropping Multics development completely, MIT didn't come into the UNIX until the early 1980s, when they developed the Windows System as part of its successful Athena project. Ten years and four years later, X is the dominant windowing system standard and is the basis of Motif, OpenWindows, and Open Desktop.

Gradually, big corporations have become directly involved with the evolutionary process, notably Hewlett-Packard, Sun Microsystems, and Digital Equipment Corporation. Little companies started to get into the action too, with UNIX available for Apple for the Macintosh and IBM for PCs, RISC-based workstations, and now PowerPC computers.

Today, UNIX runs on all sizes of computers, from humble PCs to powerful desktop visualization workstations, and even to supercomputers that require special cooling to prevent them from burning while working. It's a long way from Space Travel, a game that, ironically, isn't part of UNIX anymore.

# All This About This Multiuser Systems

Among the many words you learned earlier was one directly concerns how you interact with the computer, multiuser. The goal of a multiuser system is for all users to feel as though they've each been given their own personal computer, their own individual UNIX system, although they are actually working within a large system. To accomplish this, each user is given an account—usually based on the person's last name, initials, or another unique naming scheme—and a home directory, the default place where his or her files are saved. This leads to a bit of a puzzle: When you're working on the system, how does the system know that you're you? When to stop someone else from masquerading as you, going into your files, prying into private letters, altering memos, or worse?

On a Macintosh or PC, anyone can walk up to your computer when you're not around, flip the power switch, and you can't do much about it. You can add some security, but it's not fundamental part of the system, which results in an awkward fit between system and software. For a computer sitting on your desk in your office, that's okay; the system is not a shared multiuser, so verifying who you are when you turn on the computer is not critical.

But UNIX is a system designed for multiple users, so it is very important that the system confirm your identity in a manner that precludes others from masquerading as you. As a result, all accounts have passwords associated with them—like a PIN for a bank card, keep it secret—and when you use your password in combination with your account, the computer can be pretty sure that you are who you're claiming to be. For obvious reasons, when you're using the computer, you should always remember to end your session, or in effect, to turn off your virtual computer when you're done.

In the next hour, you will learn your first UNIX commands. At the top of the list are commands to log in to the system, enter your password, and change your password to be memorable and highly secure.

# Cracking Open the Shell

Another unusual feature of UNIX systems, especially for those of you who come from either the Macintosh or the Windows environments, is that UNIX is a command-based system rather than a graphically based (picture-oriented) system. That's a mixed blessing. It makes UNIX harder to learn, but the system is considerably more powerful than fiddling with a mouse to draw little pictures about the screen.

There are graphical interfaces to UNIX, built within the X Window System environment. Notable ones are Motif, Open Windows, and Open Desktop. Even with the best of these, the command-line heart of UNIX shines, and in my experience, it's impossible to use all the power that UNIX offers without turning to a shell.

If you're used to writing letters to your friends and family or even more shopping lists, you won't have any problem with a command-line interface: it's a command program that you tell to do. When you type specific instructions and press the Return key, the computer leaps into action and performs whatever you've specified.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_20_0.png)

# What Is UNIX Stuff?

Throughout this book, I refer to the Return key, but your keyboard may have this key labeled “Enter” or marked with a left-pointing arrow. These all mean the same thing.

JUST A MANUAL

In Windows, you might move a folder from one folder to another by opening the destination folder, fiddling around for a while to be sure you can see both of them on the screen, and then clicking and drawing the specific file from one place to the other. In UNIX it's much easier. Typing in the following simple command does the trick:

cp folder1/file folder2

This might not seem to seem much of a boon, but imagine the situation where you want to move all files with names that start with the word project or end with the suffix .c (C program files). This could be tricky and could take a lot of patience with a graphical interface. UNIX, however, makes it easy:

cp "project" *.c folder2

Soon you will not only understand this command, but you will also be able to compose your own examples!

# Getting Help

Throughout this book, the focus is on the most important and valuable flags and options for the commands covered. That's all well and good, but how do you find out about the other alternatives that might actually work for your use? That's where the UNIX “man” pages come in. You will learn how to browse them to find the information desired.

# Task 1.1: Man Pages, UNIX Online Reference

It's not to you that UNIX is a very complex operating system, with hundreds of commands that can be combined to execute thousands of possible actions. Most commands have a considerable number of options, and all seem to have some subtlety or other that's important to know. But how do you figure all this out? You need to look up commands in the online documentation set. Containing purely reference materials, the UNIX pages (man is short for manual) every command available. Search for a man page, enter man followed by the name of the command to find. Many sites also have a table of contents for the man pages (it's called whatis database, for obscure historical reasons). You can use the all-important -k flag for keyword searches, to find the name of a command if you know what it should do but you just can't remember what it's called.
