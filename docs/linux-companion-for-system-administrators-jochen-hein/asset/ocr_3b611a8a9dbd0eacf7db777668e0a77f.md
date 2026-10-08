# 266 UNIX TOOLS

example, -print0 inserts a null byte as a separator between the individual names instead of a line feed.
Instead of listing the found file names, a UNIX command can be started with the file name as a parameter. This is obtainedby using -exec which generates a new process for each found file. If the search result contains many files, it is recommended that one of the commands shown in Listing 10.2 be used, which generates only one or a few additional processes. They employ either a mechanism of the shell or the xargs program (see Section 10.1.6).

```
(Linux):$ find -name "*.bak" -exec rm -f {};
(Linux):$ rm -f $(find -name "*.bak")
(Linux):$ find -name "*.bak" | xargs rm -f
```

**Listing 10.2** Execution of commands with find.

All examples in Listing 10.2 delete all files bearing the extension .bak. The -exec parameter executes the command rm -f for each found file. The brackets are placeholders for the file name. The semicolon tells the find command where the -exec parameter ends. As the shell would also evaluate the semicolon, it must be masked with a backslash (\).
If you are not sure the specified command should be executed for all files, you can use the option -ok instead of -exec. Here, for each file, find files in which a particular piece of text occurs. The example in Listing 10.3 lists all files that contain the host name. Depending on the extent of the file system, the example can take a while to run, because all directories are searched.

Another interesting purpose of the -exec option can be seen in its combination with the grep command. This makes it quite easy, for example, to find files in which a particular piece of text occurs.

```
(Linux):# find -type f -exec grep -L \ 'hostname{}';
/etc/profile
/etc/hostname
/etc/hosts
/etc/nntpasswd
/etc/ftpaccess
```

**Listing 10.3** find in combination with grep.

In combination with the cpio or afio commands (Section 7.5.1), it is also possible to use find for the construction of a simple data backup system. A very