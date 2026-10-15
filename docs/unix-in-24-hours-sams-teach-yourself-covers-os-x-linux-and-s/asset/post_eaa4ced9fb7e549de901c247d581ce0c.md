
the system as it evolved from its early beginnings and grew into the monster it is today. Most important were the C shell, TCP/IP networking, vi editor, Berkeley Fast File System, and sendmail electronic mail-routing software from the Computer Science Research Group of the University of California at Berkeley. Also important were the early versions of UUCP and Usenet from the University of Maryland, University of Delaware, and Duke University. After dropping Multics development completely, MIT didn’t come into the Unix picture until the early 1980s, when it developed the X Window System as part of its successful Athena project. Fifteen years and five releases later, X (more formally, X11R6) is the predominant windowing system standard on all Unix systems, and it is the basis of Gnome, KDE, Unity, and Open Desktop.

Gradually, large corporations have become directly involved with the evolutionary process, notably Hewlett-Packard, Sun Microsystems, and IBM. Smaller companies have started to get into the action, too, with Unix available from Apple for the Macintosh (it’s the underpinning of Mac OS X) and Linux systems built upon the concepts of Unix from Red Hat, Debian, and many other vendors for PCs.

Today, Unix runs on all sizes of computers, from humble PC laptops to powerful desktop-visualization workstations, and even to supercomputers that require special cooling fluids to prevent them from burning up while working. It’s a long way from Space Travel, a game that, sadly, isn’t part of Unix anymore.

## What’s All This About Multiuser Systems?

Among the many *multi* words you learned earlier was one that directly concerns how you interact with the computer: multiuser. The goal of a multiuser system is for all users to feel as though they’ve been given their own personal computer, their own individual Unix system, although they actually are working within a large system. To accomplish this, each user is given an account—usually based on the person’s last name or initials or another unique naming scheme—and a home directory, the default place where the user’s files are saved. This leads to a bit of a puzzle: When you’re working on the system, how does the system know that you’re you? What’s to stop someone else from masquerading as you, going into your files, prying into private letters, altering memos, or worse?

In the early days, anyone could walk up to your Macintosh or PC when you weren’t around, flip the power switch, and pry, and you couldn’t do much about it. For a computer sitting on your desk in your office, that’s okay; the system is not a shared multiuser system, so verifying who you are when you turn on the computer isn’t critical.

But Unix is designed for multiple users, so it is very important that the system can confirm your identity in a manner that precludes others from masquerading as you. As a result, all accounts have passwords associated with them—as with a PIN for a bank card, keep it a secret!—and when you use your password in combination with your account, the computer can be pretty sure that you are who you’re claiming to be. For obvious reasons, when you’re finished using the computer, you should always remember to exit your session, or, in effect, to turn off your virtual personal computer when you’re done.

highly secure.

## Cracking Open the Shell

Another unusual feature of Unix systems, especially for those of you who come from either the Macintosh or Windows environments, is that Unix is primarily designed to be a command-line–based system rather than a more graphically based system. That’s a mixed blessing. It makes Unix harder to learn, but the system is considerably more powerful than one that asks you to fiddle with a mouse to drag little pictures about on the screen. In Unix parlance, a command-line interpreter is called a shell, and you’ll see that various shells are available, differing in both syntax and capabilities.

Graphical interfaces to Unix are built within the X Window System environment. Notable ones are KDE, OpenWindows, Gnome, and Unity. Even with the best of these, however, the command-line heart of Unix still shines through, and in my experience, it’s impossible to use all the power that Unix offers without turning to a shell.

If you’re used to writing letters to your friends and family or even just producing simple grocery lists, you won’t have any problem with a command-line interface: It’s a command program that you tell what to do. When you type specific instructions and press the Return key, the computer leaps into action and immediately performs whatever command you’ve specified, even if it’s dangerous, such as the command sequence that requests the system to “remove all my files.”

### Note

Throughout this book, I refer to pressing the Return key, but your keyboard might have this key labeled as “Enter” or marked with a left-pointing, specially shaped arrow. These all mean the same thing.

In Windows, you might move a file from one folder to another by opening the folder, opening the destination folder, fiddling around for a while to be sure that you can see both folders onscreen at the same time, and then clicking and dragging the specific file from one place to the other. In Unix it’s much easier: Typing the following simple command does the trick:

```
mv folder1/file folder2
```

This command automatically also ensures that the file has the same name in the destination directory.

This might not seem like much of a boon, but imagine that you want to move all files with names that start with the word project or end with the suffix .c (C program files). This task could be quite tricky and could take a lot of patience with a graphical interface. Unix, however, makes it easy:

```
mv project* *.c folder2
```

Soon you will not only understand this command but also be able to compose your own examples!
