Access to a system is allowed only through user login accounts set up by the system administrator. A user account includes information a user needs to log in and use a system—a user login name, a password, the user's home directory, and login initialization files. User accounts can range from occasional guests needing read-only access to a few files to regular users who need to share information between several departments. Table 5-1 lists the methods and tools available in Solaris for adding new user accounts to the system.

# Table 5-1 Adding New User Accounts

| Environment | Recommended Tool | Availability |
|---|---|---|
| On remote and/or local systems in a networked, name service (NIS, NIS+) environment | User and Group Manager (graphical user interface) from the Solstice AdminSuite | Available as a separate product. Refer to the Solstice AdminSuite 2.3 Administration Guide. |
| Local system | Admintool (graphical user interface) | Provided with Solaris 2.6. |
| Command-line | Terminal window (CDE environment) or shell tool or command tool (OpenWindows environment) | Provided with Solaris 2.6. |

One way to add user accounts is from the command line. Solaris supplies the following commands for setting up user accounts:

+   - `useradd` Add a new user account
- `userdel` Delete a user account
- `usermod` Modify a user account
- `groupadd` Add a new group
- `groupmod` Modify a group (for example, change the group ID or name)
- `groupdel` Delete a group

As with many UNIX commands, the command line method of adding user accounts is cumbersome and confusing. For this reason, Sun has added user account administration to the Solaris Admintool. Admintool is a graphical user interface designed to ease several routine system administration tasks. By using the Admintool, the system administrator is presented with a menu-like interface that is much easier to use than the ASCII interface supplied at the command prompt. Admintool does not change name service maps or tables when NIS or NIS+ is being used; this task is accomplished by an unbundled product called Solstice AdminSuite. For instructions on using AdminSuite, refer to the Solstice AdminSuite 2.3 Administration Guide.