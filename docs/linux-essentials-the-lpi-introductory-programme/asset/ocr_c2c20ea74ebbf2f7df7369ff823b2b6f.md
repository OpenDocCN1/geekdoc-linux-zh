# 4.1 Why?

More so than other modern operating systems, Linux (like Unix) is based on the idea of entering textual commands via the keyboard. This may sound antiqued to some, especially if one is used to systems like Windows, who have been trying for 15 years or so to brainwash their audience into thinking that graphical user interfaces are the be-all and end-all. For many people who come to Linux from Windows, the comparative prominence of the command line interface is at first a "culture shock" like that suffered by a 21-century person if they suddenly got transported to King Arthur's court – no cellular coverage, bad table manners, and dreadful dentists!

However, things aren't as bad as all that. On the one hand, nowadays there are graphical interfaces even for Linux, which are equal to what Windows or Mac-OS X have to offer, or in some respects even surpass these as far as convenience and power are concerned. On the other hand, graphical interfaces and the text-oriented command line are not mutually exclusive, but in fact complementary (according to the philosophy "the right tool for every job").

At the end of the day this only means that you as a budding Linux user will do well to *also* get used to the text-oriented user interface, known as the "shell". Of course nobody wants to prevent you from using a graphical desktop for everything you can do. The shell, however, is a convenient way to perform many extremely powerful operations that are rather difficult to express graphically. To reject the shell is like rejecting all gears except first in your car$^{1}$. Sure, you'll get there eventually even in first gear, but only comparatively slowly and with a horrible amount of noise. So why not learn how to really floor it with Linux? And if you watch closely, we'll be able to show you another trick or two.

# 4.1.1 What Is The Shell?

Users cannot communicate directly with the operating system kernel. This is only possible through programs accessing it via "system calls". However, you must be able to start such programs in some way. This is the task of the shell, a special user program that (usually) reads commands from the keyboard and interprets them (for example) as commands to be executed. Accordingly, the shell serves as an "interface" to the computer that encloses the actual operating system like a shell (as in "shellfish"—hence the name) and hides it from view. Of course the shell is only one program among many that access the operating system.

![](bbox=[0.31, 0.6, 0.35, 0.63])

Even today's graphical "desktops" like KDE can be considered "shells". Instead of reading text commands via the keyboard, they read graphical commands—via the mouse—but as the text commands follow a certain "grammar", the mouse commands do just the same. For example, you select objects by clicking on them and then determine what to do with them: opening, copying, deleting, ...

Even the very first Unix—and-1960s vintage—had a shell. The oldest shell to be found outside museums today was developed in the mid-1970s for "Unix version 7" by Stephen L. Bourne. This so-called "Bourne shell" contains most basic functions and was in very wide-spread use, but is very rarely seen in its original form today.

+   * Borne shell
+   * C shell
+   * Korn shell
+   * Bourne-again shell

Other classic Unix shells include the C Shell, created at the University of California in Berkeley and (very vaguely) based on the C programming language, and the largely Bourne-shell compatible, but functionally enhanced, Korn shell (by David Korn, also at AT&T).

Standard on Linux systems is the Bourne-again shell, bash for short. It was developed under the auspices of the Free Software Foundation's GNU project by Brian Fox and Chet Ramey and unifies many functions of the Korn and C shells.

> $^{1}$This metaphor is for Europeans and other people who can manage a stick shift; our American readers of course all use those wimpy automatic transmissions. It's like they were all running Windows.