
```
[me@linuxbox ~]$ ssh remote-sys 'ls *' > dirlist.txt
me@twin4's password:
[me@linuxbox ~]$
```

Notice the use of the single quotes in the command above. This is done because we do not want the pathname expansion performed on the local machine; rather, we want it to be performed on the remote system. Likewise, if we had wanted the output redirected to a file on the remote machine, we could have placed the redirection operator and the filename within the single quotes:

```
[me@linuxbox ~]$ ssh remote-sys 'ls * > dirlist.txt'
```

## Tunneling With SSH

Part of what happens when you establish a connection with a remote host via SSH is that an encrypted tunnel is created between the local and remote systems. Normally, this tunnel is used to allow commands typed at the local system to be transmitted safely to the remote system, and for the results to be transmitted safely back. In addition to this basic function, the SSH protocol allows most types of network traffic to be sent through the encrypted tunnel, creating a sort of VPN (Virtual Private Network) between the local and remote systems.

Perhaps the most common use of this feature is to allow X Window system traffic to be transmitted. On a system running an X server (that is, a machine displaying a GUI), it is possible to launch and run an X client program (a graphical application) on a remote system and have its display appear on the local system. It's easy to do; here's an example: Let's say we are sitting at a Linux system called linuxbox which is running an X server, and we want to run the xload program on a remote system named remote-sys and see the program's graphical output on our local system. We could do this:

```
[me@linuxbox ~]$ ssh -X remote-sys
me@remote-sys's password:
Last login: Mon Sep 08 13:23:11 2008
[me@remote-sys ~]$ xload
```

After the xload command is executed on the remote system, its window appears on the local system. On some systems, you may need to use the "-Y" option rather than the "-X" option to do this.

Tip: The SFTP protocol is supported by many of the graphical file managers found in Linux distributions. Using either Nautilus (GNOME) or Konqueror (KDE), we can enter a URI beginning with sftp:// into the location bar and operate on files stored on a remote system running an SSH server.

## An SSH Client For Windows?

Let’s say you are sitting at a Windows machine but you need to log in to your Linux server and get some real work done; what do you do? Get an SSH client program for your Windows box, of course! There are a number of these. The most popular one is probably PuTTY by Simon Tatham and his team. The PuTTY program displays a terminal window and allow a Windows user to open an SSH (or telnet) session on a remote host. The program also provides analogs for the scp and sftp programs.
PuTTY is available at http://www.chiark.greenend.org.uk/~sgtatham/putty/

## Summing Up

In this chapter, we have surveyed the field of networking tools found on most Linux systems. Since Linux is so widely used in servers and networking appliances, there are many more that can be added by installing additional software. But even with the basic set of tools, it is possible to perform many useful network related tasks.

## Further Reading

- For a broad (albeit dated) look at network administration, the Linux Documentation Project provides the Linux Network Administrator’s Guide: http://tldp.org/LDP/nag2/index.html
- Wikipedia contains many good networking articles. Here are some of the basics: http://en.wikipedia.org/wiki/Internet_protocol_address http://en.wikipedia.org/wiki/Host_name http://en.wikipedia.org/wiki/Uniform_Resource_Identifier

## 17 – Searching For Files

As we have wandered around our Linux system, one thing has become abundantly clear: A typical Linux system has a lot of files! This begs the question, “How do we find things?” We already know that the Linux file system is well organized according to conventions that have been passed down from one generation of Unix-like systems to the next, but the sheer number of files can present a daunting problem.

In this chapter, we will look at two tools that are used to find files on a system. These tools are:

- `locate` – Find files by name
- `find` – Search for files in a directory hierarchy

We will also look at a command that is often used with file-search commands to process the resulting list of files:

- `xargs` – Build and execute command lines from standard input

In addition, we will introduce a couple of commands to assist us in our explorations:

- `touch` – Change file times
- `stat` – Display file or file system status

## locate – Find Files The Easy Way

The `locate` program performs a rapid database search of pathnames, and then outputs every name that matches a given substring. Say, for example, we want to find all the programs with names that begin with “zip.” Since we are looking for programs, we can assume that the name of the directory containing the programs would end with “bin/”. Therefore, we could try to use `locate` this way to find our files:

```
[me@linuxbox ~]$ locate bin/zip
```

`locate` will search its database of pathnames and output any that contain the string
