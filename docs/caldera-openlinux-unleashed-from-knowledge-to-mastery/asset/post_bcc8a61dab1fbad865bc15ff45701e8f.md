
The last two chapters briefly cover C and C++ development and the GNU compiler tools. If you are familiar with C or C++ programming in other environments, these chapters will teach you how to develop under Linux.

## Part VI: Appendixes

Appendix A is a list of useful UNIX commands. You should know them before you attempt to administer a Linux system. Appendix B describes how to install Caldera OpenLinux. Appendix C is an annotated bibliography—you'll soon learn that understanding Linux requires a lot of reading.

### Conventions Used in This Book

The following typographic conventions are used in this book:

- Code lines, commands, statements, variables, and any text you type or see onscreen appears in a mono typeface. Bold mono typeface is often used to represent the user's input.
- Placeholders in syntax descriptions appear in an italic mono typeface. Replace the placeholder with the actual filename, parameter, or whatever element it represents.
- Italics highlight technical terms when they're being defined.
- The ➤ icon is used before a line of code that is really a continuation of the preceding line. Sometimes a line of code is too long to fit as a single line on the page. If you see ➤ before a line of code, remember that it's part of the line immediately above it.
- The book also contains Notes, Tips, and Cautions to help you spot important or useful information more quickly. Some of these are helpful shortcuts to help you work more efficiently.

## Essential OpenLinux

### Part I

### In This Part

- 1 Introduction to Caldera OpenLinux 7
- 2 Basic Linux Concepts and Commands 23
- 3 Using the Shell 55
- 4 Using X Window System 79
- 5 Exploring KDE 111
- 6 Text Editors 135

## Introduction to Caldera OpenLinux

### 1 CHAPTER

### IN THIS CHAPTER

- What Is Linux? 8
- Why Linux? 14
- Linux Features 16
- Caldera OpenLinux 18
- Sources of Linux Information 19
- Hardware Requirements 20
- Going Ahead with Linux 21

### What Is Linux?

Linux is a robust UNIX-like network operating system, which has taken the computing community by storm. This book will teach you how to get the most out of your Caldera OpenLinux system. It will also give you enough background to feel confident with any version of Linux and indeed most brands of UNIX.

Before starting the technical discussion, it is worthwhile to review the history of Linux. Linux is part of a strong UNIX tradition that dates back almost 30 years. Much of this rich and colorful history has influenced Linux design decisions, so being aware of it will help you understand the philosophy behind Linux and the approaches taken to implementing various pieces of functionality.

## The History of UNIX

### Birth

In the late 1960s, AT&T’s Bell Telephone Labs was working on a time-sharing computer system known as Multics. Prior to Multics, most computer systems operated in batch mode. Users would submit jobs to a queue and come back the next day to see what had happened. Multics, on the other hand, allowed users to sit in front of terminals and interact with the system. Each user was given a time slice of computing time. This allowed real-time interaction with the computer and a much faster realization and correction of errors.

Multics was a very ambitious project—too ambitious, in fact—and became unmanageable. Although its users appreciated the time-sharing concept, the project was unsustainable.

In 1969, Ken Thomson and Dennis Ritchie began implementing an operating system on a DEC PDP-7. It borrowed some good ideas from Multics but was a much smaller system. In 1970, Brian Kernighan dubbed it “UNIX” as a sarcastic play on the word “Multics.” Thus began the operating system we know today, as well as the tradition of word-play in the naming of UNIX commands and functions.

Originally, UNIX (like most operating systems of the day) was written in assembly language (a very low-level language specifying each microprocessor instruction). By 1973, after creating the language B (derived from an earlier language called BCPL), Brian Kernighan and Dennis Ritchie invented a language called C, and the UNIX kernel was rewritten in C. (The *kernel* is the core of an operating system; it controls memory allocation, process scheduling, resource management, and hardware drivers.) Writing an operating system in a high-level language was a major innovation and a huge contributor to the proliferation of UNIX—a system written in C is orders of magnitude easier to port to new architectures than one written in assembly language.

### Adolescence

