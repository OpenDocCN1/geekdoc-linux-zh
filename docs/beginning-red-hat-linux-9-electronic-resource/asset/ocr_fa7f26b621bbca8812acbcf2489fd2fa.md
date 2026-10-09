# **Ordinary Users with Extraordinary Privileges**

We’ve already seen in this chapter that when a program executes, it needs to have permissions for performing its tasks (see the attempt in the previous section to list the widgets directory). Often non-root users need to perform functions that may be restricted to root users only. This applies not just to the root and non-root user case; in fact it applies to any user or the group the user belongs to that may not have the permission to perform a certain operation.

Fortunately, there is a way to set permissions so that this can happen, *without* actually elevating the non-privileged user to a privileged status. If a certain command requires root privileges, the super-user can set the *setuid* execute permissions for this program. Once the *setuid* bit has been set, it is possible for non-privileged users to execute the program and have it behave as if it were run by root.

The *passwd* program is a typical example of such a program. Regular users can use this program to modify the password they use for logging in. By default on Red Hat Linux 9, passwords are encrypted and stored in the file /etc/shadow that can be modified only by the root user. From what we have seen so far, when a user executes the *passwd* program, the program would assume just the privileges assigned to that user. So how does the password program modify this file to update it with the new password? The trick lies in setting the *setuid* bit:

```
$ ls -al /usr/bin/passwd
-r-s--x--x 1 root root 15368 May 28 2002 /usr/bin/passwd
```

The s indicates the *setuid* bit for this program. Thus when the *passwd* program executes, it assumes the privileges of the root user. Since it is restricted to just updating the /etc/shadow file, there is not much of a risk involved. In simple terms, assigning the *setuid* bit by a privileged user to a program owned by them indicates that other users may execute the program with the same privileges as the owner. Along the lines of the *setuid* bit is the *setgid* bit. When set, the program executes with the privileges of the group it belongs to.

Of course, it is not advisable to assign the *setuid* bit arbitrarily to programs. System administrators and programmers must carefully review the program before assigning the *setuid* bit to prevent malicious users from using *setuid* bit-enabled program to compromise system security. The *setuid* and *setgid* bits can be assigned via the *chmod* command:

```
$ chmod u=rws treasure_key.txt (setting the setuid bit)
$ chmod g=rws treasure_key.txt (setting the setgid bit)
```

# **Time Attributes**

Any file has associated with it three different *time attributes*:

+   - mtime is the time at which the file was last modified
+   - atime is the time at which the file was last accessed
+   - ctime is the time at which the attributes of the file were last changed