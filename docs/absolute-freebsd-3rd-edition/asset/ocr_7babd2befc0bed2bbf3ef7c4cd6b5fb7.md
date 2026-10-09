Certain actions require absolute control of the system, including manipulating core system files such as the kernel, device drivers, and authentication systems. Such activities are designed to be performed by root.

To use the root password, you can either log in as root at a console login prompt or, if you’re a member of the group wheel, log in as yourself and use the switch user command su(1). (We’ll discuss groups later in this section.) I recommend su; it logs who uses it and can be used on a remote system. The command is very simple to use:

```
# su
Password:
#
```

Next, check your current user ID with the id(1) command:

```
# id
uid=0(root) gid=0(wheel) groups=0(wheel), 5(operator)
#
```

You now own the system—and I do mean own it. Consider every keystroke; carelessness can return your hard drive to the primordial state of unformatted empty wasteland. And share the root password sparingly, if at all, because anyone who has the root password can inflict unlimited damage on the system.

Remember, only the users in the group wheel can use the root password to become root through su(1). Anyone can use the root password at the system console, which is why physical protection of your system is vital. If you give the root password to a regular user who doesn’t have physical access to the console, they can type su and enter the root password as many times as you want, and it still won’t work.

This naturally leads to the question, “Who needs root access?” Much of the configuration discussed in this book requires use of the root password. Once you have the system running properly, you can greatly decrease or discontinue use of the root password. For those remaining tasks that absolutely require root privileges, I recommend the sudo package, and probably my book Sudo Mastery (Tilted Windmill Press,