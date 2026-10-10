# Sudo

The first command that we need to talk about before you start doing any of the other commands is "sudo." Sudo basically means "super user." In the previous chapters, we discussed how different distributions do things slightly differently, and that every single distribution of Linux has its own quirks; its own little ways of doing things depending on what the creators are worried about.

One of the things that the creators of Ubuntu Linux were worried about was security. As what we talked about before, in every Linux computer, there is a user called Root. Root is the highest level user on the computer. It is kind of like the administrator in a Microsoft Windows computer.

Just like on a Windows computer, if somebody logged in as the administrator, or somebody logged in as root on Linux, they can do absolutely anything they want to that computer. They can install viruses, malware, or spyware, or basically just cause a lot of havoc. Hackers, using special programs and scripts, can also try to login as Root and cause all these problems.

To alleviate the possibility of a hacker obtaining root access, the Ubuntu creators decided they never want anybody to login straight as Root. So in Ubuntu Linux, you cannot login as the user Root.

Now, here comes the problem. Since you cannot login as Root, how do you do all these administrative tasks then? How do you execute administrative processes? What they have is this program called sudo. It is basically a command prefix that tells the operating system that you want to run a particular process as the super user or root.

Sudo temporarily gives a user administrative access—root access—to execute an essential command in Linux. In the Windows operating system, sudo is the equivalent of the "Run as Administrator" option each time you want to run a program with administrative rights in Windows.