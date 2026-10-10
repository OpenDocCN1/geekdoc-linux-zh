![](bbox=[0.14, 0.09, 0.55, 0.25])

# Figure 2-14 Shells, terminals, and the kernel

When a user interacts with her computer, she is interacting with the kernel of the computer's operating system. However, this interaction cannot happen directly; it must have a channel through which it can access the kernel as well as a user interface that passes user input to the kernel for processing. The channel that allows a certain user to log in is called a **terminal**, and there can be many terminals in Linux that allow you to log in to the computer locally or across a network. After a user logs in to a terminal, he receives a user interface called a **shell**, which then accepts input from the user and passes this input to the kernel for processing. The shell that is used by default in Linux is the **BASH shell** (short for Bourne Again Shell), which is an improved version of the Bourne shell from AT&T and is the shell that is used throughout this book. The whole process looks similar to what is shown in Figure 2-14.

As mentioned earlier, Linux is a multiuser and multitasking operating system and, as such, can allow for thousands of terminals. Each terminal could represent a separate logged-in user that has its own shell. The four different "channels" shown in Figure 2-14 could be different users logged in to the same Linux computer. Two users could be logged in locally to the server (seated at the server itself), and the other two could be logged in across a network, such as the Internet.

By default, when you log in to a terminal, you receive a command-line shell (BASH shell), which prompts you to type in commands to tell the Linux kernel what to do. However, in this computing age, most people prefer to use a graphical interface in which they can use a computer mouse to navigate and start tasks. In this case, you can simply choose to start a graphical user interface (GUI) environment on top of your BASH shell after you are logged in to a command-line terminal, or you can switch to a graphical terminal, which allows users to log in and immediately receive a GUI environment. A typical command-line terminal login prompt looks like the following:

```
Fedora release 20 (Heisenbug)
Kernel 3.11.10-301.fc20.x86_64 on an x86_64 (tty2)
```

```
server1 login:
```

A typical graphical terminal login for Fedora Linux (called the GNOME Display Manager or gdm) is depicted in Figure 2-15.

To access a terminal device at the local server, you can press a combination of keys, such as Ctrl+Alt+F2, to change to a separate terminal. If you are logging in across the network, you