
## 4 Part I: Getting Started in Fedora

*   Subscription service to RHEL that offers stable, tested software (much of the same software in Fedora that has gone through rigorous testing)
*   Multiple support programs, ranging from an online knowledge base to assistance with custom deployment, engineering, and software development to full 24x7 onsite support
*   Official documentation, training, and certification programs

Fedora itself has become a respected and active Linux distribution that thousands of people use worldwide as a desktop, server, or programming workstation. It is the best way to get the latest Linux software that is being built on a foundation for enterprise-quality systems.

Using Fedora is a great way to get a head start learning the features of upcoming RHEL releases. The latest Fedora Linux operating system (referred to as Fedora 12) is included on the DVD that comes with this book. The book also includes a Fedora Live CD with a desktop Linux system that you can use to try out Fedora, and then install directly to your hard disk when you are ready.

### Introducing Fedora 12

With the split between community (Fedora) and commercial (Red Hat Enterprise Linux) versions of what was Red Hat Linux, Red Hat has created a model that can suit the fast-paced changes in the open source software world, while still meeting the demands for a well-supported commercial Linux distribution.

Many technology professionals choose Red Hat Enterprise Linux because of its reputation for solid performance. With the Fedora Project, Red Hat has created an environment where open source developers can bring high-quality software packages to a freely distributed, community-oriented Linux system.

More than 15,000 individual software packages (compared to just over 600 in Red Hat Linux 6.2) are included in the single, massive Fedora 12 software repository. These packages contain features that would cost you thousands of dollars to duplicate if you bought them as separate commercial products. These features let you:

*   Connect your computers to a LAN or the Internet
*   Create documents and publish your work on paper or on the Web
*   Work with multimedia content to manipulate images, play music files, view video, and even master and burn your own CDs and DVDs
*   Play games individually or over a network
*   Communicate over the Internet using a variety of Web tools for browsing, chatting, transferring files, participating in newsgroups, and sending and receiving e-mail
*   Protect your computing resources by having Fedora act as a firewall or a router to protect against intruders coming in through public networks
*   Configure a computer to act as a network server, such as a print server, Web server, file server, mail server, news server, and a database server

This is just a partial list of what you can do with Fedora. Using this book as your guide, you will find that there are many more features built into Fedora as well.

Support for new video cards, network cards, printers, and storage devices is being added every day. Linux programmers around the world are no longer the only ones creating hardware drivers. Every day more hardware vendors are creating their own Linux drivers, so they can sell products to the growing Linux market. New applications are being created to cover everything from personal productivity tools to programs that access massive corporate databases.

Remember that old Pentium computer in your closet? Don't throw it away! Just because a new release of Fedora is out doesn't mean that you need all new hardware for it to run. Support for many old computer components get carried from one release to the next. With a minimal install, you could use Fedora as a router (to route data between your LAN and the Internet), firewall (to protect your network from outside intrusion), or file server (to store shared files on your LAN)—with maybe an Ethernet card or an extra hard disk added.

At this point, you may feel that Linux is something you want to try out. This brings us to the basic question: What is Linux?

### What Is Linux?

Linux is a free operating system that was created by Linus Torvalds when he was a student at the University of Helsinki in 1991. Torvalds started Linux by writing a kernel—the heart of the operating system—partly from scratch and partly by using publicly available software. (For the definition of an operating system and a kernel, see the sidebar “What Is an Operating System?” later in this chapter.) Torvalds then released the system to his friends and to a community of “hackers” on the Internet and asked them to work with it, fix it, and enhance it. It took off.

> NOTE: I make the distinction here between hackers (who just like to play with computers) and crackers (who break into computer systems and cause damage).

Today, there are thousands of software developers around the world contributing software to the free and open source software (FOSS) community that feeds the Linux initiative. Because the source code for the software is freely available, anyone can work on it, change it, or enhance it. Developers are encouraged to pass their fixes and improvements back into the community so that Linux can continue to grow and improve.

On top of the Linux kernel effort, the creators of Linux also drew on a great deal of system software and applications that are now bundled with Linux distributions from the GNU project (GNU stands for “GNU is Not UNIX”), which is directed by the Free Software Foundation (http://www.gnu.org). There is a vast amount of software that can be used with Linux, making it an operating system that can compete with or surpass features available in any other operating system in the world.

If you have heard Linux described as a free version of UNIX, there is good reason for it. Although much of the code for Linux started from scratch, the blueprint for what the code would do was created to follow POSIX (Portable Operating System Interface for UNIX) standards. POSIX is a computer industry operating system standard that every major version of UNIX complied with. In other words, if your operating system was POSIX-compliant, it was UNIX. Today, Linux has formed its own standards and services organizations to help interoperability among Linux systems, including the Linux Foundation, which supports such efforts as the Linux Standard Base (http://www.linuxfoundation.org).

### Linux’s Roots in UNIX

Linux grew within a culture of free exchange of ideas and software. Like UNIX—the operating system on which Linux is based—the focus was on keeping communications open among software developers. Getting the code to work was the goal and the Internet was the primary communications medium. Keeping the software free and redistributable was a means to that goal. What, then, were the conditions that made the world ripe for a computer system such as Linux?

In the 1980s and 1990s, while Microsoft flooded the world with personal computers running DOS (Disk Operating System) and Windows operating systems, power users demanded more from an operating system. They ached for systems that could run on networks, support many users at once (multiuser), and run many programs at once (multitasking). DOS and Windows didn’t cut it.

UNIX, on the other hand, grew out of a culture where technology was king and marketing people were, well, hard to find. Bell Laboratories in Murray Hill, New Jersey, was a think tank where ideas came first and profits were somebody else’s problem. A quote from Dennis Ritchie, co-creator of UNIX and designer of the C programming language, in a 1980 lecture on the evolution of UNIX, sums up the spirit that started UNIX. He was commenting on both his hopes and those of his colleagues for the UNIX project after a similar project called Multics had just failed:

> What we wanted to preserve was not just a good environment in which to do programming, but a system around which a fellowship could form. We knew from experience that the essence of communal computing as supplied by remote-access, time-shared machines, is not just to type programs into a terminal instead of a keypunch, but to encourage close communication.

In that spirit, the first source code of UNIX was distributed free to universities. Like Linux, the availability of UNIX source code made it possible for a diverse population of software developers to make their own enhancements to UNIX and share them with others.
