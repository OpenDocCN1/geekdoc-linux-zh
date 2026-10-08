# # Command and Program Directories: PATH

Programs and commands are usually installed in several standard system directories, such as /bin, /usr/bin, /usr/X11R6/bin, or /usr/local/bin. Some packages place their commands in subdirectories, however, which you create inside one of these standard directories or in an entirely separate directory. In such cases, you may be unable to run those commands because your system may be unable to locate them in the new subdirectory. Your system maintains a set of directories that search for commands each time you execute one. This set of directories is kept in a system variable called PATH that is created when you start your system. If a command is in a directory that is not in this list, your system will be unable to locate and run it. To use such commands, you first need to add the new directory to the set of directories in the PATH variable. Installation tools like RPM will automatically update the PATH with the appropriate directories for you.

The PATH variable is added to by different services that start up when the system boots. A safer approach is to add a PATH definition in the /etc/profile file using that file's pathmunge function.

# ## /etc/profile

To make an application available to all users, you can add the software's directory to the path entry in the /etc/profile script. The /etc/profile script is a system script executed for each user when the user logs in. Carefully edit the /etc/profile file using a text editor, such as KEdit, Gedit, Emacs, or Vi (you may want to make a backup copy first with the cp command). You can easily add a directory to the PATH variable using the pathmunge function, which is also defined in /etc/profile. For example, if you install the Java 2 SDK, the Java commands are installed in a subdirectory called j2sdk-1.4.2/bin in the /usr/local directory. The full pathname for this directory is /usr/local/j2sdk-1.4.2/bin. You need to use pathmunge to add this directory to the list of directories assigned to PATH in the /etc/profile file.

```
pathmunge /usr/local/j2sdk-1.4.2/bin
```

You can see other uses pathmunge in /etc/profile like adding /sbin for the root user. After making your changes, you can execute the profile file to have the changes take effect.

```
$ . /etc/profile
```

> **NOTE** On older systems you had to create a new assignment entry for the PATH variable. You had to add a line that begins with PATH, followed by an = sign, and the term $PATH, followed by a colon, and then the directory to be added. The $ before PATH extracted the pathname from the PATH variable. If you added more than one directory, a colon had to separate them. There would also be a colon at the end. The following example shows the PATH variable with its list of directories and the /usr/local/j2sdk-1.4.2/bin directory added. Notice the $ before PATH after the = sign: PATH=$PATH: PATH=$PATH:/usr/local/j2sdk-1.4.2/bin.

![](bbox=[0.94, 0.76, 0.99, 0.87])