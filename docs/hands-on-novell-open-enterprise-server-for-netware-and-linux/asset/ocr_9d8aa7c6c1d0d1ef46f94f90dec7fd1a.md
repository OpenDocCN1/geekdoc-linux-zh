# Using Info Pages

Linux has another source of command documentation called **info pages**, which often provide a more current version of command documentation and can be read by using the info command, as shown in Figure 13-11. In SUSE Linux, info files are stored in the /usr/share/info directory and have the following advantages over man pages:

+   - Info files use a standard structure in the documentation layout.
+   - Info files contain specific sections that can be accessed directly from the table of contents, compared to using section numbers with the man command.
+   - Info file sections can be linked to form a complete document.

![](bbox=[0.12, 0.23, 0.98, 0.5])

You can use several command keys, listed in Table 13-4, to move around info pages.

Table 13-4 Common info command keys

| Command Key | Description |
| :--- | :--- |
| Spacebar, Page Down | Page down one screen |
| Backspace, Page Up | Page up one screen |
| b | Move cursor to the beginning of the info page |
| t | Move cursor to the next reference |
| h | Display help |
| q | Exit the info page |

# Creating Users and Groups from the Command Line

Most network administrators find it more convenient to create and manage user and group accounts with YaST, but the Certified Linux Professional (CLP) certification requires creating user and group accounts from the command line with the useradd and groupadd commands. Being able to use command-line utilities has certain advantages, such as creating users from script files and working on other Linux systems that don’t have the YaST utility installed. Command-line utilities use parameters to specify additional information and options. Parameters usually take the form of a letter preceded by a hyphen. To learn more about parameters for command-line utilities, use the man command. For example, Figure 13-12 shows an example of using the man command to view information about parameters for the useradd command. In the following activity, you learn how to use the adduser and addgroup commands to create new local users and groups on your SUSE Linux server.