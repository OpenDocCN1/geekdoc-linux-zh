# **Linux doesn't have the software I need.**

It depends on what type of software you need. If you're looking for a custom application to run a specific type of business (inventory management for veterinarians who specialize in parrots), yeah, you're probably going to be out of luck.

But if you're looking for generic desktop-type applications, you may find this to be less true than you think. There are open-source equivalents to virtually all popular Windows applications, and most of them come packaged with the top Linux distributions.

# **Linux won't run my Windows software.**

Okay, so you've got a piece of software that runs only on Windows, and it's not getting ported to Linux in the foreseeable future. Perhaps it's a vertical-market application that is tied tightly into the Windows API. Or perhaps it's a horizontal application but one that doesn't have a Linux equivalent.

Fear not. There are a couple of ways to run Windows software on a computer that has Linux installed on it. The first is an open-source software application called WINE (or its commercial equivalent, Crossover Office), and the second is a tool called VMware that runs Windows and Windows applications natively.

WINE is a program installed on a Linux computer. After it's installed, a Windows program is installed "on top of it." The Windows program runs on top of WINE. WINE translates all of the Windows operating system calls into the equivalent Linux operating system calls. As a result, the Windows program never knows it's running on a Linux computer. WINE can be tricky to install and configure, though. Crossover Office is a wrapper for WINE; it handles all of the installation and configuration issues, and works virtually flawlessly. And Transgaming's version of WINE, WINE X, lets you run a bunch of the most popular Windows games under Linux.

VMware is a piece of software that emulates a second computer, completely through software. After installing VMware, you can install a second operating system within VMware. Then, while running that second OS, you install applications that are native to that OS, just as if it were the only OS on the computer. While somewhat resource intensive, VMware provides a mechanism for you to run Windows applications perfectly on a Linux machine.

# **You have to use the command line.**

The command line is the Linux equivalent to what Windows power users think of as a "Command Box" or a "DOS Box." For those of you who grew up with MS-DOS, the command line isn't as intimidating as for those who grew up with a GUI. In either case, while the command line can be useful at times, it is rarely needed anymore for day-to-day use.

# **You have to compile everything.**

In the early days of Linux, most software came packaged simply as source code, which meant in order to use it, you had to compile it first to create an executable binary (the program itself), and then install the binary itself.

Realizing that more and more users wanted to simply use the software without a lot of fuss, software developers began taking advantage of the installation features provided by various distributions. Red Hat's RPM, SuSE's YUM, and Debian's apt-get mechanisms make installing a new software package as easy as double-clicking on a file or running a command or two at the "command line."