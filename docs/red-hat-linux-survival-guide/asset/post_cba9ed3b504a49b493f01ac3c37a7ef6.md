
```
-rw-r--r-- 1 kabir kabir 124 Jul 4 18:02 /home/kabir/.bashrc
-rw-r--r-- 1 kabir kabir 3728 Jul 4 18:02 /home/kabir/.screenrc
-rw-r--r-- 1 webcam httpd 124 Aug 7 20:57 /home/webcam/.bashrc
-rw-r--r-- 1 webcam httpd 3728 Aug 7 20:57 /home/webcam/.screenrc
```

## Setting default file permissions for users

As a system administrator, you can define the default permission settings for all the user files on your system. To set the default permissions for new files, use the umask command, as follows:

```
umask mask
```

As an example of how umask works, suppose that umask is set to 022. When a new file is created, typically a permission setting of 0666 is requested by the file creation function — open. However, in such a case, the final permission settings for the file are derived by the system, as shown in Figure 8-3.

As Figure 8-3 shows, the requested permission, 0666, is ANDed with the complement of the current mask (that is, 022 becomes 755) so that the result is 0644, which allows the file owner read- and write-access but gives everyone else read-access only.

To create a default mask for file permissions, you can embed the umask command in a global shell resource file in /etc so that when a user logs in and runs a shell, the global resource file for that shell is executed. This in turn executes the umask command and provides a default mask for the user session. For example, if your users use the /bin/csh or /bin/tcsh shell, you can put a desirable umask command in the /etc/csh.cshrc file for this purpose. For bash users, the umask is set in /etc/profile file.

## Setting executable file permissions

Program files that can be run by regular users should never have write permission set for anyone but the owner. For example, the program files in /usr/bin should have permission settings such that only root can read, write, and execute, and everyone else can only read and execute these files. Allowing others to write into a program file can create serious security holes. As an example of such a hole, if someone other than the root user is allowed to write to a program such as /usr/bin/zip, a malicious user can

replace the real Zip program with a Trojan-horse program that compromises system security and damages files and directories as it pleases.

![](img/9eb7e89292d2f85707b4d49102c865b7_216_0.png)

Figure 8-3 How umask is used by the system.

To avoid security issues of this nature, always check to make sure that the program files on your systems have proper permissions. Run COPS frequently to detect permission-related problems.

## Setting default file permissions for FTP

If many of your users FTP their files on the server, you can control the default umask setting for the FTP server to ensure that one user's file is not accessible by another. For example, if you want to set permissions so that only the user and her group can read a file uploaded on a Web server via FTP, you can modify the server_args line in the /etc/xinetd.d/ wu-ftpd file. This line by default looks as follows:

```
server_args			= -l -a
```

To set a default umask for all files uploaded via FTP, you need to add a -u argument with the appropriate umask value. For example, to set 640 (rw-r-----) permission for each file uploaded, you can set the umask to 026. To do so, change the preceding line as follows:

```
server_args			= -l -a -u026
```

Then restart the inetd server (killall -USR1 xinetd) and FTP a file via a user account to see whether the permissions have been set as expected. This can be very handy for systems that act as Web servers for many different clients. If you do not want one client to see another client’s files, you can use this option along with a special ownership setting. For example, suppose you keep all of your Web client files in the /www partition or directory, where each client site has a directory of its own (for example, /www/myclient1, /www/myclient2, and so on). You have probably already given each client an FTP account with which to upload files to these directories. To stop a client from seeing another client’s files, use umask with the FTP server as described above and then reset the ownership of each client site as follows:

```
chown -R client.webserveruser /www/clientdir
```

For example, if you run your Web server as httpd and have a client user called myclient, then the preceding command will look like this:

```
chown -R myclient.httpd /www/myclient
```

This changes the ownership of the /www/myclient directory along with all of its subdirectories and files to the myclient user and to the httpd group, allowing the client user to own, modify, and delete her files and the Web server to read the files in the directory. To disallow everyone else, you must change the permissions as follows:

```
chmod -R 2770 /www/clientdir
```

For the current example, the actual command is as follows:

```
chmod -R 2770 /www/myclient
```

This sets all the files and subdirectory permissions for /www/myclient to 2770, which allows the files and directories to be readable, writable, and executable by the owner (myclient) and the Web server user (httpd) and also ensures that when new files are created, they have their permissions set to allow the Web server user to read the file. This is done using the set-GID (2) digit.

## Running Programs

### IN THIS CHAPTER

- Learning Linux from the command line
- Starting a program from the command line
- Stopping a running program
- Changing a program's priority
- Monitoring and logging running programs
- Scheduling programs using at and cron

Linux is primarily a command-line operating system, which is also capable of running a very rich Graphical User Interface (GUI) called X Window system. However, like most Unix systems the power of Linux lies within the commands themselves. Therefore knowing how to run, monitor, log, and schedule commands is very important in becoming an expert in Linux. In this chapter you will learn how to do just that.

## Working from the Linux Command Line

Much of your work with Linux will consist of entering and executing commands one after another. These commands follow established rules commonly known as command-line syntax. If you do not follow the syntax correctly, a command may execute incorrectly, and problems can result.

Commands are entered at a Linux command prompt, which can be found either when you’re logged in to Linux and not running X or a

graphical interface, or from a terminal window within a graphical environment (often called an xterm). When you type a command, you type the name of the command, possibly followed by other information. The items that follow the name of the program are called arguments. The program carries the responsibility of determining how to use the arguments.

The general syntax of a Linux command is:

```
command_name options parameters
```

In the following command, for example, there are two arguments, -l and doc.txt:

```
wc -l doc.txt
```

![](img/9eb7e89292d2f85707b4d49102c865b7_221_0.png)

When entering commands at the command line, remember the arguments are case sensitive just as filenames in Unix are.

There are two types of arguments: options and parameters. Options come right after the program name and are usually prefixed with a dash (-). The parameters follow the options. In the preceding example, -l is an option telling the wc command to count the number of lines in the doc.txt file (the parameter).

![](img/9eb7e89292d2f85707b4d49102c865b7_221_1.png)

Most commonly, you use commands one at a time. However, you can stack multiple commands into one command line by separating the commands with a semicolon. For example, you can clear the screen and then list the contents of the current directory with one command line with the following command:

```
clear; ls
```

## Saving typing with wildcards

When you use directory and file commands, you can use special characters called wildcards to specify patterns of filenames. Wildcards make selecting multiple items easy. For example, to list all of the files in the current directory that end in .c, you would use the following command:

```
ls *.c
```
