
- Delay fixing a system problem or helping an employee with a simple question.
- Neglect security measures that would protect sensitive data.

These actions are unethical because they invade others' privacy and impede the work of your employer. Most are also illegal and would make an unscrupulous system administrator subject to criminal prosecution. But as you might suspect, some unethical actions are likely to go undetected, especially if you are the sole person in a company with expertise in Linux.

![](img/43f64015de86d989e30eff5bb284fb96_49_0.png)

An excellent resource on legal issues related to technology is www.gigalaw.com.

To have a successful career as a system administrator, you should decide at the outset on a few guidelines for your relationships with employers and the fellow employees whose systems you manage. Your self-made guidelines might include statements such as these:

- I realize that I know more about the systems I manage than others, but I also realize that they know more about their job functions and what they need from their computer systems.
- I understand that other employees and managers trust me to handle their technology needs so they can be productive.
- I know I can never read files that do not belong to me personally unless I am required to do so as part of a legal proceeding or to comply with a publicly acknowledged company policy.
- I must treat other employees as my clients. My success as a system administrator depends on their satisfaction with my work, not on how much I know about technology.

Occasionally, a rogue system administrator decides to configure systems so that no one else can figure out how everything is put together. This is sometimes done in the name of job security: "They can't fire me," this kind of system administrator reasons, "or the entire company will have to shut down."

In fact, however, your best route to success as a system administrator (not to mention peace of mind) comes through making your employer successful. This allows you to grow professionally by accepting additional responsibility and embracing technical opportunities. If you train yourself well, you need never feel compelled to make implied threats of holding your employer "hostage" because you are the only person who can maintain the computer systems. Remember these two rules:

- Good jobs are always available for well-trained technical people; don't base ideas of job security on working at a single company. Instead, build a reputation as both a technical expert and a personable employee so that potential future employers will be eager to hire you and past employers will be sorry they lost you.
- If you haven’t trained yourself well, you’re not worth keeping as an employee. Your employer can then replace you with someone who is not being territorial under the guise of "job security." The true expert is always able to set up efficient, standardized, well-documented systems and have a solid career based on managing those systems.

To read more about working as a system administrator, visit the System Administrators Guild (SAGE) at www.sage.org. SAGE is part of the USENIX group, an organization for people who work with advanced computing systems (see www.usenix.org). USENIX and SAGE have tremendous resources for system administrators.

![](img/43f64015de86d989e30eff5bb284fb96_50_0.png)

In relation to the topics in this section, consider reviewing the SAGE Code of Ethics at http://sageweb.sage.org/resources/publications/code_of_ethics.html.

## STARTING TO USE LINUX

In this section, you start using Linux. Ideally, you should have access to a computer with Linux installed as you read these sections.

![](img/43f64015de86d989e30eff5bb284fb96_50_1.png)

If you are not working in a classroom or lab, you may need to jump ahead to Chapter 8 ("Installing Linux") to install Linux yourself. Because installation is a fairly advanced topic, several chapters of foundational material are provided so you can better understand the installation process.

### Logging In

Before you can do anything in Linux, you must log in to the system. When you log in, you identify yourself to the operating system so that it knows you are authorized to use the system, and which parts of the system to permit you to access. Unlike some older versions of Windows that you might have used, you cannot access any features of Linux without logging in.

Each person who uses a Linux system typically has his or her own user account. A user account is a set of permissions to use the system, with an associated user name and password. You must have a valid user name and password in order to log in. If you are working in a classroom or lab, your instructor should provide you with a user name and password. If you have installed your own Linux system, you should have created a user account (with a user name and password) when you installed Linux.

Linux operates in two modes: graphical and text. The text mode provides only a simple prompt at which you type your user name, press Enter, then type your password and press Enter. If you log in using a valid user name and password, you see a command-line prompt such as this:

[nwells@inverness nwells]$

At this prompt, you can enter commands to start programs or interact with the system. An explanation of each part of this prompt is provided later in this chapter. When you are working in this mode, you are using a console.

More commonly, you log in to Linux using a graphical login screen. This screen appears automatically after you turn on the Linux-based computer (after many lines of start-up information scroll by). When you enter your user name and password in the text boxes provided, you see a graphical desktop, similar to the one shown in Figure 1-5. This desktop interface is your main working environment.

![](img/43f64015de86d989e30eff5bb284fb96_51_0.png)

Figure 1-5 The GNOME desktop interface

### Graphical Environments

The desktop interface used by default on all major Linux distributions is very similar to the interface of any Microsoft Windows or Apple Macintosh computer. The Linux desktop interface can be reconfigured in many ways (as described in later chapters), but its basic operation is straightforward. Two different desktops are popular on Linux systems: the KDE desktop and the GNOME desktop (guh-NOME). Both of these desktops include the following basic features:

- A taskbar containing numerous icons across the bottom of the screen
- A main menu that you access by clicking on the icon in the lower-left corner of the screen (at the same location as the Start button in Microsoft Windows operating systems)
- Multiple levels of menus that group programs together by subject
- Desktop icons that you can double-click to access commonly used programs
- Multiple overlapping windows that you control using your mouse. Each window can be moved, resized, and so forth.

### Opening a Terminal Window

From within the graphical desktop (the GUI, or the desktop), you can start a text-mode interface—a terminal window—that resembles a console. From this window you can enter commands from the keyboard.

> A terminal window is also known by other names: a command-line interface (CLI) or an xterm window. Xterm (EX-term) is the name of one popular program that provides a terminal window in UNIX and Linux.

To start a terminal window in Red Hat Linux, click the main menu button in the lower-left corner of the desktop—it is the icon with a Red Hat on it. When the menu appears, click System Tools, and then click Terminal on the submenu that appears. A terminal window appears. You can also open a Terminal window by right-clicking the background of the desktop and selecting Open Terminal from the context menu that appears. You can open as many terminal windows as you want by repeating these steps. (See Figure 1-6.)

## EXPLORING THE FILE SYSTEM

Manipulating files and directories is a large part of what you do on a computer, whether as a regular user or as a system administrator. For example, you search directories for a file, you open that file to review or change its contents, and you save an updated version of the file. This section describes some basic concepts and tools (both text-based and graphical) that enable you to access files on a Linux system.
