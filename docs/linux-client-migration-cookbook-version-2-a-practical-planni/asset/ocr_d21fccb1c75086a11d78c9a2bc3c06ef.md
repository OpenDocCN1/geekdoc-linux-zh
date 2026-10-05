# 5.2.3 Multi-user

The way in which users are used in Linux is based on the model of UNIX. Since UNIX was developed as a multi-user operating system from the start, the concept of multiple users is very tightly bound to the workings of the operating system. The Windows operating system originally started as a single-user, single-thread operating system. Since then, Windows has come a long way. Because of this difference in history, there are inherent differences between the way multiple users are handled by both operating systems.

There are several different ways to look at how good an operating system handles multiple users:

+   - Multiple users run processes at the same time?
- Can multiple users be logged on at the same time?
- Can applications be installed for multiple users?
- What are the rights of the different users?

> Note: Useful's multi-station client computing solution is an excellent example of how to leverage the multi-user flexibility in the Linux OS and the X architecture. See 7.5, "Multi-station client architecture" on page 162 and Appendix D, "Multi-station computing deep dive using Useful Desktop'" on page 289 for more details.

# Can multiple users run processes at the same time

One way to look at multi-user is that more than one user can run processes at the same time. In Linux, usually all system processes run as the root user. Any number of users can have processes running on a Linux system at the same time. The number can be limited by specific tables in the kernel, but in essence the code enables any number.

In Windows, it is also possible to have processes running for multiple users at the same time. This property is the basic building block for the Windows Terminal Server.

# Can multiple users be logged on at the same time

In the case of both operating systems, the answer to this question is yes. Multiple users can be logged on at once.

If a login consists of having a console with a graphical display, this is also possible in both operating systems. In Windows, this is done using Terminal Server and a Remote Desktop Protocol (RDP) connection. In Linux, this is done by allowing the session manager to create screens on Xservers.