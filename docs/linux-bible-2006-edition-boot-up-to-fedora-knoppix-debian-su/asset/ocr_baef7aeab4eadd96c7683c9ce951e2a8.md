# Chapter 2 + Running Commands from the Shell 37

```
drw-r--r-- -- chris sales 4096 May 10 01:50 .kde
-rw-r--r-- -- chris sales 149872 May 11 22:49 letter
```

```
^ ^ ^ ^ ^^
col 1 col 2 col 3 col 4 col 5 col 6 col 7
```

Displaying a long (-l) of the contents of your home directory shows you more file sizes and directories. The total line shows the total amount of disk used by the files in the list (158 kilobytes in this example). Directories such as the current directory (.) and the parent directory (..) — the directory above the current — are noted by the letter d at the beginning of each (each directory with a d and each file with a). The file and directory names are shown in column 7. In this example, a dot (.) represents /home and two dots (..) represent /home. Most of the files in this example are dot (.) files that used to store GUI properties (.kde directory) or shell properties (.bash files). The only non-dot file is the one named letter.

Column 3 shows the directory or file owner. The /home directory is owned by root, and everything else is owned by the user, who belongs to the size groups (listed in column 4).

In addition to d or -, each line contains the permissions for that file or directory. (Permissions and configuring shell property files are described later in this chapter.) Other information in the listing includes the number of links to the item (column 2) the size of each file in bytes (column 5) and the date and time each file was most recently modified (column 6).

> > [!NOTE]
> Note
> 
The number of characters shown for a directory (4096 bytes in these examples) reflects the size of the file containing information about the directory. While this number can grow over 4096 bytes for a directory that contains a lot of files, this number doesn't reflect the size of files contained in that.

# Checking System Activity

In addition to being a multiuseruser operating system, Linux is also a multitasking system. Multitasking means that many programs can be running at the same time. An instance of a running program is referred to as a process. Linux provides tools for listing processes, monitoring system usage, and stopping (or killing) processes when necessary.

The most common utility for checking processes is the ps command. Use it to see which programs are running, the resources they are using, and who is running them. Here is an example of the ps command:

```
$ ps -au
USER PID %CPU MEM VSZ TTY STAT TIME COMMAND
root 2146 0.0 1.808 1100 ttyp0 S 14:50 0:00 -- Jake
jake 2147 0.0 0.7 1836 1020 ttyp0 S 14:50 0:00 --bash
jake 2310 0.0 0.7 2592 912 ttyp0 R 18:22 0:00 -au
```