In 1973, Thomson and Ritchie presented a paper on UNIX at the Symposium for Operating System Principles, and interest in the system was phenomenal. At the time, AT&T was under antitrust investigation and was barred from entering the computer market. However, AT&T lawyers approved the release of UNIX to universities under the conditions that there would be no promotion, no guaranteed bug fixes, and no support.

Universities eagerly adopted the system. Because of AT&T's release policies, UNIX users had to band together to support each other. This led to a long-standing UNIX tradition of sharing and collaborating. UNIX users are loyal to the system as much because of the values instilled by UNIX's history as because of the system's technical merits.

In 1975, Ken Thomson returned to the University of California at Berkeley and brought UNIX with him. Two graduate students, Bill Joy and Chuck Haley, began working on the system, with Joy authoring the Vi full-screen text editor. Out of the work at Berkeley, the Berkeley System Distribution (BSD) version of UNIX was created.

In 1979, AT&T realized it had a valuable product and changed the licensing terms of UNIX. Its source code could no longer be used by universities in operating systems courses, UNIX was suddenly a business product, not a community good to be shared freely. This period also marked the end of hobbyist computing and the free sharing of software and the beginning of the serious PC software market.

### Adulthood

Until the early 1980s, UNIX was derided as a rogue operating system mostly used by college students, not a serious environment for work. Large computer companies had their own proprietary (and incompatible) systems, and users of these systems were locked in.

However, in the 1980s, a new class of computer began encroaching on the minicomputer's territory: the scientific workstation offered lots of processing power in a small box on a worker's desk. The first workstations used proprietary operating systems, but a startup known as Sun Microsystems took the radical approach of offering UNIX workstations. Within a few years, other vendors like Silicon Graphics, Hewlett-Packard, and even IBM and DEC offered UNIX workstations. UNIX wiped out proprietary competition in the workstation market and destroyed the minicomputer market. UNIX was set to explode.

![](img/df365d352a104b50fea29e59a052de4d_46_0.png)

### Midlife Crisis

Unfortunately, UNIX had begun to splinter. Each manufacturer offered slightly different versions of UNIX with minor incompatibilities. Although the incompatibilities really were minor, managers who may not have understood computers saw a confusing mess when they looked at UNIX. Some vendors offered UNIX with a BSD heritage, whereas others were derived from AT&T’s “official” System V UNIX.

In the late 1980s and early 1990s, the computing power of PCs began to approach that of UNIX workstations. Although PCs were saddled with DOS and early versions of Windows, they quickly became a standard for business computing. Before the UNIX vendors could react, their “next big market” had been swallowed whole by Microsoft and the personal computer.

UNIX vendors formed alliances to combat this threat, but the alliances were shaky at best and simply wasted energy. All the while Windows’ market share was increasing. Windows even began to threaten UNIX’s supremacy in the scientific and server market.

### Maturity

During this period, members of the UNIX community had become unhappy with AT&T’s licensing terms and had begun several projects to produce a less-restrictive version of UNIX.

P. J. Plaugher’s Idris project and Andrew Tanenbaum’s Minix were aimed at replacing the UNIX kernel. BSD developers began replacing all AT&T code in their system with code written from scratch.

At the same time, another group took a different approach. In 1983, Richard Stallman founded the Free Software Foundation and began the GNU Project. (GNU is a self-referencing acronym that stands for GNU’s Not UNIX.) Rather than starting with the kernel, GNU began writing free replacements for the system utilities such as compilers, editors, and utility commands. After years of effort, GNU versions of practically every UNIX system program existed. The GNU software was of such high quality that even users of commercial UNIX systems routinely replaced the vendor utilities with the GNU utilities.

By the mid-1990s, the splinters in UNIX had largely been repaired. Standards such as those developed by the IEEE’s (Institute of Electrical and Electronic Engineers) POSIX committees and the ANSI/ISO committees legally unified the various flavors of UNIX.

However, Microsoft had by then grown into the world’s largest software company and was aggressively pursuing UNIX’s market with its new Windows NT operating system. Microsoft owned the desktop and was targeting the server room, promising a uniform interface and a universal de facto standard. UNIX’s future was in question.
