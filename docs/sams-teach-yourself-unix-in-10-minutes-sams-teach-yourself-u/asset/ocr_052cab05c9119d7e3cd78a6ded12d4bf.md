# LOGGING OUT FROM A KDE SESSION

If you logged in to the UNIX system through the KDE graphical interface, you can point and click your way out of the system. To log out:

+   1. Click the K symbol, which pops up the main KDE menu.
+   2. Select Logout from the menu
+   3. KDE prompts you and tells you that it is ready to close your session. Click the Logout button to complete the process.

# THE UNIX COMMAND PROMPT

You're probably wondering what use UNIX is going to be to you if all you can do is log in and log out. Patience! UNIX can be a bit overwhelming if approached too quickly. The power of UNIX comes from its wealth of built-in utilities and the way that processes can be combined to perform tasks that might require customized programming on another operating system. For example, suppose you're running a Web server on your UNIX computer and you want to count the number of accesses from a machine named kiwi. If you're a programmer, it isn't too difficult to write a program to do this—but with UNIX you don't need to! Instead, you can just enter a command such as this:

```
>grep "kiwi" /var/log/httpd/access.log ; wc -l
```

This example uses grep, a program that finds patterns, to find all the lines in the Web server log which contain kiwi; it then hands the results to we, a program which counts things. Obviously, you aren't expected to know how to construct this command yet—but you will be capable of doing so by the end of the book.

When you are typing commands into UNIX, you are typing them into what is known as a shell. For all the old DOS users out there, a shell is sort of like a version of Command.Com—on steroids. If you remember the days of DOS, you probably also remember different DOS shells that added capabilities to your computer. UNIX has a wide variety of shells that you can use, each offering a different set of capabilities. In addition to giving the user a place to run commands, shells also provide a scripting language that is much like a DOS batch file, but far more capable.

Programs written using a shell are called shell scripts.