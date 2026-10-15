
3. The design of the system allowed users to run multiple processes concurrently and to connect these processes with IPC channels, including pipes, FIFOs, and sockets, as discussed in Section 1.7.2. We present the implementation of this design aspect in Chapter 9.

## 1.8.3 AT&T System V

In response to the changing business environment in the early 1980s, Bell Laboratories/AT&T licensed further releases of UNIX as System III and finally as System V, starting in 1983. This main branch of UNIX continued to be developed, as shown in Figure 1.3, through System V, Release 4 (SVR4), when it again diverged and evolved to survive as SCO UNIX in the mid- to late 1990s. Currently, there are four major System V-based UNIX systems: AIX 7.x, OpenServer 6.x, UnixWare 7.x, Solaris 11.x, OpenSolaris and its variants, and HP-UX 11i v3.

## 1.8.4 Berkeley Software Distributions

The University of California at Berkeley initiated and maintained the development of UNIX along its second main branch throughout the 1980s and into the 1990s. Contractual agreements made the operating system freely available to universities, so these releases contributed in large part to the popularization of UNIX. These versions were released as Berkeley Software Distributions (BSD), 3BSD, and 4BSD-4.4BSD. Most recently, BSD UNIX survives as FreeBSD, and its offshoot PC-BSD, OpenBSD, and NetBSD. Today, the most popular variants of BSD UNIX are FreeBSD 10.x, OpenBSD 5.x, NetBSD 6.x, and Mac OS X 10.9.x (Darwin).

In this book, we show example commands primarily under PC-BSD. Where appropriate, we also discuss features of Solaris.

## 1.8.5 History of Shells

The development of the shell as a UNIX utility parallels the development of the system itself. Steven R. Bourne wrote the first commercially available shell, the Bourne shell. Available in the seventh edition in 1979, it is the default shell on many System V versions. The C shell, written in the late 1970s primarily by Bill Joy, was made available soon after in 2BSD. When introduced, it provided a C program-like programming interface for writing shell scripts. Following the development of the C shell, the Korn shell was introduced officially in SVR4 in 1986. Written by David Korn of Bell Laboratories, it included a superset of Bourne shell commands but had more functionality. It also included some useful features of the C shell. We discuss the development history of the UNIX shell in a bit more detail in Chapter 2.

The three major shells have slightly different features and command sets. In this textbook, we discuss common features and command sets for all UNIX shells and versions. Whenever we discuss a feature or command that is particular to a shell or version, we state that specifically.

## 1.8.6 Current and Future Developments

Probably the most exciting and challenging current UNIX development for all other flavors of UNIX (besides Solaris and FreeBSD) focuses on the incorporation of the ZFS into the kernel, and having the boot disk use ZFS. ZFS was developed by Sun Microsystems in the years prior to its incorporation into the Solaris family in 2006. It is now the standard file system in only Solaris (and its noncommercial equivalent, OpenIndiana) and FreeBSD (and its offshoot PC-BSD). Since the purchase of Sun by Oracle, the source development of ZFS has proceeded basically along two branches: the Oracle Solaris branch and the open branch.

Another major challenge on the horizon for UNIX systems is the incorporation of systemd into the kernel. Currently, systemd is a suite of system management daemons, libraries, and utilities designed as a central management and configuration platform for Linux. systemd is used on a majority of the current implementations and official releases of the Linux kernel. It is a Linux init system (the process called on by the Linux kernel to initialize the user space during the Linux startup process and manage all processes afterwards), thus replacing the UNIX System V and BSD-style init daemon. The name systemd adheres to the convention of making daemons easier to distinguish by having the letter d as the last letter of the filename. Whether or not systemd will be incorporated into the UNIX kernel remains to be seen.

Finally, the replacement of the X Window System protocol by various other software systems promises to yield a smaller, more effective GUI system. Wayland is a protocol that specifies the communication between a display server (called a Wayland compositor) and its clients, as well as a reference implementation of the protocol in C.

## 1.9 VARIATIONS IN UNIX SYSTEMS

As shown in Figure 1.3, the development of the UNIX systems proceeded along three main branches from a single core. Many of the branches’ divergences and similarities were caused by the Bell Laboratories and AT&T legal licensing arrangements during the 1970s and 1980s. The primary advantage of the divergences was a command- and function-rich operating system in each of the branches. The early Bell Labs releases were copied and distributed freely as source code, which academic and commercial users could easily modify to suit their hardware and software. Such adaptations led to a proliferation of ways in which various aspects of the operating system evolved. Even the later releases of System V and BSD could be modified easily via accommodations provided by the vendor of the operating system version, even if the source code was not available. Many of the later releases were compatibility releases meant to provide uniformity between any particular implementation and its perceived competitors. The important contribution of these compatibility releases and their offshoots is a helpful amount of homogeneity, regardless of whether you use a modern derivative of SVR4, Solaris, 4.4BSD, Linux, or Apple OS X.

Divergence has the drawback that programs and even commands that work on one version fail to work on another, thus defeating the inherent strength of user-friendliness of the system itself. Attempts have been made to standardize UNIX—for example, via the IEEE Portable Operating System Interface (POSIX). This software standard not only covers UNIX, but also in particular specifies program operation and user interfaces, leaving their implementations to the developer. Several standards have been adopted, and more
