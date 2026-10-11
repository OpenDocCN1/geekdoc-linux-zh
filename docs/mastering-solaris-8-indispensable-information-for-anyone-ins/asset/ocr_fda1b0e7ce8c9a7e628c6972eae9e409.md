+   *   **type c** Search for a file of the specified type c. (See Table 4.3.)
+   *   **user** Search for a file with a user in the /etc/passwd file or a NIS/NIS+ database.

> **NOTE** An infinite loop symbolic directory exists when a symbolic link to a directory points to one of its higher-level directories. In the example ln -s /usr/home/me /usr/home, the me directory points to /usr/home. When you run a find against an infinite loop, it might try to look in the /usr/home/me (for example) and see that it is a symbolic link to /usr/home. It would then look in /usr/home and see the directory me and try to look in it again. This loop would give the appearance that find was hung and it would have to be killed.

Table 4.3 shows the values that can be substituted for c in the search string expression type c.

TABLE 4.3: TYPE ARGUMENTS

| c | Value | Type of File |
|---|---|---|
| b | Block-special file |  |
| c | Character-special file |  |
| d | Directory |  |
| D | Door |  |
| f | Plain file |  |
| l | Symbolic link |  |
| p | FIFO named pipe |  |
| s | Socket |  |

The <execute *command*> portion of the find command is used to execute a command when a file matches the criteria specified in the search string expressions listed earlier. Among the various commands you can execute are the following (again, preceded by a hyphen):

+   *   **exec <command> { } \;** Run the command.
+   *   **cpio <*device*name>** An executable command. Means that, if a file matches the search criteria, write the current file on the specified device in copy in/out (cpio) format.
+   *   **print** Cause the current path to be printed. This is the default execution if nothing else is specified.