# ### 5.13 Getting Process IDs

A process can get its process ID and its parent’s process ID with these calls:

![](bbox=[0.14, 0.21, 0.85, 0.3])

![](bbox=[0.14, 0.31, 0.85, 0.4])

I already used `getpid` in an example back in Section 2.4.3.

# ### 5.14 chroot System Call

![](bbox=[0.14, 0.49, 0.85, 0.59])

This system call, reserved for superuser processes, changes the root directory of the process, the directory whose path is /. It’s nonstandard but implemented on essentially all UNIX-like systems (because it’s very old).

There are two uses for `chroot` that come to mind:

+   - When a command with built-in path names (such as /etc/passwd) is to be run on other than the usual files. A new tree can be constructed wherever convenient; the root can be changed, and then the command can be executed. This is primarily useful in testing new commands before they are installed.

+   - For added security, such as when a web-server process begins processing an HTML file. It can set the root to the base path, which guarantees that no paths to other files can be accessed. Even the path “..” won’t work because at the root it’s interpreted as a reference right back to the root.