
...it even if you've never used Linux before, although you'll find it an easier read if you've at least casually used Linux for a few days. Although this book is geared toward LPIC-1 and Linux+ candidates, it's also a good and quick introduction to Linux for those who want to get up to speed on the OS but who don't intend to take either exam.

This book is written with the assumption that you know at least a little bit about Linux (what it is, and possibly a few Linux commands). I also assume that you know some basics about computers in general, such as how to use a keyboard, how to insert a floppy disk into a floppy drive, and so on. Chances are you have used computers in a substantial way in the past—perhaps even Linux, as an ordinary user, or maybe you have used Windows or Mac OS. I do *not* assume that you have extensive knowledge of Linux system administration, but if you've done some system administration, you can still use this book to fill in gaps in your knowledge.

As a practical matter, you'll need a Linux system with which to practice and learn in a hands-on way. LPIC topic 102 is titled “Linux Installation & Package Management,” and Linux+ domain 1.0 is titled “Installation,” but neither of the exams nor this book focuses on actually installing Linux on a computer from scratch, although some of the prerequisites (such as disk partitioning) are covered. You may need to refer to your distribution's documentation to learn how to accomplish this task.

## How This Book Is Organized

This book consists of seven phases plus this introduction. The phases are organized as follows:

- Phase 1, “Working on the Command Line,” covers the basic tools you need to interact with Linux. These include shells, redirection, pipes, the Vi editor, and basic file manipulation commands.
- Phase 2, “Managing Hardware and the Kernel,” describes x86 and x86-64 hardware and how Linux interacts with it. Specific tasks include setting BIOS options, using Linux tools to identify your hardware, configuring USB and disk devices, compiling a kernel, and managing the X Window System.
- Phase 3, “Managing Software,” covers the programs you'll use to manage software. Much of this phase is centered around the RPM and Debian package management systems. Additional tasks cover compiling software from source code, managing processes, and controlling the computer's startup scripts.
- Phase 4, “Documenting the System,” covers maintaining your own notes on the system's configuration, using log files created by the computer, and locating documentation on the computer itself and online.
- Phase 5, “Managing Partitions and Filesystems,” covers the tools used to manage partitions and the filesystems contained on them. Specific tasks include planning your partitions, creating partitions, creating filesystems, mounting and unmounting filesystems, maintaining filesystem health, and installing a boot loader.
- Phase 6, “Configuring Network Features,” is the largest phase in the book. It describes basic network configuration (bringing up a network connection, using a network connection, and so on), configuring routers and servers (routers, super servers, mail servers, Web servers, file sharing servers, and SSH servers), and printing.
- Phase 7, “Managing Security,” describes security tasks in Linux, including methods of blocking unwanted external access, setting user security restrictions, setting good passwords, and monitoring the system for security breaches.

Each phase consists of a series of numbered tasks. Each task includes several sections:

- **Scenario**: This section outlines a situation that would require use of the commands or features described by the task. It also introduces any fictitious hostnames, IP addresses, or other information that will be used as example data in the remainder of the task. You may need to change such fictitious identifiers for use on your own system or network, of course.
- **Scope of Task**: This section describes the probable time requirements; the necessary hardware, software, and preparatory setup steps; and any potential pitfalls or risks associated with the task.
- **Procedure**: You’ll read what to do to perform the task in this section. It’s broken down into subsections that vary with the specific task.
- **Criteria for Completion**: This section summarizes the task; you should verify that you’ve achieved each of the goals.

You should perform each task to acquire hands-on experience with Linux, helping you to understand how Linux works. I recommend you don’t stop there, though. This book provides you with the basics you’re likely to use most often, but most of the commands and features described by each phase’s tasks have greater depth than I can cover in the space allotted. Read the online documentation and, above all, try doing more with the commands. Only by using the commands and features yourself will you truly learn them well.

> **NOTE** A few tasks are highly system specific. For instance, Phase 3 includes tasks for installing software via both RPM Package Manager (RPM) and Debian package systems. Most Linux systems use just one of these two systems (in fact, using both is a bad idea), and a few use other systems entirely. Thus, you won’t be able to complete both of these tasks unless you have access to two Linux installations. If you can’t complete a task because you lack appropriate hardware or software or for any other reason, you should still read the task and do as much of it as you can do.

## Conventions Used in This Book

This book uses certain typographic styles in order to help you quickly identify important information and to avoid confusion over the meaning of words such as onscreen prompts. In particular, look for the following styles:

- *Italicized text* indicates key terms that are described at length for the first time in a chapter. (*Italic* is also used for emphasis.)
- A **monospaced font** indicates the contents of configuration files, messages displayed at a text-mode Linux shell prompt, filenames, text-mode command names, and Internet URLs.
- *Italicized monospaced text* indicates a variable—information that differs from one system or command run to another, such as the name of a client computer or a process ID number.
- **Bold monospaced text** is information that you’re to type into the computer, usually at a Linux shell prompt. This text can also be italicized to indicate that you should substitute an appropriate value for your system. (When isolated on their own lines, commands are preceded by non-bold monospaced `$` or `#` command prompts.)

In addition to these text conventions, which can apply to individual words or entire paragraphs, a few conventions highlight segments of text:

A note indicates information that’s useful or interesting but that’s somewhat peripheral to the main text. A note might be relevant to a small number of networks, for instance, or it may refer to an outdated feature.

![](img/f430a19bdf014c43ad7c2d594afd5b21_20_0.png)

A tip provides information that can save you time or frustration and that may not be entirely obvious. A tip might describe how to get around a limitation or how to use a feature to perform an unusual task.

![](img/f430a19bdf014c43ad7c2d594afd5b21_20_1.png)

Warnings describe potential pitfalls or dangers. If you fail to heed a warning, you may end up spending a lot of time recovering from a bug, or you may even have to restore your entire system from scratch.

![](img/f430a19bdf014c43ad7c2d594afd5b21_20_2.png)

## The Exam Objectives

Behind every computer industry exam you can be sure to find exam objectives—the broad topics in which exam developers want to ensure your competency. The LPIC and Linux+ objectives are very similar, which is why this book can cover both exams. They aren’t quite identical, though.

## LPIC Objectives

The official LPI objectives for the LPIC 101 and 102 exams are listed here. LPI breaks its certification into two exams, but you’re likely to take both exams on the same day. Certain topics are covered, to a different extent, in both the 101 and 102 exams.

Exam objectives are subject to change at any time without prior notice and at LPI’s sole discretion. Please visit the LPIC Certification page of LPI’s website ([http://www.lpi.org/en/lpic.html](http://www.lpi.org/en/lpic.html)) for the most current listing of exam objectives.

![](img/f430a19bdf014c43ad7c2d594afd5b21_20_3.png)
