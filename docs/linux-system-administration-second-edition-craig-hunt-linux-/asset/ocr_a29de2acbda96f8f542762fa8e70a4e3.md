# ## Adding Users from the Command Line

Adding a user from the command line also requires the five steps listed earlier. You can use the useradd command to accomplish all of the steps except assigning a password. The useradd command accepts the information needed for the individual fields in the `/etc/passwd` file as arguments, as follows:

```
`useradd [-D] [-g default_group] [-b default_home] [-s default_shell] username`
```

The useradd command creates a new user account using the values given on the command line (supplying default values for any items not specified). useradd enters data into the appropriate system files. It then creates the user’s home directory at /home/username by default or at the location specified by the –b option. The useradd command copies sample configuration files from /etc/skel. In Red Hat, a group with the same name as the user is created, and the user is added to that group. (Other distributions handle groups differently, as explained further in the “The Function of Groups” section later in this chapter, which also describes Red Hat’s approach in more detail.)

Next give the user a password, using the passwd command:

```
`# passwd donald
New UNIX password:
Retype new UNIX password:`
```

**Tip** It is possible to pass a password on the command line with the –p option, but you must first encrypt the password using the crypt command. If you don’t, the system assumes that the string is encrypted and your login won’t work.

The configuration files contained in `/etc/skel` are intended to be set up for the typical user in that system. The files in this directory should include `.Xdefaults`, `.bash_logout`, `.bash_profile`, `.bashrc`, `.kderc`, `.kde/`, and `Desktop/`. You may add any files that will routinely be contained in your users’ home directories.

Default values for certain user characteristics may be set in the `/etc/login.defs` file. The mail directory, which typically is set to /var/spool/mail/username, is set via the MAIL_DIR variable in that file. Password aging information is also stored in the login.defs file. The minimum and maximum UID and GID values are stored there for automatic selection by the useradd command.

# ## Modifying User Accounts

Most system administrators make changes to user accounts by editing the appropriate files. It is often easier to use a text editor to edit the passwd file to change a simple configuration detail like the user’s shell than to bring up a GUI utility or use usermod at the command line. We’ll show you all three, and you can decide which you prefer.

# ### Manually Modifying User Accounts

The most direct way to modify a user’s account information is to edit the corresponding entry in /etc/passwd. For example, suppose you wish to change our hypothetical user Donald’s shell to the C shell. Use your favorite editor to open the /etc/passwd file. Donald’s line looks like this:

```
`donald:x:503:503:Unka Donald:/home/donald:/bin/bash`
```

Simply change the /bin/bash to /bin/csh, and save the file. The next time Donald logs in, he will be using the C shell. Of course, other information, including the user’s name string, Unka Donald, may