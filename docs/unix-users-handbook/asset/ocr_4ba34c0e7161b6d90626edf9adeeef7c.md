```
nispasswd nispasswd (1) - change NIS+ password information
nispasswd nispassdwd (1m) - NIS+ password update daemon
nispasswd passwd (1) - change login password and password attributes
nispasswd passwd (4) - password file
nispasswd pwcovy (1m) - installs and updates /etc/shadow
nispasswd with information from /etc/passwd

rpc.nispassdd rpc.nispassdd (1m) - NIS+ password update daemon
rpc.ypasswd rpc.ypasswd (1m) - server for modifying NIS password file
yppasswd yppasswd (1) - change your network password in the NIS database
ypassdd rpc.ypassdd (1m) - server for modifying NIS password file
```

This command produces a long list of "man" pages from a database, including sections 1 and 4 for passwd that our find command produced. In order to use the "-k" option, a "man" page database must have been produced by your system administrator by issuing the catman command.

I am obviously a big advocate of using "man" pages, because I included many "man" pages at the end of chapters throughout the book. Anytime you see the "man" page icon, there is a "man" page for the command in the chapter number referenced in the icon. Although the "man" page for your UNIX variant may be different from the one appearing in the book, the commands on most UNIX variants are similar, and the "man" pages act as an excellent reference.

# Electronic Mail

All UNIX variants come with electronic mail programs. You can use one of the electronic mail programs on your system to send and receive electronic mail from other users on the system. You can also communicate with users on other systems and across the internet if your system administrator has set up this capability. In this chapter, we'll cover the basics of sending and receiving electronic mail. I cover this very early in the book because you may receive a message after your first login indicating that you have received mail messages and you'll want to read them. You may receive a welcome message or a request to change your password immediately after your first login.

The most basic electronic mail program, and one that exists on every UNIX variant on which I have worked, is mail. This is a very easy program to use that requires very little explanation. In the following example, I invoke the mail program, issue "?" to print a list of

![](bbox=[0.85, 0.22, 0.95, 0.3])

![](bbox=[0.85, 0.31, 0.95, 0.4])