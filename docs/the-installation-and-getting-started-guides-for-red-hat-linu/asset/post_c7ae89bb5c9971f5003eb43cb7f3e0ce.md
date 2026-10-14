
+   • Tip: Always make sure you know which working directory you're in before you state the relative path to the directory or file you want to get to. You don't have to worry about your position in the filesystem, though, when you state the absolute path to another directory or file.

Now that you're starting to get the hang of changing directories, see what happens when you change to root's login directory.

```
cd /root
```

Oops... You're not logged in as root, so you're “denied permission” to access that directory.

Denying access to the root and other users' accounts (or login directories) is one way your Linux system prevents accidental or malicious tampering. You'll find out more about file “ownership” and permissions later in this chapter.

Really want to change to the root login? Then you've got to use the su command. Type this series of commands:

```
[billy@localhost billy] su root
Password: (your root password)
[root@localhost billy]# cd /root
[root@localhost /root]#
```

As soon as you give the root password, you'll see the changes in your command prompt to show your new, superuser status: the root account designation at the front of the prompt and # at the end (as shown in Figure 16-4).

![](img/46f4935125ba89e12897afbe9d77a097_705_0.png)

# Figure 16-4: Becoming root

Now, when you cd to root’s login directory, you’ll be granted access.

When you’re done being root, just type exit at the prompt.

```
[root@localhost /root]# exit
exit
[billy@localhost billy]
```

+   - **Summary:** To change directories using absolute pathnames, type cd/ directory/directory; to change directories using relative pathnames, type cd directory to move one directory below, cd directory/directory to move two directories below, etc.; to jump from anywhere on the filesystem to your login directory, type cd ~; to change to the parent of the directory you’re in, type cd .. Use . to refer to your current directory.

## Looking Around With ls

Now that you know how to move around, it's time to take a look at what's in the directories. But first, let's make sure you've got something you can look for in your login directory before we go any further. You can start by creating an empty file. To do so, you can use a utility called touch at the shell prompt. Try it; type:

```
touch foo.bar
```

Now, in your login directory, you've got an empty file called foo.bar. You'll see it in a couple minutes. Let's also create a new directory, using the mkdir command. At the prompt, type:

```
mkdir tigger
```

Now, you've created a directory called tigger in your login directory. From root, your new directory's absolute pathname would be /home/yourlogin/tigger, and your directory is the parent of tigger. (You can learn more about creating — and removing — files and directories in Chapter 3.)

Now, you're ready to go.

In the DOS world, using the dir command will display the contents of a directory.

The same can be said of Linux — with some notable exceptions.

In Linux, dir won't fully display the contents of directories, and doesn't have the power or flexibility of the list command — ls.

In your login directory, for example, type:

```
dir
```

Now, in the same xterm window, type:

```
ls
```

## The Getting Started Guide for Red Hat Linux 6.0

Looks the same (see Figure 16-5). You see, among other contents, your new file, foo.bar and the new directory, tigger.

![](img/46f4935125ba89e12897afbe9d77a097_707_0.png)

Figure 16-5: The dir and ls commands seem similar

But here the similarities end. Where dir shows you the contents of your directory, it doesn't actually show you everything. Even using the ls command, by itself, won't show you all the files in your directory. To see everything, you've got to call upon an option or two.

For example, in the same window that you'd used to type the dir and ls commands, now type:

```
ls -a
```

Quite a difference. When you added the -a option, you were specifying that you wanted to list all the files in the directory (see Figure 16-6).

In fact, there are a multitude of options available with the ls command.
