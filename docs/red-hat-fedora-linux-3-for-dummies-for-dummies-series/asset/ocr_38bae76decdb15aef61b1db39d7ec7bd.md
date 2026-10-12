![](bbox=[0.05, 0.09, 0.15, 0.2])

Fedora Core assigns a unique group to each user. For example, when you add the first user to your system, that user gets the user ID and group ID of 500. The next user receives the user ID and group ID of 501, and so on. This system gives you lots of control over who gets what access to your files.

# ## Making Your Own Rules

You, as the owner of a file, can specify permissions for reading, writing to, or executing a file. You can also determine who (yourself, a group of people, or everyone in general) can do these actions on a file. What do these permissions mean? Read on (you have our permission):

+   * **Read permission:** You can read the file. For a directory, read permission allows the `ls` command to list the names of the files in the directory. You must also have execute permission for the directory name to use the `-l` option of the `ls` command or to change to that directory.
+   * **Write permission:** You can modify the file. For a directory, you can create or delete files inside that directory.
+   * **Execute permission:** You can type the name of the file and execute it. You cannot view or copy the file unless you also have read permission. Files containing executable Linux commands, called *shell scripts*, must therefore be both executable and readable by the person executing them. Programs written in a compiled language, such as C, however, must have only executable permissions, to protect them from being copied where they shouldn’t be copied.

For a directory, execute permission means that you can change to that directory (with `cd`). Unless you also have read permission for the directory, `ls -l` doesn’t work. You can list directories and files in that directory, but you cannot see additional information about the files or directories by using just an `ls -l` command. Although this arrangement may seem strange, it’s useful for security.

The first character of a file permission is a hyphen (-) if it’s a file; the first character of a directory permission is d. The nine other characters are read, write, and execute positions for each of the three categories of file permissions:

+   * **Owner** (also known as the user)
+   * **Group**
+   * **Others**