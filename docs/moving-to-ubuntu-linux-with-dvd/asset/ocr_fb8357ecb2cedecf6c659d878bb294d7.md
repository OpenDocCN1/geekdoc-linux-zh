For those of you who may have used other Linux (or UNIX) systems, you may have had access to an account called root. This is the superuser account with ultimate power over the system. Ubuntu locks down the root account and does not allow a direct login. To execute commands with root privileges, Ubuntu makes use of the *sudo* command.

When you run a program with sudo (or gksudo), you are asked for your password to confirm access. After entering your password, your account can execute additional root-level commands for the next 15 minutes without having to reenter your password. That said, you still need to preface your commands with *sudo* or *gksudo*.

To run a command inside a GNOME terminal session, or a command shell, preface the command with *sudo*.

```
sudo command_name
```

From time to time, you may need to run several commands with root privileges. At those times, it may get a little tiring to prefix each and every command with *sudo*. To get around this, you can enter a session with administrative privileges by typing the following.

```
sudo -i
```

When you are through with your admin session, type **exit**.

In Chapter 21, I give an extended tour of the command shell. There, you will have additional opportunity to see *sudo* in action.

![](bbox=[0.14, 0.68, 0.25, 0.77])

> *Note* Always use **gksudo** when running graphical applications that need administrative privileges.

# I Need More Help!

Way back in the introduction to the book, I gave you a list of places that you might look to for help, some online and others in the community. As it turns out, your desktop has a very handy and fairly impressive collection of help, right at your fingertips.

The GNOME documentation browser, or Help Center, if you prefer (command name *help*) is something you've probably already guessed at.