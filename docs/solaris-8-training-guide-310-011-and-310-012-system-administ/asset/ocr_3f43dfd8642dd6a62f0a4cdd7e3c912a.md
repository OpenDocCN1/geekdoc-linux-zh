+   - SunOS. Sun’s early operating system and the best-known BSD operating system.
- Solaris. Sun’s SRV4 implementation, also referred to as SunOS 5.x.
- HP-UX. Hewlett-Packard’s version of UNIX. HP-UX 9.x was System V, release 3, and HP-UX 11i is based on the System V, release 4 OS.
- Digital UNIX. Digital Equipment’s version of OSF/1.
- IRIX. The Silicon Graphics version of UNIX. Early versions were BSD-based; version 6 was System V, release 4.
- AIX. IBM’s System V-based UNIX.
- Linux. A free UNIX operating system for the INTEL platform; it was quickly gaining a hold in the UNIX community. Versions of Linux became available on Sun, HP, and IBM systems.

With the uncontrolled proliferation of UNIX versions, standards became a major issue. In 1993, Sun announced that it was moving to System V in an effort to promote standards in the UNIX community. With two major flavors of UNIX, standards could not become a reality. Without standards, UNIX would never be taken seriously as a business computing system. Thus, Sun developed BSD, but provided its users with System V, release 4, shrink-wrapped directly from AT&T. In addition, any applications developed by Sun to be added onto UNIX were to be SRV4-compliant. Sun challenged its competitors to provide true portability for the user community.

The Graphical User Interface (GUI) was the next wave in the development of the UNIX operating system. As each hardware vendor tried to outdo the others, ease of use became an issue. Again, in this area especially,

standards were important. Applications that were to be portable needed a GUI standard. Therefore, Sun and AT&T started promoting OPEN LOOK, which they jointly developed. Their goal was to create a consistent look and feel for all flavors of UNIX; unfortunately, OSF had its own GUI called OSF/MOTIF. Thus, round two of the fight for standards began, with MOTIF beating out OPEN LOOK.

MOTIF was based on a GUI developed at MIT named the X Window System, which allowed a user sitting at one machine to run programs on a remote machine while still interacting with the program locally. X was, in effect, one way for different systems to interface with each other. X allowed a program run on one computer to display its output on another computer, even when the other computer was of a different operating system and hardware architecture. The program displayed its output on the local machine, and accepted keyboard and mouse input from the local machine, but it executed on the CPU of the remote machine.

The local machine was typically a workstation or terminal called a dedicated X terminal, and was built specifically to run the X Window System. The remote machine might be a minicomputer or server, a mainframe, or even a supercomputer. In some cases, the local machine and the remote machine might, in fact, be the same. In summary, X was a distributed, intelligent, device-independent, operating-system-independent windowing system.

As stated earlier, MOTIF beat OPEN LOOK in the standards war. Sun conceded, and started to provide a package that contained both OPEN LOOK and MOTIF—called the Common Desktop Environment (CDE)—as standard equipment beginning with Solaris 2.5.1.