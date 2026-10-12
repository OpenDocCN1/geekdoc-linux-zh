you can see a long, detailed list of information on each file. (You can put multiple single-letter options together after a single dash, for example, -la.)

```
$ ls -la /home/chris
total 158
drwxrwxrwx 2 chris sales 1024 May 12 13:55 .
drwxr-xr-x 3 root root 1024 May 10 01:49 ..
-rw------- 1 chris sales 2204 May 18 21:30 .bash_history
-rw-r--r-- 1 chris sales 24 May 10 01:50 .bash_logout
-rw-r--r-- 1 chris sales 230 May 10 01:50 .bash_profile
-rw-r--r-- 1 chris sales 124 May 10 01:50 .bashrc
drw-r-r-- 1 chris sales 4096 May 10 01:50 .kde
-rw-rw-r-- 1 chris sales 149872 May 11 22:49 letter
```

Displaying a long list (-1 option) of the contents of your home directory shows you more about file sizes and directories. Directories such as the current directory (.) and the directory above the current directory (..) are noted as directories by the letter "d" at the beginning of each entry. In this case, dot (.) represents /home/chris and two dots (..), which is also referred to as the parent directory, represents /home. The /home directory is owned by root. All other files are owned by the user chris (who belongs to the sales group).

The file or directory names shown on the right are mostly dot (.) files that are used to store GUI properties (.kde) or shell properties (.bash files). The only non-dot file shown in this example is the one named letter. At the beginning of each line are the permissions set for each file. (Permissions and configuring shell property files are described later in this chapter.) Other information in the listing includes the size of each file in bytes (column 4) and the date and time each file was most recently modified (column 5).

# # Checking system activity

In addition to being a multi-user operating system, Linux is also a multitasking system. Multitasking means that many programs can be running at the same time. An instance of a running program is referred to as a *process*. Linux provides tools for listing running processes, monitoring system usage, and stopping (or killing) processes when necessary.

The most common utility for checking running processes is the ps command. With ps, you can see which programs are running, the resources they are using, and who is running them. The following is an example of the ps command:

```
$ ps au
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 2146 0.0 0.8 1908 1100 ttyp0 S 14:50 0:00 login --jake
jake 2147 0.0 0.7 1836 1020 ttyy0 S 14:50 0:00 -bash
jake 2310 0.0 0.7 2592 912 tty0 R 18:22 0:00 ps au
```

In this example, the -a option asks to show processes of all users that are associated with your current terminal, and the -u option asks that user names be shown, as well as other information