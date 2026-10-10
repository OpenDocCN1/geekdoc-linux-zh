# # Types of User Accounts

While in Linux all user accounts are created the same way using the `useradd` utility (see Chapter 10, “Administering Users and Groups”), not all user accounts behave the same way. There are three basic types of user accounts in Linux:

+   - **Root:** The root user account is the main administrator user account on the system. It is identified by being assigned the special user ID value of 0. The root user account has permission to access all files and directories on the system, regardless of any permission settings assigned.
+   - **Standard:** Standard Linux user accounts are used to log into the system and perform standard tasks, such as running desktop applications or shell commands. Standard Linux users normally are assigned a $HOME directory, with permissions to store files and create subdirectories. Standard Linux users cannot access files outside their $HOME directory unless given permission by the file or directory owner. Most Linux distributions assign standard user account user IDs over 1000.
+   - **Service:** Service Linux user accounts are used for applications that start in the background, such as network services like the Apache web server or MySQL database server. By setting the *passwd* value in the *shadow* file to an asterisk, these user accounts are restricted so that they cannot be used to log into the system. Also, the login shell defined in the `/etc/passwd` file is set to the `nologin` value to prevent access to a command shell. Service accounts normally have a user ID less than 1000.

![](bbox=[0.13, 0.55, 0.23, 0.61])

> Some Linux distributions, such as Ubuntu, don’t allow you to log in directly as the root user account. Instead they rely on escalating privileges (discussed in the next section) to allow standard user accounts to perform administrative tasks.

# ## Escalating Privileges

While the root user account has full access to the entire Linux system, it’s generally considered a bad practice to log in as the root user account to perform system-related activities. There’s no accountability for who logs in with the root user account, and providing the root user account password to multiple people in an organization can be dangerous.

Instead, most Linux administrators use privilege escalation to allow their standard Linux user account to run programs with the root administrator privileges. This is done using three different programs:

+   - `su` The `su` command is short for *substitute user*. It allows a standard user account to run commands as another user account, including the root user account. To run the `su` command, the standard user must provide the password for the substitute user account. While this solves the problem of knowing who is performing the administrator task, it doesn’t solve the problem of multiple people knowing the root user account password.