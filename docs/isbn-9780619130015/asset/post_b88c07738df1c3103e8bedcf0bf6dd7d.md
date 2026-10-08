
## DISCOVERY

- 1. Remove the colon characters from the phoneadd program and reposition the cursor to improve the appearance of the data entry screen.
- 2. Place the screen display from the phoneadd program in a function, called phscreen. Using the vi editor, type the function into .mystuff (from Exercise 3) and test the function by calling it from the command line.
- 3. Add menu items to phmenu that call the sort_date and sort_dept functions you created in the .myfuncs file. Test the program.
- 4. Create a shell function, average. Store it in a file, avgfunc. The function should accept three arguments. Assume the arguments are numbers. The function should calculate and output the average of the three numbers.
- 5. Create a script file, minmax. In the file, create a shell script, min. It should accept two arguments, assumed to be numbers. The function is to output the lesser of the two arguments. For example, if 5 and 10 are passed to the function, it should output 5.
- 6. Edit the minmax file you created in Discovery Exercise 6. Add a shell function named max. It should accept two arguments, assumed to be numbers. The function is to output the greater of the two arguments. For example, if 8 and 4 are passed to the function, it should output 8.

## Exploring the UNIX Utilities

Your supervisor at Dominion Consulting asks you to accomplish several computer tasks, including creating a bootable floppy disk, making backups on floppy disks, auditing system performance, analyzing hard disk storage, and removing unnecessary files. Further, you have been asked to create a man page to describe the Phmenu program that you wrote in Chapter 7.

### LESSON A

**Objectives**

In this lesson you will:

- Define the classifications of the UNIX utility programs
- Duplicate a floppy disk
- Create a "bootable floppy" to boot the system in case of emergency
- Determine hard disk usage and available free space
- Locate and remove unnecessary files from the hard disk
- Display the CPU status and internal memory usage

## Using the UNIX Utilities

In this chapter, you continue to explore UNIX utilities. Utilities are designed to provide basic services to UNIX users, just like your local utility companies provide basic services (e.g., electricity and running water) to your community. This chapter lets you practice using UNIX commands and utilities, such as using the man command with UNIX's text formatting utilities. Before you can begin to carry out your assigned tasks for Dominion Consulting, you need to learn more about UNIX utilities.

## Understanding UNIX Utilities

UNIX utilities let you create and manage files, run programs, produce reports, and generally interact with the system. Beyond these basics, the utility programs offer a full range of services that let you monitor and maintain the system and recover from a wide range of errors. UNIX utilities are classified into seven major function areas dictated by user needs: file processing, networking, communications, system status, programming, source code management, and miscellaneous. UNIX utilities are programs, but they are usually referred to as commands.

> Note: For the sake of completeness, this chapter contains some references and commentary about utilities in general, but it concentrates on those utilities that relate to file processing, system status, and miscellaneous tasks.

Utility programs are distinguished from other operating system programs in that they are "add-ons" and not part of the UNIX shells or a component of the kernel. Utilities are also unique because they are exclusively dedicated to improving computer performance for the benefit of users. New utility programs are continually being added as developers find better and faster ways to make UNIX run more efficiently. Finally, most UNIX utilities are small programs that often consist of only one command.

## Classifying UNIX Utility Programs

Utilities can be classified in several categories, as some work exclusively with UNIX files, others handle network tasks, and still others are designed to help programmers. File processing utilities, listed in Table 8-1, is the largest category. These utilities display and manipulate files.

| Utility | Brief Description of Function |
| :--- | :--- |
| afio | Creates an archive or restores files from archive |
| awk | Processes files |
| cat | Displays or joins files |
| cmp | Compares two files |
| comm | Compares sorted files and shows differences |
| cp | Copies files |
| cpio | Copies and backs up files to an archive |
| cut | Selects characters or fields from input lines |
| dd | Copies and converts input records |
| diff | Compares two text files and shows differences |
| fdformat | Formats a floppy disk at a low level |
| find | Finds files within file tree |
| fmt | Formats text very simply |
| grep | Matches patterns in a file |
| groff | Processes embedded text formatting codes |
| gzip | Compresses or decompresses files |
| head | Displays the first part of a file |
| ispell | Checks one or more files for spelling errors |
| less | Displays text files (pauses when screen is full) |
| ln | Creates a link to a file |
| lpr | Prints file (hard copy) |
| ls | Lists file and directory names and attributes |
| man | Displays documentation for commands |
| mkdir | Creates a new directory |
| mkfs | Builds a UNIX file system |
| mv | Renames and moves files and directories |
| od | Formats and displays data from a file |
| paste | Concatenates files horizontally |
| pr | Formats text files for printing and displays them |
| rdev | Queries or sets the root image device |
| rm | Removes files |
| rmdir | Removes directory |
| sed | Edits streams (non-interactive) |
| sort | Sorts or merges files |
| tail | Displays the last lines of files |
| tar | Copies and backs up files to a tape archive |
| touch | Changes file modification dates |
| uniq | Displays unique lines of sorted file |
| wc | Counts lines, words, and bytes |

Table 8-1: File processing utilities

System status utilities, listed in Table 8-2, is the second largest category. It includes utilities that display and alter the status of files, disks, and the overall system. These utilities let you know who is online, the names and status of running processes, the amount of hard disk space available, and where to find other commands you need to run.

| Utility | Brief Description of Function |
| :--- | :--- |
| chgrp | Changes the group associated with a file |
| chmod | Changes the access permissions of a file |
| chown | Changes the owner of a file |
| date | Sets and displays date and time |
| df | Displays the amount of free space remaining on disk |
| du | Summarizes file space usage |
| file | Determines file type (e.g., shell script, executable, ASCII text, and others) |
| finger | Displays detailed information about users who are logged on |
| free | Displays amount of free and used memory in the system |
| kill | Terminates a running process |
| ps | Displays process status by process identification number and name |
| sleep | Suspends execution for a specified time |
| top | Dynamically displays process status, like ps, but in real time |
| w | Displays detailed information about the users who are logged on |
| who | Displays brief information about the users who are logged on |

Table 8-2: System status utilities

Network utilities, listed in Table 8-3, consist of the essential commands for communicating and sharing information on a network.

| Utility | Brief Description of Function |
| :--- | :--- |
| ftp | Transfers files over a network |
| rcp | Remotely copies a file from network computer |
| rlogin | Logs on to a remote computer |
| rsh | Executes commands on a remote computer |
| rwho | Displays the names of users attached to a network |
| telnet | Connects to remote computer on a network |

Table 8-3: Network utilities
