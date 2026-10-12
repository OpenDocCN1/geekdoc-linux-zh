system administrators often access files and programs via the root account. When a program is run using the root user account, the files that this program creates often are set with root ownership, effectively disallowing any use of the program by non-root users.

# Setting users’ configuration file permissions

Each user’s home directory houses some partially hidden files with filenames that start with a period (or dot). These files, often referred to as dot files, are often used to execute commands at user login. For example, all the shells (csh, tcsh, bash, etc.) available to a user read their settings from a dot file, such as those with the extension .cshrc or .bashrc. If a user is not careful to keep file permissions set properly, another not-so-friendly user can cause problems for the naive user. For example, if one user’s .cshrc file is writable by a second user, the latter can play a silly trick like putting a logout command at the beginning of the .cshrc file so that the first user will be logged out as soon as she logs in. Of course, there are worse silly tricks that the malevolent-minded could use to harm your system. To avoid privacy problems of this nature, you should make sure to keep watch for such situations on a multiuser system. Here are a couple ways that you can do so:

+   - If you have a lot of users, you can run the COPS program, a security analysis tool (www.fish.com/cops/), to detect many permission problems.
+   - If you have only a handful of users, you can also quickly perform simple checks, such as the following:

```
find /home -type f -name "*.rc" -exec ls -l {} \;
```

This command generates a list of permissions for all the dot files ending in rc (.cshrc, .bashrc, and so on) in the /home directory hierarchy. If your users’ home directories are kept in /home, this quickly shows you which users might have a permission problem. For example, a sample output of the above command is shown below: