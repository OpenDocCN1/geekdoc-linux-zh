# # Chapter 1: FreeBSD Requirements

# ## FreeBSD INSTALLATION

> ### Note
> 
> *The word* ***server*** *can refer to either the entire computer or to a specific program that runs on the computer to provide the specific server functionality. One consequence of this fact is that a single computer can provide multiple network server functions. For instance, a single system might run a web server and a mail server. In most cases, the meaning of the term* ***server*** *(in reference to a computer or a program) *should* *be clear from context. When the meaning might not be clear, I elaborate by referring to a* ***server computer*** *or a* ***server program****.

Another advantage of FreeBSD as a server OS is FreeBSD’s excellent reliability. Despite the fact that x86 hardware is quite varied and sometimes not as reliable as the hardware used in traditional server computers, such as those made by Sun or Silicon Graphics (SGI), FreeBSD is quite stable. It’s not uncommon to find a FreeBSD server that’s been running continually for months without problems. Reboots are often done to perform hardware upgrades rather than to upgrade an individual software package or to work around a problem that’s causing flaky behavior. Because many computers rely upon a server computer, this high reliability is very important in a server OS.

Server computers need efficient and reliable networking subsystems. These include the individual server packages that they run, as well as core OS features, such as drivers for network cards and the *Transmission Control Protocol/Internet Protocol* (*TCP/IP*) *stack*, which is the part of the OS’s kernel that’s responsible for managing network functions. The FreeBSD TCP/IP stack is well respected and efficient. It also includes security features that enable you to implement a *packet-filter firewall* with FreeBSD. This topic is covered in Chapter 17. A packet-filter firewall enables you to block individual network packets based on features such as the source and destination IP addresses. Such features, which are increasingly common and sophisticated in modern OSs, are vital for servers, which often come under attack. Many individual FreeBSD server programs also include important security features aside from FreeBSD’s packet filtering capabilities.

# ## FreeBSD vs. Non-UNIX OSs

In deciding which OS to run, you’re faced with specific choices. If FreeBSD is one of your choices (as presumably it is if you’re reading this book), then you can classify other potential choices in two groups: non-UNIX-like and UNIX-like. This section describes the options in the first group, and *summarizes* FreeBSD’s strengths and weaknesses compared to each. FreeBSD is a UNIX-like OS. If you’re casting your OS net widely at first, you may want to first decide whether or not to run a UNIX-like OS, and then settle on the specific UNIX-like OS if you decide to take that route.

The range of OSs available today is quite broad—so broad that this section can’t cover all of them. Instead, this section focuses on the most popular (and some not-so-popular) OSs that run on common low-end hardware (x86 and PowerPC CPUs):

+   1. **DOS** The *Disk Operating System* (DOS) was the original OS for the IBM PC, and it’s still available today in various forms. All of these forms are primitive and limited compared to modern OSs. Their main advantages are their small