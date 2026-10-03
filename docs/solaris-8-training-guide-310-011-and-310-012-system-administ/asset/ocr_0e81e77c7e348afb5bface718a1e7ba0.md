# MANAGING USER AND GROUP ACCOUNTS FROM THE COMMAND LINE

Another way to manage user accounts is from the command line. Although using the command line is more complex than using the Admintool GUI interface, the command line provides a little more flexibility. Solaris supplies the user administration commands described in Table 5.4 for setting up and managing user accounts.

TABLE 5.4
Account Administration Commands

| Command | Description |
|---|---|
| useradd | Adds a new user account |
| userdel | Deletes a user account |
| usermod | Modifies a user account |
| groupadd | Adds a new group |
| groupmod | Modifies a group (for example, changes the group ID or name) |
| groupdel | Deletes a group |

# Adding User Accounts from the Command Line

You can add new user accounts on the local system using the useradd command. This command adds an entry for the new user into the /etc/passwd and /etc/shadow files, which are described in Chapter 8.

Just like Admintool, the useradd command also copies all the user initialization files found in the /etc/skel directory into the new user's home directory. User initialization files are covered in the next section of this chapter.