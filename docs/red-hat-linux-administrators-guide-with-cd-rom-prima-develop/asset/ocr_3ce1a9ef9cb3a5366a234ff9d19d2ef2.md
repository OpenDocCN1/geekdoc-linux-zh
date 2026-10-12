# # Adding New Users with useradd

When you use useradd, the command does more than simply add a new user to the system. It goes through a series of steps in creating files, adding directories, and modifying other items. This section explains what you will see when adding a new user and describes how the machine actually performs the task so that you don't have to do it step by step. However, understanding the process is always a good idea. Even when adding users via the automated method, you may sometimes have to go back and clean out users in case of file backups or restorations.

When first adding a new user, you might want to use the absolute path to execute the command. Based on the permissions that you currently have as root, and whether you used the su or su - command or logged in directly as root, /usr/sbin may or may not be in your path. It is good practice to use the absolute path, as follows:

```
# /usr/sbin/useradd joe
```

Using the absolute path not only helps you to familiarize yourself with each program's location, but also helps you avoid using any older or replaced files by the same name that come earlier in your search path.

> > **TIP**
> > You can always add a directory to your path temporarily so that you do not need to type the absolute path each time you invoke the command. Enter the following to modify your $PATH and add /usr/sbin to your default search:
> > `export PATH=$PATH:/usr/sbin*`

The useradd command creates a /home/joe directory and installs joe in the /etc/passwd (and /etc/shadow if shadowed passwords were enabled during the install) and in the /etc/group files. It also places specific dotfiles within that user's home directory based on the contents of the /etc/skel directory. Although this command creates the necessary files and directories, you still have not set the password. The user joe will still be unable to log in until the password is set. Once again, to set the password, simply type passwd and the username. For instruction on setting user-specific passwords, see Chapter 5.