
## The Getting Started Guide for Red Hat Linux 6.0

Let's check our changes by listing the file (ls -l sneakers.txt):

```
-rw-r--r-- 1 billy billy 150 Mar 19 08:08 sneakers.txt
```

![](img/46f4935125ba89e12897afbe9d77a097_739_0.png)

Figure 16-20: Removing group write permissions

And there it is; now, neither the group nor others have write permission to sneakers.txt. To return the group's write access for the file, we can just add the value of w (2) to the second set of permissions.

```
chmod 664 sneakers.txt
```

- Tip: Beware 666 and 777. Biblical implications aside, either of these settings will allow everyone to read and write to a file or directory. Such settings as these could allow tampering with sensitive files, so in general, it's not a good idea to allow these settings.

Here's a list of some common settings, numerical values and their meanings:

- `-rw---- (600)` — Only the user has read and write permissions.
- `-rw-r--r-- (644)` — Only user has read and write permissions; the group and others can read only.
- `-rwx--- (700)` — Only the user has read, write and execute permissions.
- `-rwxr-xr-x (755)` — The user has read, write and execute permissions; the group and others can only read and execute.
- `-rwx--x--x (711)` — The user has read, write and execute permissions; the group and others can only execute.
- `-rw-rw-rw- (666)` — Everyone can read and write to the file. Bad idea.
- `-rwxrwxrwx (777)` — Everyone can read, write and execute. Another bad idea.

Here are a couple common settings for directories:

- `drwx--- (700)` — Only the user can read, write in this directory.
- `drwxr-xr-x (755)` — Everyone can read the directory, but its contents can only be changed by the user.

- **Summary:** You can change permissions with the chmod command by using letters or numbers. Type chmod (permissions) file to change permissions of a file or directory.

You've already come quite a distance in learning about your Red Hat Linux system — from navigation to setting and changing permissions. Now, it's time to learn a little more about managing what you have on your system. The following chapter will help you to understand a little more about file types and how to work with a variety of commands.

## 17 Managing Files and Directories

If you're a Linux newbie — and there are many — you may feel a little disoriented when you want to accomplish your first tasks. Relax. If you've had any experience with other operating systems, learning Linux is a bit like learning to drive in a new country: The ideas are the same, but some of the particulars are a bit different. We'll go over several of those “rules of the road” in this chapter. But there's one component of your new operating system you just can't do without: the shell. We've made numerous references to the shell — as in “shell prompt,” or “bash.” Now, it's time to learn a little more about this indispensable tool. But first, a little history...

### Shell Collecting

In the olden days (we're talking '60s here), when AT&T's Dennis Ritchie and Ken Thompson were designing UNIX, they wanted to create a way that humans could interact with their new system.

Operating systems at the time did come with “command interpreters,” which could take commands from the user and interpret them for the computer to understand.

But Ritchie and Thompson wanted something more, something which could offer better features than the command interpreters of the day.

Enter the Bourne shell (known simply as sh), created by S.R. Bourne, which fulfilled the goals of UNIX's creators.

Since the creation of the Bourne shell, other shells have been developed, such as the C shell (csh) and the Korn shell (ksh).

When the Free Software Foundation sought a royalty-free shell, developers began to work on the language behind the Bourne shell as well as some of the popular features from other shells available at the time.

The result was the Bourne Again Shell — or bash.
