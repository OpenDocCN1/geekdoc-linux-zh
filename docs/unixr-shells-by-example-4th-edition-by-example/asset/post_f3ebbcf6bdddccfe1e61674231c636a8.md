
## EXAMPLE 1.1

```shell
$ cat /etc/shell
/bin/bash
/bin/sh
/bin/ash
/bin/bsh
/bin/tcsh
/bin/csh
/bin/ksh
/bin/zsh
```

## EXPLANATION

The /etc/shell (Linux) file contains a list of all shell programs available on your version of Linux. The most popular versions are bash (Bourne Again shell), tcsh (TC shell), and ksh (Korn shell).

**What Is POSIX?** In order to provide software standards for different operating systems and their programs, the POSIX standard (also referred to as the Open Systems Standards) evolved, consisting of participants from the Institute of Electrical and Electronics Engineering (IEEE) and the International Organization for Standardization (ISO). Their goal was to supply standards that would promote application portability across different platforms, to provide a UNIX-like computing environment; thus, new software written on one machine would compile and run on another machine with different hardware. For example, a program written for a BSD UNIX machine would also run on Solaris, Linux, and HP-UX machines. In 1988 the first standard was adopted, called POSIX 1003.1. Its purpose was to provide a C language standard. In 1992, the POSIX group established standards for the shell and utilities to define the terms for developing portable shell scripts, called the IEEE 1003.2 POSIX shell standard and general utility programs. Although there is no strict enforcement of these standards, most UNIX vendors try to comply with the POSIX standard. The term “POSIX compliancy,” when discussing shells and their general UNIX utilities, is an attempt to comply with the standards presented by the POSIX committee, when writing new utilities or adding enhancements to the existing ones. For example, the Bourne Again shell is a shell that is almost 100% compliant and gawk is a user utility that can operate in strict POSIX mode.

## 1.3 History of the Shell

The first significant, standard UNIX shell was introduced in V7 (seventh edition of AT&T UNIX) in late 1979, and was named after its creator, Stephen Bourne. The Bourne shell is a programming language is based on a language called Algol, and was primarily used to automate system administration tasks. Although popular for its simplicity and speed, it lacks many of the features for interactive use, such as history, aliasing, and job control.

The C shell, developed at the University of California, Berkeley, in the late 1970s, was released as part of BSD UNIX. The shell, written primarily by Bill Joy, offered a number of additional features not provided in the standard Bourne shell. The C shell is based on the C programming language, and when used as a programming language, it shares a similar syntax. It also offers enhancements for interactive use, such as command-line history aliases, and job control. Because the shell was designed on a large machine and a number of additional features were added, the C shell has a tendency to be slow on small machines and sluggish even on large machines when compared with the Bourne shell.

With both the Bourne shell and the C shell available, the UNIX user now had a choice, and conflicts arose over which was the better shell. To provide the best of both worlds, David Korn, from AT&T, invented the Korn shell in the mid-1980s. It was released in 1986 and officially became part of the SVR4 distribution of UNIX in 1988. The Korn shell, really a superset of the Bourne shell, runs not only on UNIX/Linux systems, but also on OS/2, VMS, and DOS. It provides upward compatibility with the Bourne shell, adds many of the popular features of the C shell, and is fast and efficient. The Korn shell has gone through a number of revisions. The most widely used version of the Korn shell is the 1988 version, although the 1993 version has gained popularity. Linux users may find they are running the free version of the Korn shell, called the Public Domain Korn shell, or simply pdksh, a clone of David Korn’s 1988 shell. It is free and portable and currently works in a wide variety of full compatible with its namesake, Korn shell, and to make it POSIX compliant. Also available is the Z shell (zsh), another Korn shell clone with TC shell features, written by Paul Falstad, and freely available at a number of Web sites.

With the advent of Linux, the Bourne Again shell (bash) gained popularity as a super Bourne shell. The Bourne Again shell was developed in 1988 by Brian Fox of the Free Software Foundation under the GNU copyright license and is the default shell for the Linux operating system. It was intended to conform to the IEEE POSIX 1003.2/ISO 9945.2 Shell and Tools standard. The Bourne Again shell also offers a number of new features (both at the interactive and programming level) missing in the original Bourne shell (yet Bourne shell scripts will still run unmodified). It also incorporates the most useful features of both the C shell and Korn shell. It’s big. The improvements over Bourne shell are command-line history and editing, directory stacks, job control, functions, aliases, arrays, integer arithmetic (in any base from 2 to 64), and Korn shell features such as extended metacharacters, select loops for creating menus, the let command, and more.

What is the TC shell? The TC shell is an expanded, completely compatible version of the C shell. Some of the new features are command-line editing (emacs and vi), scrolling the history list, advanced filename, variable, and command completion, spelling correction, job scheduling, automatic locking and logout, time stamps in the history list, and more. It is also big. People often ask, “What does the ‘T’ in TC shell stand for?” A little history is involved. Back in 1976, DEC announced and shipped a new virtual memory operating system called TOPS-20, based on TENEX, an operating system used by researchers at that time around the country. One of the most favored features among TOPS-20 users, and one most identified with TOPS-20 itself, was “escape recognition,” also called command completion. With this, the user can often get the system to, in
