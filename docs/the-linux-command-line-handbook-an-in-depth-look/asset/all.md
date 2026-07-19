![image](Images/image-KOJIXABG.png)

The Linux Command Line Handbook : An In-Depth Look

Elena Alexandrov

Published by CCL Publishing, 2023.

While every precaution has been taken in the preparation of this book, the publisher assumes no responsibility for errors or omissions, or for damages resulting from the use of the information contained herein.

THE LINUX COMMAND LINE HANDBOOK : AN IN-DEPTH LOOK

First edition. July 20, 2023.

Copyright © 2023 Elena Alexandrov.

Written by Elena Alexandrov.

## Contents

[introduction](#chapter0002.html)

[Why Use The Command Line?](#chapter0003.html)

[What This Book Is About](#chapter0004.html)

[How To Read This Book](#chapter0005.html)

[1 – Learning The Shell](#chapter0006.html)

[What Is The Shell?](#chapter0007.html)

[Terminal Emulators](#chapter0008.html)

[Try Some Simple Commands](#chapter0009.html)

[Ending A Terminal Session](#chapter0010.html)

[2 – Navigation](#chapter0011.html)

[Understanding The File System Tree](#chapter0012.html)

[The Current Working Directory](#chapter0013.html)

[Listing The Contents Of A Directory](#chapter0014.html)

[Changing The Current Working Directory](#chapter0015.html)

[Absolute Pathnames](#chapter0016.html)

[Relative Pathnames](#chapter0017.html)

[Some Helpful Shortcuts](#chapter0018.html)

[3 – Exploring The System.](#chapter0019.html)

[Options And Arguments](#chapter0020.html)

[Long Format](#chapter0021.html)

[Determining A File's Type With file](#chapter0022.html)

[Viewing File Contents With less](#chapter0023.html)

[Symbolic Links](#chapter0024.html)

[Hard Links](#chapter0025.html)

[Character Ranges](#chapter0026.html)

[Wildcards Work In The GUI Too](#chapter0027.html)

[mkdir – Create Directories](#chapter0028.html)

[cp – Copy Files And Directories](#chapter0029.html)

[mv – Move And Rename Files](#chapter0030.html)

[rm – Remove Files And Directories](#chapter0031.html)

[ln – Create Links](#chapter0032.html)

[5 – Working With Commands.](#chapter0033.html)

[Identifying Commands](#chapter0034.html)

[type – Display A Command's Type](#chapter0035.html)

[which – Display An Executable's Location](#chapter0036.html)

[help – Get Help For Shell Builtins](#chapter0037.html)

[—help – Display Usage Information](#chapter0038.html)

[man – Display A Program's Manual Page](#chapter0039.html)

[apropos – Display Appropriate Commands](#chapter0040.html)

[whatis – Display A Very Brief Description Of A Command](#chapter0041.html)

[info – Display A Program's Info Entry](#chapter0042.html)

[Creating Your Own Commands With alias](#chapter0043.html)

[6 – Redirection](#chapter0044.html)

[Standard Input, Output, And Error](#chapter0045.html)

[Redirecting Standard Output](#chapter0046.html)

[Redirecting Standard Error](#chapter0047.html)

[Redirecting Standard Output And Standard Error To One File](#chapter0048.html)

[Disposing Of Unwanted Output](#chapter0049.html)

[/dev/null In Unix Culture](#chapter0050.html)

[Redirecting Standard Input](#chapter0051.html)

[cat – Concatenate Files](#chapter0052.html)

[Pipelines](#chapter0053.html)

[The Difference Between > and |](#chapter0054.html)

[Filters](#chapter0055.html)

[uniq - Report Or Omit Repeated Lines](#chapter0056.html)

[wc – Print Line, Word, And Byte Counts](#chapter0057.html)

[grep – Print Lines Matching A Pattern](#chapter0058.html)

[head / tail – Print First / Last Part Of Files](#chapter0059.html)

[tee – Read From Stdin And Output To Stdout And Files](#chapter0060.html)

[7 – Seeing The World As The Shell Sees It..](#chapter0061.html)

[Pathname Expansion](#chapter0062.html)

[Pathname Expansion Of Hidden Files](#chapter0063.html)

[Tilde Expansion](#chapter0064.html)

[Arithmetic Expansion](#chapter0065.html)

[Brace Expansion](#chapter0066.html)

[Parameter Expansion](#chapter0067.html)

[Command Substitution](#chapter0068.html)

[Quoting](#chapter0069.html)

[Double Quotes](#chapter0070.html)

[Single Quotes](#chapter0071.html)

[Escaping Characters](#chapter0072.html)

[Backslash Escape Sequences](#chapter0073.html)

[8 – Advanced Keyboard Tricks.](#chapter0074.html)

[Command Line Editing](#chapter0075.html)

[Cursor Movement](#chapter0076.html)

[Completion](#chapter0077.html)

[Using History](#chapter0078.html)

[Searching History](#chapter0079.html)

[History Expansion](#chapter0080.html)

[script](#chapter0081.html)

[9 – Permissions](#chapter0082.html)

[Owners and Group Members](#chapter0083.html)

[Reading, Writing, And Executing](#chapter0084.html)

[chmod – Change File Mode](#chapter0085.html)

[Setting File Mode With The GUI](#chapter0086.html)

[umask – Set Default Permissions](#chapter0087.html)

[Changing Identities](#chapter0088.html)

[su – Run A Shell With Substitute User And Group IDs](#chapter0089.html)

[sudo – Execute A Command As Another User](#chapter0090.html)

[Ubuntu And sudo](#chapter0091.html)

[chown – Change File Owner And Group](#chapter0092.html)

[chgrp – Change Group Ownership](#chapter0093.html)

[Exercising Our Privileges](#chapter0094.html)

[10 – Processes.](#chapter0095.html)

[Viewing Processes](#chapter0096.html)

[Viewing Processes Dynamically With top](#chapter0097.html)

[Controlling Processes](#chapter0098.html)

[Interrupting A Process](#chapter0099.html)

[Putting A Process In The Background](#chapter0100.html)

[Returning A Process To The Foreground](#chapter0101.html)

[Stopping (Pausing) A Process](#chapter0102.html)

[Signals](#chapter0103.html)

[Sending Signals To Processes With kill](#chapter0104.html)

[Sending Signals To Multiple Processes With killall](#chapter0105.html)

[More Process Related Commands](#chapter0106.html)

[11 – The Environment](#chapter0107.html)

[What Is Stored In The Environment?](#chapter0108.html)

[Examining The Environment.](#chapter0109.html)

[How Is The Environment Established?](#chapter0110.html)

[What's In A Startup File?](#chapter0111.html)

[Which Files Should We Modify?](#chapter0112.html)

[Using A Text Editor](#chapter0113.html)

[12 –Introduction To vi](#chapter0114.html)

[Why We Should Learn vi](#chapter0115.html)

[Starting And Stopping vi](#chapter0116.html)

[Editing Modes](#chapter0117.html)

[Moving The Cursor Around](#chapter0118.html)

[Appending Text](#chapter0119.html)

[Opening A Line](#chapter0120.html)

[Deleting Text](#chapter0121.html)

[Cutting, Copying, And Pasting Text](#chapter0122.html)

[Joining Lines](#chapter0123.html)

[Search-And-Replace](#chapter0124.html)

[Editing Multiple Files](#chapter0125.html)

[13 – Customizing The Prompt](#chapter0126.html)

[Anatomy Of A Prompt](#chapter0127.html)

[Trying Some Alternative Prompt Designs](#chapter0128.html)

[Adding Color](#chapter0129.html)

[Terminal Confusion](#chapter0130.html)

[Moving The Cursor](#chapter0131.html)

[Saving The Prompt](#chapter0132.html)

[14 – Storage Media](#chapter0133.html)

[Mounting And Unmounting Storage Devices](#chapter0134.html)

[Viewing A List Of Mounted File Systems](#chapter0135.html)

[Determining Device Names](#chapter0136.html)

[Creating New File Systems](#chapter0137.html)

[Manipulating Partitions With fdisk](#chapter0138.html)

[Creating A New File System With mkfs](#chapter0139.html)

[Testing And Repairing File Systems](#chapter0140.html)

[Formatting Floppy Disks](#chapter0141.html)

[Moving Data Directly To/From Devices](#chapter0142.html)

[Creating CD-ROM Images](#chapter0143.html)

[Writing CD-ROM Images](#chapter0144.html)

![image](Images/image-KOJIXABG.png)

## introduction

![image](Images/image-8OLLAO0U.png)

Welcome to the fascinating world of Linux command line! This book is your comprehensive guide to exploring and mastering the powerful tools and commands that make up the Linux command line environment. Whether you're new to Linux or a seasoned user, this book will help you navigate the complexities of the command line and develop the skills necessary to become proficient in its use.

The Linux command line is a versatile and robust tool that allows you to perform a wide range of tasks, from simple file management to complex system administration functions. With the right knowledge and expertise, you can customize and optimize your Linux system, automate tasks, and even develop your own software.

In this book, we'll start with the fundamentals of working with the command line, including how to navigate directories and manage files. From there, we'll delve into more advanced topics like process management, network configuration, and shell scripting. By the time you finish reading, you'll have a solid understanding of how the Linux command line works and be able to use it to solve a wide variety of problems.

So, whether you're a student, a professional, or just a curious individual looking to expand your knowledge of Linux, this book is the perfect resource for you. Let's get started on your journey to mastering the Linux command line!

![image](Images/image-KOJIXABG.png)

## Why Use The Command Line?

![image](Images/image-8OLLAO0U.png)

The command line interface (CLI) has been around for decades and remains a fundamental part of Linux operating systems. It provides a text-based way to interact with the computer's operating system, allowing users to enter commands and receive feedback from the computer in the form of text responses. While many people prefer using a graphical user interface (GUI) to interact with their computer, the command line interface offers several advantages that make it an attractive option for certain tasks:

Speed: Using the command line interface can be faster than using a GUI because you can enter commands more quickly than navigating through a series of menus and options. This can be especially useful when you need to perform repetitive tasks or complete a task quickly.

Control: The command line interface gives you greater control over your computer than a GUI. You can execute complex commands, write scripts to automate tasks, and modify system settings with greater precision.

Accessibility: The command line interface can be accessed remotely, which makes it an essential tool for system administrators and developers. By using a command line interface, they can manage servers and computer clusters from a remote location.

Troubleshooting: When something goes wrong with a computer, the command line interface is often the best way to diagnose and fix the problem. System logs and processes can be viewed and monitored from the command line, allowing users to identify issues and resolve them quickly.

Learning: Learning to use the command line interface is an essential skill for anyone who wants to work with Linux operating systems. It can help users gain a deeper understanding of how the operating system works and develop valuable programming and automation skills.

Overall, while using the command line interface may not be the easiest way to interact with a computer, it offers many benefits to users who are willing to learn and invest time in using it effectively.

![image](Images/image-KOJIXABG.png)

## What This Book Is About

![image](Images/image-8OLLAO0U.png)

This book is a comprehensive guide to the Linux command line interface, designed to help readers develop the skills and knowledge needed to become proficient in using this essential tool.

Throughout the book, readers will learn how to use the Linux command line to perform a wide variety of tasks, from basic file management to advanced system administration functions. Topics covered in the book include navigating directories, working with files and directories, process management, network configuration, and shell scripting.

In addition to providing practical guidance on how to use the Linux command line, the book also explains the underlying concepts and principles that govern the Linux operating system. Readers will learn about the various command line utilities that are available in Linux, as well as the system architecture and file system organization that make it such a powerful and versatile platform.

Whether you are a beginner just starting out with Linux or a seasoned professional looking to expand your knowledge, this book is the perfect resource for anyone looking to master the Linux command line interface. With its clear explanations, real-world examples, and practical tips, this book will help readers gain the confidence and skills needed to use the Linux command line effectively and efficiently.

![image](Images/image-KOJIXABG.png)

## How To Read This Book

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

To get the most out of this book, we recommend that you read it from start to finish, in the order that the chapters are presented. Each chapter builds on the concepts and skills covered in the previous chapters, so reading the book in sequence will help you develop a solid foundation in the basics of the Linux command line interface.

As you read each chapter, we encourage you to follow along with the examples and exercises provided in the text. These exercises are designed to help you reinforce your understanding of the concepts covered in the chapter and develop your practical skills.

In addition to reading the text and completing the exercises, we also recommend that you experiment with the Linux command line on your own system. This will give you hands-on experience with the commands and techniques covered in the book, and help you develop a deeper understanding of how the Linux operating system works.

Finally, we encourage you to use this book as a reference guide as you continue to work with the Linux command line. The book includes a comprehensive index and glossary, making it easy to find the information you need when you need it.

By following these guidelines and making use of the exercises and examples provided in the text, you'll be well on your way to mastering the Linux command line interface and becoming a more effective Linux user.

![image](Images/image-KOJIXABG.png)

## 1 – Learning The Shell

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In this part of the book, you will learn how to navigate directories, work with files and directories, and use basic commands like ls, cd, and mkdir. You will also learn how to use redirection and pipelines to manage input and output, and how to use wildcards and regular expressions to work with files and directories more efficiently.

By the end of Part 1, you will have a solid foundation in the basics of the Linux shell, and be able to use it to perform a wide variety of tasks. This will set the stage for more advanced topics covered in later parts of the book.

![image](Images/image-KOJIXABG.png)

## What Is The Shell?

![image](Images/image-8OLLAO0U.png)

In the context of Linux, the shell is a program that provides a command line interface (CLI) for users to interact with the operating system. It is a text-based interface that allows users to enter commands and receive feedback from the system in the form of text responses.

The shell interprets the commands entered by the user and communicates with the operating system to carry out the requested actions. It provides a way for users to navigate directories, create and delete files, manage system processes, and perform a wide variety of other tasks.

There are several different shells available in Linux, including the Bourne-Again SHell (bash), the Z SHell (zsh), and the Korn SHell (ksh), among others. Each shell has its own set of features and capabilities, but they all provide a way for users to interact with the operating system using the command line interface.

Learning to use the shell is an essential skill for anyone working with Linux. It provides a powerful and flexible way to manage the operating system, and can be used to perform complex tasks, automate processes, and develop software.

![image](Images/image-KOJIXABG.png)

## Terminal Emulators

![image](Images/image-8OLLAO0U.png)

A terminal emulator is a program that allows users to access the shell and run command line utilities from a graphical user interface (GUI). It emulates a terminal or console, which is the text-based interface traditionally used to interact with the shell.

Terminal emulators provide a number of advantages over traditional terminals, including the ability to resize the terminal window, use multiple tabs or windows, and customize the terminal's appearance and behavior.

There are several terminal emulators available for Linux, including GNOME Terminal, Konsole, xterm, and Terminator, among others. Each emulator has its own set of features and capabilities, but they all provide a way for users to interact with the shell using a graphical interface.

In addition to providing access to the shell, terminal emulators can also be used to run other command line utilities, such as text editors, network utilities, and system administration tools. This makes them a versatile and powerful tool for working with Linux.

![image](Images/image-KOJIXABG.png)

## Try Some Simple Commands

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

Sure, here are some simple commands that you can try in the Linux shell or terminal emulator:

pwd - This command prints the current working directory to the screen.

- This command lists the contents of the current directory.

cd - This command changes the current directory to the specified directory.

mkdir - This command creates a new directory with the specified name.

- This command creates a new empty file with the specified name.

- This command displays the contents of a file on the screen.

echo - This command displays a message on the screen.

- This command clears the screen.

To use these commands, open a shell or terminal emulator and type the command followed by any required arguments. For example, to list the contents of the current directory, you would type "ls" and press enter.

Keep in mind that Linux commands are case-sensitive, so make sure to type them exactly as shown. Also, be careful when using commands like "rm" (which deletes files) or "sudo" (which grants administrative privileges), as they can have serious consequences if used incorrectly.

![image](Images/image-KOJIXABG.png)

## Ending A Terminal Session

![image](Images/image-8OLLAO0U.png)

To end a terminal session in Linux, you can use the "exit" command. This command terminates the current shell session and returns you to the parent shell.

To use the "exit" command, simply type "exit" at the command prompt and press Enter. This will close the current shell session and any open terminal emulator windows associated with it.

If you have multiple terminal sessions open, you can use the "logout" command to end all of them at once. This command logs you out of the current shell and terminates all active shell sessions.

In some cases, you may also be able to close a terminal window by clicking the "X" button in the upper-right corner of the window. However, this will only close the window and not necessarily terminate the shell session running inside it. To make sure the session is properly terminated, it's always best to use the "exit" or "logout" command.

![image](Images/image-KOJIXABG.png)

2 – Navigation

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Understanding The File System Tree

![image](Images/image-8OLLAO0U.png)

In Linux, the file system is organized as a hierarchical tree structure, with the root directory at the top of the tree. This root directory is represented by a forward slash ("/") character, and all other directories and files in the system are located somewhere within this tree structure.

The file system tree is organized into a number of standard directories, each with a specific purpose. Some of the most commonly used directories in the file system include:

/bin - This directory contains essential system utilities and programs that are required for basic system operation.

/etc - This directory contains system configuration files, such as network settings, user accounts, and system startup scripts.

- This directory contains the home directories of individual users on the system.

/lib - This directory contains shared libraries that are used by system programs and utilities.

/opt - This directory contains optional software packages that are not part of the core system.

/tmp - This directory is used for temporary files that are created by programs and utilities.

/usr - This directory contains additional system utilities and programs, as well as user documentation.

/var - This directory contains variable data files, such as system logs and spool files.

Understanding the organization of the file system tree is an essential skill for working with Linux, as it provides a framework for navigating and managing files and directories on the system. By learning how to navigate the file system tree using the shell, you can become a more effective Linux user and administrator.

![image](Images/image-KOJIXABG.png)

## The Current Working Directory

![image](Images/image-8OLLAO0U.png)

In Linux, the current working directory refers to the directory that you are currently located in within the file system tree. When you open a new shell or terminal emulator window, the default working directory is usually your home directory.

You can use the "pwd" command to display the full path of the current working directory. For example, if you are currently located in the /home/user/Documents directory, typing "pwd" at the command prompt will display "/home/user/Documents" on the screen.

You can use the "cd" command to change the current working directory to a different directory within the file system tree. For example, if you want to change the current working directory to the /home/user/Pictures directory, you would type "cd /home/user/Pictures" at the command prompt and press enter.

It's important to keep track of the current working directory when navigating the file system tree, as many shell commands and utilities operate on the current directory by default. By understanding and managing the current working directory, you can become a more efficient and effective Linux user.

![image](Images/image-KOJIXABG.png)

## Listing The Contents Of A Directory

![image](Images/image-8OLLAO0U.png)

In Linux, you can use the "ls" command to list the contents of a directory. By default, the "ls" command will list the files and directories in the current working directory.

To list the contents of a specific directory, you can include the directory path as an argument to the "ls" command. For example, if you want to list the contents of the /home/user/Documents directory, you would type "ls /home/user/Documents" at the command prompt and press enter.

The "ls" command provides several options that can be used to modify the output format or display additional information about the files and directories listed. For example, you can use the "-l" option to display the files and directories in a long format, which includes additional information such as file permissions, owner, and size. You can use the "-a" option to display all files and directories, including hidden files.

![image](Images/image-KOJIXABG.png)

## Changing The Current Working Directory

![image](Images/image-8OLLAO0U.png)

you can use the "cd" command to change the current working directory to a different directory within the file system tree. The "cd" command stands for "change directory".

To use the "cd" command, simply type "cd" followed by the directory path that you want to change to. For example, to change the current working directory to the /home/user/Documents directory, you would type "cd /home/user/Documents" at the command prompt and press enter.

You can use various shortcuts with the "cd" command to make navigating the file system tree faster and more efficient. For example, typing "cd" followed by a single dash ("-") will change the current working directory to the previous directory you were in, and typing "cd" followed by two periods ("..") will change the current working directory to the parent directory of the current directory.

It's important to keep track of the current working directory when using the "cd" command, as many other shell commands and utilities operate on the current directory by default. By mastering the use of the "cd" command and its various shortcuts, you can become a more efficient and effective Linux user, able to quickly and easily navigate the file system tree.

![image](Images/image-KOJIXABG.png)

## Absolute Pathnames

![image](Images/image-8OLLAO0U.png)

In Linux, an absolute pathname is a full path that specifies the exact location of a file or directory within the file system tree. It starts from the root directory ("/") and includes all directories and subdirectories leading to the file or directory in question.

For example, the absolute pathname for a file named "example.txt" located in the /home/user/Documents directory would be "/home/user/Documents/example.txt".

You can use absolute pathnames to specify the exact location of files or directories when running shell commands or using utilities. Absolute pathnames are useful when you need to specify a file or directory that is not located in the current working directory.

To use an absolute pathname in a shell command, simply type the full pathname instead of just the file or directory name. For example, to list the contents of the /home/user/Documents directory using an absolute pathname, you would type "ls /home/user/Documents" at the command prompt and press enter.

![image](Images/image-CJJTTG07.png)

Let's say you have a file named "example.txt" located in the /home/user/Documents directory. If you want to open this file using a text editor like nano, you could use the following command:

![image](Images/image-PHI5A8LF.png)

This command specifies the absolute pathname of the file, which includes the full directory path leading to the file. When you run this command, nano will open the file "example.txt" located in the /home/user/Documents directory.

Note that you could also use a relative pathname to open the same file, but the relative pathname would depend on your current working directory. Using an absolute pathname ensures that you can always locate the file, regardless of your current working directory.

![image](Images/image-KOJIXABG.png)

## Relative Pathnames

![image](Images/image-8OLLAO0U.png)

In Linux, a relative pathname is a path that specifies the location of a file or directory relative to the current working directory. It does not include the full path to the file or directory from the root directory ("/").

For example, if your current working directory is /home/user/Documents and you want to access a file named "example.txt" located in the /home/user/Pictures directory, you could use the relative pathname "../Pictures/example.txt". The ".." indicates the parent directory of the current working directory, and the subsequent "/Pictures/example.txt" specifies the file location relative to the parent directory.

You can use relative pathnames to specify files or directories that are located near the current working directory. They are particularly useful when you want to navigate between directories quickly and efficiently.

To use a relative pathname in a shell command, simply type the path relative to the current working directory instead of the full pathname. For example, to list the contents of a directory named "images" located in the parent directory of the current working directory, you would type "ls ../images" at the command prompt and press enter.

Let's say your current working directory is /home/user/Documents, and you want to open a file named "example.txt" located in a subdirectory named "notes". You could use the following command:

![image](Images/image-Q89KIKAL.png)

This command specifies the relative pathname of the file, which includes the path to the file relative to the current working directory. When you run this command, nano will open the file "example.txt" located in the "notes" subdirectory of the current working directory.

![image](Images/image-KOJIXABG.png)

## Some Helpful Shortcuts

![image](Images/image-8OLLAO0U.png)

In Linux, there are several helpful shortcuts that you can use to navigate the file system tree and work more efficiently in the shell. Here are a few of the most commonly used shortcuts:

Tab Completion - If you start typing a file or directory name and press the Tab key, the shell will automatically complete the name for you if it is unique. If the name is not unique, pressing Tab twice will display a list of possible completions.

Ctrl + A - This shortcut moves the cursor to the beginning of the current command line.

Ctrl + E - This shortcut moves the cursor to the end of the current command line.

Ctrl + U - This shortcut deletes the entire current command line.

Ctrl + R - This shortcut opens the reverse search history function, which allows you to search for previous commands.

Ctrl + C - This shortcut interrupts the current process or command.

![image](Images/image-KOJIXABG.png)

3 – Exploring The System.

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Options And Arguments

![image](Images/image-8OLLAO0U.png)

In Linux, shell commands typically consist of a command name, followed by options and arguments. Options modify the behavior of the command, while arguments specify the files, directories, or other inputs that the command should operate on.

Options are usually preceded by a hyphen ("-") or double hyphen ("—") and are case-sensitive. They can be combined together or used individually. For example, the "ls" command has several options, including "-l" to display the contents of a directory in a long format, and "-a" to display hidden files.

Arguments are typically provided after the command and options, and can take various forms depending on the command. For example, when using the "cp" command to copy a file, the first argument is the source file, and the second argument is the destination file.

Some commands also accept flags as arguments, which are preceded by a hyphen and modify the behavior of the command in a specific way.

Suppose you want to list the contents of a directory in long format and display hidden files. To do this, you would use the following command:

bash

ls -la /home/user/Documents

In this command, the "-l" option is used to display the contents of the directory in long format, and the "-a" option is used to display hidden files. The argument "/home/user/Documents" specifies the directory whose contents you want to list.

When you run this command, the shell will display a detailed list of the contents of the "/home/user/Documents" directory, including hidden files, in long format. By using options and arguments with the "ls" command, you can customize the output to suit your needs and gain greater insight into the contents of the file system tree.

![image](Images/image-KOJIXABG.png)

## Long Format

![image](Images/image-8OLLAO0U.png)

In Linux, the long format option ("-l") for the "ls" command displays the contents of a directory in a detailed and informative format. When using this option, the "ls" command will display the following information for each file or directory in the directory:

File Permissions - A series of ten characters that indicate the file type and permissions for the owner, group, and other users.

Number of links - The number of hard links to the file.

Owner - The username of the owner of the file.

Group - The name of the group that owns the file.

File Size - The size of the file in bytes.

Modification Time - The date and time when the file was last modified.

Filename - The name of the file or directory.

Here's an example of what the long format output for the "ls" command might look like:

![image](Images/image-399J9JNC.png)

In this example, the file "example.txt" has the following characteristics:

File type: "-rw-r—r—" indicates that the file is a regular file, and that the owner can read and write to the file, while members of the group and other users can only read the file.

Number of links: "1" indicates that the file has only one hard link.

Owner: "user" indicates that the file is owned by the user "user".

Group: "users" indicates that the file belongs to the "users" group.

File size: "12345" indicates that the file is 12,345 bytes in size.

Modification time: "Jan 1 10:00" indicates that the file was last modified on January 1 at 10:00 AM.

Filename: "example.txt" indicates the name of the file.

By mastering the use of the long format option for the "ls" command, you can gain greater insight into the contents of a directory and become a more effective Linux user.

![image](Images/image-KOJIXABG.png)

## Determining A File's Type With file

![image](Images/image-8OLLAO0U.png)

In Linux, the "file" command is used to determine the type of a file, based on its contents. The "file" command can identify a wide variety of file types, including text files, images, audio files, executables, and more.

To use the "file" command, simply type "file" followed by the name of the file you want to identify. For example, to determine the type of a file named "example.jpg", you would type "file example.jpg" at the command prompt and press enter.

The "file" command will then display a brief description of the file type, based on the contents of the file. For example, if "example.jpg" is an image file, the "file" command might display "JPEG image data, JFIF standard 1.01".

The "file" command is particularly useful when you encounter a file with an unknown or unusual file extension and need to determine its type before opening or manipulating it. By mastering the use of the "file" command, you can become a more efficient and effective Linux user, able to quickly and easily identify files and work with them more effectively.

![image](Images/image-KOJIXABG.png)

## Viewing File Contents With less

![image](Images/image-8OLLAO0U.png)

In Linux, the "less" command is used to view the contents of a file within the shell, without opening a separate text editor or program. The "less" command is particularly useful for viewing large files or files with long lines of text.

To use the "less" command, simply type "less" followed by the name of the file you want to view. For example, to view the contents of a file named "example.txt", you would type "less example.txt" at the command prompt and press enter.

Once you have opened the file with "less", you can use various keyboard shortcuts to navigate and search through the file. Some common shortcuts include:

Up Arrow and Down Arrow - Scroll up and down within the file.

Page Up and Page Down - Scroll up and down one full screen within the file.

/ - Search forward for a specific string within the file.

? - Search backward for a specific string within the file.

q - Quit the "less" command and return to the shell.

Suppose you have a file named "example.txt" that contains a large amount of text. To view the contents of this file within the shell using the "less" command, you would type the following command:

![image](Images/image-348HE8MZ.png)

When you run this command, the shell will display the contents of the "example.txt" file within the terminal window, using the "less" program. You can then use the arrow keys to scroll up and down within the file, or use the "Page Up" and "Page Down" keys to move through the file more quickly.

If you want to search for a specific string within the file, you can type "/" followed by the string you want to search for. For example, to search for the word "Linux" within the file, you would type "/Linux" and press enter. The "less" command will then highlight the first occurrence of the word "Linux" within the file, and you can use the "n" key to find the next occurrence of the string.

![image](Images/image-KOJIXABG.png)

## Symbolic Links

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, a symbolic link (or "symlink") is a special type of file that acts as a reference or pointer to another file or directory. Symbolic links can be created using the "ln" command with the "-s" option.

Here's an example of how to create a symbolic link:

![image](Images/image-IMXJ5N4O.png)

In this example, "/path/to/original" is the path to the original file or directory that you want to link to, and "/path/to/link" is the path where you want to create the symbolic link.

When you create a symbolic link, the link appears in the file system as a separate file, but it actually points to the original file or directory. When you access the symbolic link, the operating system transparently redirects you to the original file or directory, allowing you to work with the file or directory as if it were located at the link's location.

Symbolic links are useful for a variety of purposes, such as creating shortcuts to commonly-used files or directories, organizing files and directories, and allowing multiple users to access the same files or directories without duplicating them. However, it's important to note that symbolic links can be broken if the original file or directory is moved or deleted, so it's important to use them with care and keep track of their dependencies.

![image](Images/image-KOJIXABG.png)

## Hard Links

![image](Images/image-8OLLAO0U.png)

In Linux, a hard link is a special type of link that points to the same underlying file as the original file, rather than creating a separate reference file like a symbolic link. Hard links can be created using the "ln" command without any special options.

Here's an example of how to create a hard link:

![image](Images/image-M0FY3HKF.png)

In this example, "/path/to/original" is the path to the original file that you want to link to, and "/path/to/link" is the path where you want to create the hard link.

When you create a hard link, the link and the original file both point to the same location on the disk, and changes made to either file are reflected in both files. This means that the hard link can be used to access the same file from multiple locations, without creating a separate copy of the file.

![image](Images/image-KOJIXABG.png)

## Character Ranges

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux shell commands, you can use character ranges to specify a range of characters to include in a command or search. A character range is a sequence of characters enclosed in square brackets, with a hyphen separating the starting and ending characters of the range.

For example, to list all files in the current directory that start with the letters "a" through "f", you could use the following command:

![image](Images/image-WA9XHBXY.png)

In this command, "[a-f]" is the character range that specifies the letters to include, and the "*" specifies that any file name that starts with the specified characters should be included.

Here are some more examples of how to use character ranges in Linux shell commands:

[0-9] - Includes all numeric characters from 0 through 9.

[a-z] - Includes all lowercase alphabetical characters from a through z.

[A-Z] - Includes all uppercase alphabetical characters from A through Z.

[abc] - Includes the individual characters "a", "b", and "c".

[!a-z] - Includes all characters that are not lowercase alphabetical characters from a through z.

![image](Images/image-KOJIXABG.png)

## Wildcards Work In The GUI Too

![image](Images/image-8OLLAO0U.png)

Yes, wildcards are not just limited to the command line, they can also be used in the Graphical User Interface (GUI) to search for files and perform actions on them.

For example, in the file manager in Linux, you can use the asterisk (*) as a wildcard to search for files or folders that match a certain pattern. Suppose you want to find all files in a folder that have "report" in their filename, you can use the following search pattern: "report". This will find all files that have "report" in their filename, whether it's at the beginning, middle or end of the filename.

Similarly, you can use other wildcards such as "?" to represent a single character, or "[ ]" to represent a range of characters in a filename.

Wildcards can also be used to perform batch actions on files in the GUI, such as renaming or moving a group of files that match a certain pattern.

![image](Images/image-KOJIXABG.png)

## mkdir – Create Directories

![image](Images/image-8OLLAO0U.png)

In Linux, the "mkdir" command is used to create new directories (folders) within the file system. The basic syntax of the command is as follows:

![image](Images/image-7IY9IDUW.png)

For example, to create a new directory called "my_directory", you would type the following command:

![image](Images/image-YCOG07JC.png)

If you want to create a directory with multiple levels of subdirectories, you can use the "-p" option to create all necessary parent directories as well. For example, to create a directory called "my_directory" with a subdirectory called "my_subdirectory", you would type the following command:

![image](Images/image-L2M399W9.png)

This would create the "my_directory" directory if it didn't already exist, and then create the "my_subdirectory" directory within it.

The "mkdir" command also supports various options that can be used to modify its behavior, such as setting permissions or creating directories with a specific group or owner.

![image](Images/image-KOJIXABG.png)

## cp – Copy Files And Directories

![image](Images/image-8OLLAO0U.png)

In Linux, the "cp" command is used to copy files and directories from one location to another within the file system. The basic syntax of the command is as follows:

![image](Images/image-27N9BQEZ.png)

For example, to copy a file called "file.txt" from the current directory to a directory called "backup", you would type the following command:

![image](Images/image-Q4XMOAAP.png)

If you want to copy a directory and its contents to another location, you can use the "-r" option to copy the directory recursively. For example, to copy a directory called "my_directory" and all of its contents to a directory called "backup", you would type the following command:

![image](Images/image-6CVV84F7.png)

The "cp" command also supports various options that can be used to modify its behavior, such as preserving file attributes or copying only new or modified files.

![image](Images/image-KOJIXABG.png)

## mv – Move And Rename Files

![image](Images/image-8OLLAO0U.png)

In Linux, the "mv" command is used to move or rename files and directories within the file system. The basic syntax of the command is as follows:

![image](Images/image-JODG766T.png)

For example, to move a file called "file.txt" from the current directory to a directory called "backup", you would type the following command:

![image](Images/image-ZUWZXVHW.png)

If you want to rename a file, you can simply specify the new name as the destination file. For example, to rename a file called "file.txt" to "newfile.txt", you would type the following command:

![image](Images/image-8BCY1D53.png)

If you want to move or rename a directory and its contents, you can use the "-r" option to move or rename the directory recursively. For example, to move a directory called "my_directory" and all of its contents to a directory called "backup", you would type the following command:

![image](Images/image-3DRIJCRM.png)

The "mv" command can also be used to move files or directories from one location to another and rename them at the same time.

![image](Images/image-KOJIXABG.png)

## rm – Remove Files And Directories

![image](Images/image-8OLLAO0U.png)

In Linux, the "rm" command is used to remove files and directories from the file system. The basic syntax of the command is as follows:

![image](Images/image-16AOI15I.png)

For example, to remove a file called "file.txt" from the current directory, you would type the following command:

![image](Images/image-KRSVSC20.png)

If you want to remove a directory and all of its contents, you can use the "-r" option to remove the directory recursively. For example, to remove a directory called "my_directory" and all of its contents, you would type the following command:

![image](Images/image-GRJF4VM7.png)

It's important to be careful when using the "rm" command, as it can permanently delete files and directories from the file system without the ability to recover them. To help prevent accidental deletion of important files, you can use the "-i" option to prompt for confirmation before deleting each file or directory.

![image](Images/image-KOJIXABG.png)

## ln – Create Links

![image](Images/image-8OLLAO0U.png)

In Linux, the "ln" command is used to create hard or symbolic links between files. The basic syntax of the command is as follows:

![image](Images/image-XWQ1W6A1.png)

For example, to create a hard link between a file called "file.txt" and a link file called "link.txt", you would type the following command:

![image](Images/image-64DEL7LF.png)

If you want to create a symbolic link instead of a hard link, you can use the "-s" option. For example, to create a symbolic link between a file called "file.txt" and a link file called "link.txt", you would type the following command:

![image](Images/image-HPJNQ8XX.png)

Hard links and symbolic links behave differently. A hard link is simply another name for the same file, and changes made to one file are reflected in the other. A symbolic link is a special file that contains a reference to another file or directory, and changes made to the original file are not reflected in the symbolic link.

![image](Images/image-KOJIXABG.png)

## 5 – Working With Commands.

![image](Images/image-8OLLAO0U.png)

Commands in Linux are the instructions that you give to the computer to perform a specific action or task. These commands can be executed in the shell environment, which is the command line interface that allows you to interact with the Linux operating system.

There are thousands of commands available in Linux, each with its own syntax and set of options and arguments. Some of the most common commands are used to manipulate files and directories, manage system resources, monitor system performance, and control user access and permissions.

To use a command in Linux, you simply type the command name and any necessary options and arguments into the shell environment and press Enter. The command is then executed by the computer, and any output or results are displayed in the shell environment.

![image](Images/image-KOJIXABG.png)

## Identifying Commands

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, there are several ways to identify commands, including:

Using the "which" command - The "which" command is used to display the location of a command's executable file. For example, to find the location of the "ls" command, you would type the following command:

![image](Images/image-W8TJX66H.png)

Using the "type" command - The "type" command is used to display information about a command, including its location and whether it's a built-in command or an external command. For example, to find information about the "ls" command, you would type the following command:

![image](Images/image-K5PDUW3B.png)

Using the "help" command - Many commands include built-in help that can be accessed using the "help" command. For example, to view the help information for the "ls" command, you would type the following command:

![image](Images/image-CJJTTG07.png)![image](Images/image-G7F8C1IA.png)

Using the "man" command - The "man" command is used to display the manual page for a command, which includes detailed information about its usage, options, and arguments. For example, to view the manual page for the "ls" command, you would type the following command:

![image](Images/image-CJJTTG07.png)![image](Images/image-01ZIXNA3.png)![image](Images/image-KOJIXABG.png)

## type – Display A Command's Type

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "type" command is used to display information about a command, including its location and whether it's a built-in command or an external command.

The basic syntax of the command is as follows:

![image](Images/image-EH3Q4KD7.png)

For example, to display information about the "ls" command, you would type the following command:

![image](Images/image-2W92NDWL.png)

The output of the command will indicate whether "ls" is a built-in command or an external command, and will display the location of the command's executable file if it's an external command.

The "type" command can also be used to display information about shell keywords and aliases, as well as functions that have been defined in the shell environment.

![image](Images/image-KOJIXABG.png)

## which – Display An Executable's Location

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "which" command is used to display the location of an executable file associated with a command.

The basic syntax of the command is as follows:

![image](Images/image-CO9OJ8KW.png)

For example, to display the location of the "ls" command, you would type the following command:

![image](Images/image-2GJXAP7Y.png)

The output of the command will display the full path to the executable file associated with the "ls" command. This can be useful if you want to know which version of a command you're running, or if you want to modify the command's behavior by editing the executable file directly.

![image](Images/image-KOJIXABG.png)

## help – Get Help For Shell Builtins

![image](Images/image-8OLLAO0U.png)

In Linux, many shell built-in commands include built-in help that can be accessed using the "help" command.

The basic syntax of the command is as follows:

![image](Images/image-GJUIX8C7.png)

For example, to display help information for the "cd" command, you would type the following command:

![image](Images/image-7ABS07SX.png)

The output of the command will display information about the usage, options, and arguments of the specified built-in command.

Note that the "help" command only works for built-in commands, not external commands. For external commands, you can typically access help information using the "—help" or "-h" option, or by using the "man" command to view the command's manual page.

![image](Images/image-KOJIXABG.png)

## —help – Display Usage Information

![image](Images/image-8OLLAO0U.png)

In Linux, many commands include a built-in option to display usage information and help. This option is typically specified using "—help" or "-h".

The basic syntax of the command is as follows:

![image](Images/image-LA3KEDDW.png)

For example, to display usage information for the "ls" command, you would type the following command:

![image](Images/image-67SALJ87.png)

The output of the command will display information about the usage, options, and arguments of the specified command.

Note that not all commands include a built-in help option, and some may use different options, such as "-h" or "-?", to display help information. Additionally, some commands may not provide detailed help information, but rather a brief summary of the available options and arguments.

![image](Images/image-KOJIXABG.png)

## man – Display A Program's Manual Page

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "man" command is used to display a program's manual page, which provides detailed information about the program's usage, options, and arguments.

The basic syntax of the command is as follows:

![image](Images/image-EOB6H6TG.png)

For example, to display the manual page for the "ls" command, you would type the following command:

![image](Images/image-VFKZIUCC.png)

The output of the command will display detailed information about the "ls" command, including its usage, options, and arguments.

![image](Images/image-KOJIXABG.png)

## apropos – Display Appropriate Commands

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "apropos" command is used to display a list of appropriate commands based on a search term or keyword.

The basic syntax of the command is as follows:

![image](Images/image-668T0WBR.png)

For example, to display a list of commands related to file compression, you could use the following command:

![image](Images/image-9D5D9BPP.png)

The output of the command will display a list of commands related to file compression, including their names and a brief description of their functionality.

![image](Images/image-KOJIXABG.png)

## whatis – Display A Very Brief Description Of A Command

![image](Images/image-8OLLAO0U.png)

In Linux, the "whatis" command is used to display a very brief description of a command.

The basic syntax of the command is as follows:

![image](Images/image-D3GR6LTT.png)

For example, to display a brief description of the "ls" command, you would type the following command:

![image](Images/image-KFBIIEWN.png)

The output of the command will display a very brief description of the "ls" command, typically just a few words.

The "whatis" command is a quick and convenient way to get a general idea of what a command does, without having to wade through detailed help or manual pages. By mastering the use of the "whatis" command, you can become a more efficient and effective Linux user, able to quickly and easily get the information you need to perform a wide range of tasks within the shell environment.

![image](Images/image-KOJIXABG.png)

## info – Display A Program's Info Entry

![image](Images/image-8OLLAO0U.png)

In Linux, the "info" command is used to display a program's Info entry, which provides detailed information about the program's usage, options, and arguments in a structured, hypertext format.

The basic syntax of the command is as follows:

![image](Images/image-AW4VS6KV.png)

For example, to display the Info entry for the "ls" command, you would type the following command:

![image](Images/image-RNVS51BJ.png)

The output of the command will display the Info entry for the "ls" command, which includes a detailed overview of the command's functionality and usage, as well as hyperlinks to related sections and topics.

![image](Images/image-KOJIXABG.png)

## Creating Your Own Commands With alias

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "alias" command is used to create your own custom commands, which can be useful for simplifying common tasks or for creating shortcuts to frequently used commands.

The basic syntax of the command is as follows:

![image](Images/image-VX1KRJ0F.png)

For example, to create a new command called "ll" that is an alias for the "ls -l" command, you would type the following command:

![image](Images/image-KH02YA39.png)

Once the alias is created, you can use the new command just like any other command. For example, to use the "ll" command to list the contents of a directory in long format, you would type the following command:

![image](Images/image-L873L5BA.png)

The output of the command will be the same as if you had typed "ls -l directory_name".

By mastering the use of the "alias" command, you can become a more efficient and effective Linux user, able to create your own custom commands to simplify and streamline your workflow within the shell environment. However, it's important to note that aliases are specific to your current shell session and will not persist beyond your current session unless they are added to your shell configuration file (such as .bashrc).

![image](Images/image-KOJIXABG.png)

6 – Redirection

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Standard Input, Output, And Error

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, there are three standard streams of data that can be redirected using redirection operators:

Standard Input (stdin) - This is the stream of data that is used as input to a command. By default, stdin is read from the keyboard, but it can also be redirected to read from a file or another command's output.

Standard Output (stdout) - This is the stream of data that is produced as output by a command. By default, stdout is written to the terminal screen, but it can also be redirected to write to a file or another command's input.

Standard Error (stderr) - This is the stream of data that is produced as error output by a command. By default, stderr is written to the terminal screen along with stdout, but it can also be redirected to write to a file or to discard the output entirely.

The redirection operators ">" and ">>" are used to redirect stdout, "<" is used to redirect stdin, and "2>" and "&>" are used to redirect stderr and stdout+stderr, respectively.

![image](Images/image-KOJIXABG.png)

## Redirecting Standard Output

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the ">" and ">>" redirection operators are used to redirect standard output (stdout) from a command to a file.

The basic syntax of the ">" operator is as follows:

![image](Images/image-QPYAK9LK.png)

For example, to redirect the output of the "ls" command to a file called "directory_contents.txt", you would use the following command:

![image](Images/image-Z7IJN16A.png)

This would create a new file called "directory_contents.txt" containing the output of the "ls" command.

The basic syntax of the ">>" operator is similar to the ">" operator, but it appends the output to the end of the file rather than overwriting it:

![image](Images/image-AO5PC18B.png)

For example, to append the output of the "ls" command to an existing file called "directory_contents.txt", you would use the following command:

![image](Images/image-SMZCK9K2.png)

This would add the output of the "ls" command to the end of the "directory_contents.txt" file.

![image](Images/image-KOJIXABG.png)

## Redirecting Standard Error

![image](Images/image-8OLLAO0U.png)

In Linux, the "2>" and "&>" redirection operators are used to redirect standard error (stderr) from a command to a file.

The basic syntax of the "2>" operator is as follows:

![image](Images/image-186COK7U.png)

For example, to redirect the error output from the "ls" command to a file called "ls_errors.txt", you would use the following command:

![image](Images/image-KEC5E4EP.png)

This would create a new file called "ls_errors.txt" containing the error output of the "ls" command (in this case, an error message indicating that the specified directory does not exist).

The basic syntax of the "&>" operator is similar to the "2>" operator, but it redirects both standard output (stdout) and standard error (stderr) to the same file:

![image](Images/image-607IHPJX.png)

For example, to redirect both the output and error output from the "ls" command to a file called "ls_output.txt", you would use the following command:

![image](Images/image-0ED5I52P.png)

This would create a new file called "ls_output.txt" containing both the output and error output of the "ls" command.

![image](Images/image-KOJIXABG.png)

## Redirecting Standard Output And Standard Error To One File

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "&>" redirection operator is used to redirect both standard output (stdout) and standard error (stderr) from a command to the same file.

The basic syntax of the "&>" operator is as follows:

![image](Images/image-57N1TGY8.png)

For example, to redirect both the output and error output from the "ls" command to a file called "ls_output.txt", you would use the following command:

![image](Images/image-73W40IDI.png)

This would create a new file called "ls_output.txt" containing both the output and error output of the "ls" command.

![image](Images/image-KOJIXABG.png)

## Disposing Of Unwanted Output

![image](Images/image-8OLLAO0U.png)

In Linux, the "/dev/null" device file can be used to dispose of unwanted output from a command.

The "/dev/null" file is a special file that discards all data written to it and produces no output when read from. By redirecting output to "/dev/null", you can effectively discard unwanted output from a command.

The basic syntax for redirecting output to "/dev/null" is as follows:

![image](Images/image-C0SPK9TR.png)

For example, to discard the output of the "ls" command, you would use the following command:

![image](Images/image-U6KUWGC3.png)

This would effectively discard the output of the "ls" command, without writing it to a file or displaying it on the terminal screen.

![image](Images/image-KOJIXABG.png)

## /dev/null In Unix Culture

![image](Images/image-8OLLAO0U.png)

In Unix and Linux culture, the "/dev/null" device file has become an iconic symbol of the power and flexibility of the command line.

The "/dev/null" file is a special file that discards all data written to it and produces no output when read from. It is often used in shell scripts and commands to discard unwanted output or to prevent output from being displayed on the terminal screen.

Because the "/dev/null" file is such a powerful and versatile tool, it has become a popular topic of discussion and humor in the Unix and Linux community. References to "/dev/null" are often used in jokes and memes, and the file is sometimes referred to as the "black hole" of the system.

![image](Images/image-KOJIXABG.png)

## Redirecting Standard Input

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "<" redirection operator is used to redirect standard input (stdin) for a command from a file rather than from the keyboard.

The basic syntax of the "<" operator is as follows:

![image](Images/image-XELU9626.png)

For example, to use the contents of a file called "input.txt" as input to the "sort" command, you would use the following command:

![image](Images/image-WMFQABI6.png)

This would use the contents of the "input.txt" file as input to the "sort" command, rather than reading input from the keyboard.

![image](Images/image-KOJIXABG.png)

## cat – Concatenate Files

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "cat" command is used to concatenate files and display their contents on the terminal screen or redirect the output to a file using standard output (stdout) redirection.

The basic syntax of the "cat" command is as follows:

![image](Images/image-7PS20HUN.png)

For example, to concatenate the contents of two files, "file1.txt" and "file2.txt", and display the resulting output on the terminal screen, you would use the following command:

![image](Images/image-CP0ND4C3.png)

This would display the contents of both files on the terminal screen, one after the other.

Alternatively, to concatenate the contents of the two files and write the output to a new file called "output.txt", you would use the following command:

![image](Images/image-XXMNLBWF.png)

This would create a new file called "output.txt" containing the concatenated contents of the two files.

![image](Images/image-KOJIXABG.png)

## Pipelines

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, pipelines are a powerful feature that allow you to connect multiple commands together to process data in a series of stages.

A pipeline is created by connecting the output of one command to the input of another command using the "|" (pipe) symbol. The output of the first command is sent through the pipe to the input of the second command, and so on, until the end of the pipeline is reached.

The basic syntax of a pipeline is as follows:

![image](Images/image-4VD2K5MF.png)

For example, to find all files in the current directory with the ".txt" extension, sort the results alphabetically, and then display the sorted list on the terminal screen, you could use the following pipeline:

![image](Images/image-ATUV5KZZ.png)

This pipeline uses the "ls" command to list all files in the current directory, the "grep" command to filter the results to only include files with the ".txt" extension, and the "sort" command to sort the filtered results alphabetically.

![image](Images/image-KOJIXABG.png)

## The Difference Between > and |

![image](Images/image-8OLLAO0U.png)

In Linux, the ">" and "|" symbols are both used for redirection, but they serve different purposes.

The ">" symbol is used to redirect standard output (stdout) from a command to a file, overwriting the contents of the file if it already exists. For example, the following command redirects the output of the "ls" command to a file called "directory_contents.txt":

![image](Images/image-ZJAZCIVW.png)

In contrast, the "|" symbol is used to connect the output of one command to the input of another command in a pipeline. For example, the following command finds all files in the current directory with the ".txt" extension and then sorts the results alphabetically:

![image](Images/image-N555PQ9X.png)

In this pipeline, the output of the "ls" command is sent through the pipe to the input of the "grep" command, which filters the results to only include files with the ".txt" extension. The filtered results are then sent through the pipe to the input of the "sort" command, which sorts the results alphabetically.

In summary, the ">" symbol is used to redirect output to a file, while the "|" symbol is used to connect the output of one command to the input of another command in a pipeline.

![image](Images/image-KOJIXABG.png)

## Filters

![image](Images/image-8OLLAO0U.png)

In Linux, filters are commands that process and modify input data in some way and then output the modified data to the next stage of a pipeline.

Filters can be used to perform a wide variety of data processing tasks, such as searching for specific patterns in text data, sorting and filtering data by specific criteria, or converting data from one format to another.

Some common filters in Linux include:

"grep" - a command used to search for specific patterns in text data

"sort" - a command used to sort data in alphabetical or numerical order

"cut" - a command used to extract specific fields or columns from data

"awk" - a command used to manipulate and process text data in complex ways

"sed" - a command used to search for and replace specific patterns in text data

"tr" - a command used to translate or replace characters in text data

For example, to search for all lines in a text file that contain the word "Linux", you could use the following pipeline:

![image](Images/image-FV1UNC44.png)

This pipeline uses the "cat" command to display the contents of the "input.txt" file, and then passes the output through the pipe to the "grep" command, which searches for all lines that contain the word "Linux" and outputs them to the terminal screen.

![image](Images/image-KOJIXABG.png)

## uniq - Report Or Omit Repeated Lines

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "uniq" command is used to filter out repeated lines from input data and output only the unique lines.

The basic syntax of the "uniq" command is as follows:

![image](Images/image-BHNHRIJ3.png)

For example, to display the unique lines in a file called "input.txt", you would use the following command:

![image](Images/image-G6BYVAFG.png)

This would display the unique lines in the "input.txt" file, omitting any duplicate lines.

The "uniq" command can also be used with several options to modify its behavior. For example, the "-c" option can be used to count the number of occurrences of each unique line, and the "-d" option can be used to display only the lines that are repeated in the input data.

For example, to count the number of occurrences of each unique line in a file called "input.txt", you would use the following command:

![image](Images/image-VUYCQM4S.png)

This would display a list of unique lines in the "input.txt" file, along with the number of times each line appears.

![image](Images/image-KOJIXABG.png)

## wc – Print Line, Word, And Byte Counts

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "wc" command is used to count the number of lines, words, and bytes in a file or input data.

The basic syntax of the "wc" command is as follows:

![image](Images/image-DPZCXH7W.png)

For example, to display the number of lines, words, and bytes in a file called "input.txt", you would use the following command:

![image](Images/image-J6TZV69Z.png)

This would display the number of lines, words, and bytes in the "input.txt" file.

The "wc" command can also be used with several options to modify its behavior. For example, the "-l" option can be used to count only the number of lines, the "-w" option can be used to count only the number of words, and the "-c" option can be used to count only the number of bytes.

For example, to display only the number of lines in a file called "input.txt", you would use the following command:

![image](Images/image-L7UBI5Y4.png)

This would display only the number of lines in the "input.txt" file.

![image](Images/image-KOJIXABG.png)

## grep – Print Lines Matching A Pattern

![image](Images/image-8OLLAO0U.png)

In Linux, the "grep" command is used to search for lines in a file or input data that match a specified pattern or regular expression.

The basic syntax of the "grep" command is as follows:

![image](Images/image-1K3OR94T.png)

For example, to search for all lines in a file called "input.txt" that contain the word "Linux", you would use the following command:

![image](Images/image-V23R49KL.png)

This would display all lines in the "input.txt" file that contain the word "Linux".

The "grep" command can also be used with several options to modify its behavior. For example, the "-i" option can be used to perform a case-insensitive search, the "-n" option can be used to display the line numbers for matching lines, and the "-v" option can be used to display only lines that do not match the specified pattern.

For example, to search for all lines in a file called "input.txt" that do not contain the word "Linux", you would use the following command:

![image](Images/image-ZQINEJLP.png)

This would display all lines in the "input.txt" file that do not contain the word "Linux".

![image](Images/image-KOJIXABG.png)

## head / tail – Print First / Last Part Of Files

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "head" and "tail" commands are used to display the first or last few lines of a file, respectively.

The basic syntax of the "head" command is as follows:

![image](Images/image-R4095YX1.png)

For example, to display the first 10 lines of a file called "input.txt", you would use the following command:

![image](Images/image-3IQYA5L4.png)

This would display the first 10 lines of the "input.txt" file.

The "head" command can also be used with the "-n" option to specify the number of lines to display. For example, to display the first 5 lines of a file called "input.txt", you would use the following command:

![image](Images/image-X5R125PJ.png)

The basic syntax of the "tail" command is similar to that of the "head" command:

![image](Images/image-4SBWVV37.png)

For example, to display the last 10 lines of a file called "input.txt", you would use the following command:

![image](Images/image-WD6B4OQM.png)

This would display the last 10 lines of the "input.txt" file.

The "tail" command can also be used with the "-n" option to specify the number of lines to display. For example, to display the last 5 lines of a file called "input.txt", you would use the following command:

![image](Images/image-UJNE1FSN.png)![image](Images/image-KOJIXABG.png)

## tee – Read From Stdin And Output To Stdout And Files

![image](Images/image-8OLLAO0U.png)

In Linux, the "tee" command is used to read input data from stdin (standard input) and output it to both stdout (standard output) and one or more files.

The basic syntax of the "tee" command is as follows:

![image](Images/image-YGM13S6H.png)

For example, to display the output of the "ls" command on the terminal screen and also save it to a file called "directory_contents.txt", you would use the following command:

![image](Images/image-0XRLD1U6.png)

This would display the output of the "ls" command on the terminal screen and also save it to the "directory_contents.txt" file.

The "tee" command can also be used with several options to modify its behavior. For example, the "-a" option can be used to append output to existing files instead of overwriting them, and the "-i" option can be used to ignore interrupt signals.

For example, to append the output of the "ls" command to an existing file called "directory_contents.txt", you would use the following command:

![image](Images/image-4VKUS0AT.png)

This would append the output of the "ls" command to the end of the "directory_contents.txt" file, rather than overwriting its contents.

![image](Images/image-KOJIXABG.png)

7 – Seeing The World As The Shell Sees It..

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Pathname Expansion

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, "pathname expansion" refers to the process of automatically expanding special characters and symbols in pathnames to match files or directories in the file system. This can be a powerful tool for working with groups of files or directories that share a common pattern or naming convention.

Some of the most commonly used characters for pathname expansion include:

(asterisk): Matches any string of characters, including an empty string.

? (question mark): Matches any single character.

[] (brackets): Matches any single character in the specified set. For example, [aeiou] would match any vowel.

{} (braces): Generates a list of strings by expanding a comma-separated list of words. For example, {one,two,three} would expand to "one", "two", and "three".

For example, suppose you have a directory containing a set of files named "file1", "file2", "file3", and so on. To list all of these files, you could use the following command:

![image](Images/image-APYAUC5S.png)

This would expand the "file*" pattern to match all files that start with the string "file".

Similarly, suppose you have a directory containing a set of files with names like "image001.jpg", "image002.jpg", and so on. To list all of these files, you could use the following command:

![image](Images/image-WN7XGTW1.png)

This would expand the "image*.jpg" pattern to match all files that start with the string "image" and end with the ".jpg" extension.

![image](Images/image-KOJIXABG.png)

## Pathname Expansion Of Hidden Files

![image](Images/image-8OLLAO0U.png)

In Linux, pathname expansion also applies to hidden files and directories that start with a dot (.), which are not displayed by default when listing the contents of a directory. To match hidden files and directories using pathname expansion, you can use the following syntax:

![image](Images/image-F7SQYPRO.png)

This will match all hidden files and directories in the current directory.

You can also use other pathname expansion characters to match specific hidden files or directories. For example, to match all hidden files and directories that start with the letter "a", you can use the following command:

![image](Images/image-5LUG5HUQ.png)

This will match all hidden files and directories in the current directory that start with the letter "a".

![image](Images/image-KOJIXABG.png)

## Tilde Expansion

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, tilde expansion refers to the process of automatically expanding the tilde (~) character to represent the home directory of the current user. This can be a useful shorthand when working with files and directories in your home directory.

For example, suppose your home directory is "/home/user". To change to your home directory, you could use the following command:

cd ~

This would expand the tilde character to represent your home directory, resulting in the command "cd /home/user".

You can also use tilde expansion in combination with pathname expansion to quickly reference files and directories in your home directory. For example, suppose you have a file called "my_file.txt" in your home directory. To display the contents of this file, you could use the following command:

![image](Images/image-404P86UC.png)

This would expand the tilde character to represent your home directory, resulting in the command "cat /home/user/my_file.txt".

![image](Images/image-KOJIXABG.png)

## Arithmetic Expansion

![image](Images/image-8OLLAO0U.png)

In Linux, arithmetic expansion allows you to perform mathematical operations within a shell command or script. This can be useful for performing calculations or manipulating numerical data.

The basic syntax for arithmetic expansion is as follows:

![image](Images/image-D9GL7JKE.png)

Where "expression" is a mathematical expression that can include variables, constants, operators, and functions.

For example, suppose you have two variables "x" and "y" that contain the values 5 and 7, respectively. You could use arithmetic expansion to add these variables together and store the result in a third variable "z" as follows:

![image](Images/image-F2AROCO0.png)

This would set the value of "z" to 12.

You can also use arithmetic expansion with a variety of operators and functions to perform more complex mathematical operations. For example, the following command calculates the square root of 25:

![image](Images/image-BPB2LXN1.png)

This would output the value "5".

![image](Images/image-KOJIXABG.png)

## Brace Expansion

![image](Images/image-8OLLAO0U.png)

In Linux, brace expansion allows you to generate a series of strings by specifying a pattern using curly braces {}. This can be a useful tool for generating file names, directories, or any other string that follows a consistent pattern.

The basic syntax for brace expansion is as follows:

![image](Images/image-N6TO4V2K.png)

Where "string1" through "stringN" are the strings to be generated, separated by commas.

For example, suppose you want to create a series of directories named "project1", "project2", and "project3". You could use brace expansion to generate the directory names as follows:

![image](Images/image-WVTMSAM7.png)

This would generate the directories "project1", "project2", and "project3".

You can also use brace expansion with more complex patterns, including ranges and nested braces. For example, the following command generates a series of file names with the format "file001", "file002", and so on up to "file100":

![image](Images/image-2O4KOK8E.png)![image](Images/image-KOJIXABG.png)

## Parameter Expansion

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, parameter expansion allows you to manipulate the values of variables in various ways within a shell command or script. This can be useful for working with text strings, file paths, and other types of data.

The basic syntax for parameter expansion is as follows:

![image](Images/image-7CFTF7O7.png)

Where "parameter" is the name of the variable to be expanded.

For example, suppose you have a variable "filename" that contains the value "/home/user/documents/myfile.txt". You can use parameter expansion to extract the directory path from this variable as follows:

![image](Images/image-FBY9THNE.png)

This would output the directory path "/home/user/documents".

You can also use parameter expansion to perform other types of text manipulation, such as replacing substrings or performing case conversion. For example, the following command replaces all occurrences of the string "old" with "new" in the variable "text":

![image](Images/image-O1RGUGTP.png)

By mastering the use of parameter expansion, you can become a more efficient and effective Linux user, able to quickly and easily manipulate variables and text data using the command line.

![image](Images/image-KOJIXABG.png)

## Command Substitution

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, command substitution allows you to execute a command within a shell command or script and use the output of that command as part of the original command. This can be useful for performing complex operations or manipulating data from other commands.

The basic syntax for command substitution is as follows:

![image](Images/image-8INBV3IQ.png)

Where "command" is the command to be executed.

For example, suppose you want to create a directory with a name based on the current date and time. You can use command substitution with the "date" command to generate the name as follows:

![image](Images/image-GQL9NPUF.png)

This would create a directory with a name based on the current date and time in the format "YYYY-MM-DD_HH-MM-SS".

You can also use command substitution to perform other types of text manipulation or data processing. For example, the following command counts the number of files in the current directory:

![image](Images/image-IRIOOY6I.png)

This would output a message indicating the number of files in the directory.

![image](Images/image-KOJIXABG.png)

## Quoting

![image](Images/image-8OLLAO0U.png)

In Linux, quoting refers to the process of enclosing a text string within special characters to indicate how the string should be interpreted by the shell. There are three types of quoting in Linux: single quotes, double quotes, and backslashes.

Single quotes are used to indicate that the enclosed string should be treated as a literal string, with no variable substitution or command execution. For example, the following command will print the string "$HOME" literally:

![image](Images/image-XSO7OXWX.png)

Double quotes are used to indicate that variable substitution and command substitution should be performed within the enclosed string. For example, the following command will print the value of the "HOME" environment variable:

![image](Images/image-VC62EOWL.png)

Backslashes are used to escape special characters within a string. For example, the following command will print the string "I said, 'Hello!'" with the single quotes included:

![image](Images/image-72KLL7NK.png)![image](Images/image-KOJIXABG.png)

## Double Quotes

![image](Images/image-8OLLAO0U.png)

In Linux, double quotes are a type of quoting that allow you to include variables and command substitution within a text string. When a text string is enclosed in double quotes, any variable names or command substitutions within the string are expanded by the shell before the string is executed.

For example, suppose you have a variable "name" that contains the value "John". You can use double quotes to include this variable within a text string as follows:

![image](Images/image-NRJZS3AT.png)

This would output the string "Hello, John!".

Double quotes also allow you to use certain escape sequences within a text string, such as "\n" for a new line or "\t" for a tab character. For example, the following command would print a message with a new line character:

![image](Images/image-05XIQ9RS.png)

This would output the message "Hello," on one line and "World!" on the next line.

![image](Images/image-KOJIXABG.png)

## Single Quotes

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, single quotes are a type of quoting that treat the enclosed text string as a literal string. When a text string is enclosed in single quotes, the shell does not perform any variable substitution or command execution within the string.

For example, suppose you have a variable "name" that contains the value "John". If you enclose the variable within single quotes as follows:

![image](Images/image-5BQJLZBQ.png)

This would output the string "Hello, $name!", with the variable name printed literally rather than being expanded.

Single quotes are useful when you want to include special characters within a text string, such as spaces, tabs, or other characters that may be interpreted by the shell. When a text string is enclosed in single quotes, any special characters within the string are treated as literal characters rather than being interpreted by the shell.

![image](Images/image-KOJIXABG.png)

## Escaping Characters

![image](Images/image-8OLLAO0U.png)

In Linux, escaping characters refers to the process of using the backslash character () to indicate that a special character should be treated as a literal character within a text string. The backslash character tells the shell to treat the character that follows it as a literal character, rather than interpreting it as a special character.

For example, suppose you want to include a single quote within a text string that is enclosed in single quotes. You can use the backslash character to escape the single quote as follows:

![image](Images/image-1TJV6JCW.png)

This would output the string "I said 'Hello!'", with the single quotes included.

Similarly, you can use the backslash character to escape other special characters within a text string, such as double quotes, backslashes, or newline characters. For example, the following command would print a message with a newline character:

![image](Images/image-3TDRUTSO.png)

This would output the message "Hello," on one line and "World!" on the next line.

![image](Images/image-KOJIXABG.png)

## Backslash Escape Sequences

![image](Images/image-8OLLAO0U.png)

In Linux, backslash escape sequences are special sequences of characters that begin with a backslash () and are used to represent special characters or control codes within a text string. Backslash escape sequences are commonly used to represent characters that cannot be typed directly, such as newline characters, tabs, or other control codes.

Some commonly used backslash escape sequences in Linux include:

\n - represents a newline character

\t - represents a tab character

\r - represents a carriage return character

' - represents a literal single quote character

" - represents a literal double quote character

For example, the following command would print a message with a newline character:

![image](Images/image-P95DHMMS.png)

This would output the message "Hello," on one line and "World!" on the next line.

![image](Images/image-KOJIXABG.png)

8 – Advanced Keyboard Tricks.

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Command Line Editing

![image](Images/image-8OLLAO0U.png)

Command line editing is a powerful feature in Linux that allows you to quickly edit and modify commands as you type them on the command line. By using keyboard shortcuts and other techniques, you can move the cursor, delete text, and perform other editing tasks without having to use the arrow keys or the backspace key.

Some commonly used keyboard shortcuts for command line editing in Linux include:

Ctrl+A - Move the cursor to the beginning of the line.

Ctrl+E - Move the cursor to the end of the line.

Ctrl+U - Delete all text from the cursor to the beginning of the line.

Ctrl+K - Delete all text from the cursor to the end of the line.

Ctrl+W - Delete the word immediately before the cursor.

Ctrl+Y - Paste the last text that was deleted using Ctrl+U or Ctrl+K.

By using these and other keyboard shortcuts for command line editing, you can save time and streamline your workflow on the command line. Additionally, many Linux distributions allow you to customize these shortcuts to better suit your preferences and workflow.

![image](Images/image-KOJIXABG.png)

## Cursor Movement

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

Cursor movement is an essential feature in Linux that allows you to move the cursor around the command line, selecting, copying, or editing text as you go. By using keyboard shortcuts and other techniques, you can navigate your way through the command line quickly and easily.

Ctrl+B - Move the cursor back one character.

Ctrl+F - Move the cursor forward one character.

Alt+B - Move the cursor back one word.

Alt+F - Move the cursor forward one word.

Additionally, many Linux distributions support a "vi mode" of cursor movement, allowing you to use vi-style commands to move around the command line. This can be a powerful way to navigate and edit text on the command line, particularly if you are already familiar with vi or other text editors.

![image](Images/image-KOJIXABG.png)

## Completion

![image](Images/image-8OLLAO0U.png)

Completion is a powerful feature in Linux that allows you to quickly and easily complete command and file names, reducing typing and avoiding errors. By using keyboard shortcuts and other techniques, you can complete partial command or file names, making it easier to navigate the file system and execute commands.

Some commonly used keyboard shortcuts for completion in Linux include:

Tab - Complete the current word or display possible completions.

Ctrl+X Ctrl+F - Complete a filename.

Ctrl+X Ctrl+@ - Display possible completions.

Alt+/ - Attempt to complete the current word using a file in the current directory.

Additionally, many Linux distributions support customizable completion, allowing you to define your own completion functions or customize the behavior of existing completion functions. By mastering the use of completion in Linux, you can become a more efficient and effective Linux user, able to navigate and execute commands on the command line quickly and easily.

![image](Images/image-KOJIXABG.png)

## Using History

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

Using command history is a powerful feature in Linux that allows you to quickly recall and modify previous commands, reducing typing and avoiding errors. By using keyboard shortcuts and other techniques, you can view your command history, search for specific commands, and recall or modify previous commands.

Some commonly used keyboard shortcuts for using command history in Linux include:

Up arrow - Recall the previous command in the history.

Down arrow - Recall the next command in the history.

Ctrl+R - Search for a previous command based on a partial match.

!! - Execute the previous command in the history.

!-n - Execute the command n commands back in the history.

!string - Execute the most recent command starting with the specified string.

![image](Images/image-KOJIXABG.png)

## Searching History

![image](Images/image-8OLLAO0U.png)

Searching history is a powerful feature in Linux that allows you to quickly find and execute previous commands based on a search term. By using keyboard shortcuts and other techniques, you can search your command history for specific commands, allowing you to quickly recall and execute commands without having to type them again.

Some commonly used keyboard shortcuts for searching history in Linux include:

Ctrl+R - Search for a previous command based on a partial match.

Ctrl+S - Forward search for a previous command based on a partial match.

Ctrl+G - Cancel the current search.

Up arrow - Recall the previous command in the history.

Down arrow - Recall the next command in the history.

![image](Images/image-KOJIXABG.png)

## History Expansion

![image](Images/image-8OLLAO0U.png)

History expansion is an advanced feature in Linux that allows you to use history commands and operators to modify and execute previous commands. By using history expansion, you can save time and avoid errors by reusing and modifying previously executed commands.

Some commonly used history expansion operators in Linux include:

!! - Execute the previous command in the history.

!-n - Execute the command n commands back in the history.

!string - Execute the most recent command starting with the specified string.

!?string - Execute the most recent command containing the specified string.

!:n - Use the nth word of the previous command.

!:n-m - Use the range of words n to m from the previous command.

![image](Images/image-KOJIXABG.png)

## script

![image](Images/image-8OLLAO0U.png)

The "script" command in Linux is a powerful tool that allows you to record all input and output to a shell session into a file. By using the "script" command, you can create a log of everything that was typed into the shell session and everything that was output to the screen, including error messages, command outputs, and other information.

To start a script session, simply type "script" at the command prompt, followed by the name of the file you want to record the session to. For example:

![image](Images/image-W0PTPCU6.png)

Once you start a script session, all input and output to the shell will be recorded to the specified file. To stop the session, simply type "exit" at the command prompt. For example:

![image](Images/image-M3CIKG5U.png)

The resulting file will contain a complete log of everything that was typed into the shell session and everything that was output to the screen. By using the "script" command, you can create detailed records of your shell sessions, making it easier to troubleshoot issues or reproduce specific scenarios.

![image](Images/image-KOJIXABG.png)

## 9 – Permissions

![image](Images/image-8OLLAO0U.png)

file permissions determine who can access and modify files and directories on the system. Each file and directory has a set of permissions that are represented by three types of access: read, write, and execute. There are three levels of access: owner, group, and other. The owner is the user who owns the file or directory, the group is a set of users who share access to the file or directory, and other refers to all users who are not the owner or a member of the group.

To view the permissions of a file or directory in Linux, you can use the "ls -l" command, which displays the permissions in a long format. For example:

![image](Images/image-6CO3GUK8.png)

In this example, the first character ("-") indicates that this is a file, and the following nine characters represent the permissions. The first three characters ("rw-") indicate that the owner has read and write access, the next three characters ("r—") indicate that the group has read access only, and the final three characters ("r—") indicate that other users also have read access only.

To modify the permissions of a file or directory in Linux, you can use the "chmod" command. The "chmod" command allows you to add or remove permissions for the owner, group, or other users. For example, to add execute permission for the owner of a file, you can use the following command:

![image](Images/image-WTMTH2OV.png)

In this example, "u" represents the owner of the file, and "+x" adds execute permission.

![image](Images/image-KOJIXABG.png)

## Owners and Group Members

![image](Images/image-8OLLAO0U.png)

In Linux, each file and directory has an owner and a group. The owner is the user who owns the file or directory, and the group is a set of users who share access to the file or directory.

To view the owner and group of a file or directory in Linux, you can use the "ls -l" command. The output will display the owner and group of the file or directory in the third and fourth columns. For example:

![image](Images/image-R2CHLXCZ.png)

In this example, "user" is the owner of the file, and "group" is the group that the file belongs to.

To change the owner or group of a file or directory in Linux, you can use the "chown" and "chgrp" commands, respectively. For example, to change the owner of a file to "newuser", you can use the following command:

![image](Images/image-QVSKK7OF.png)

In this example, "newuser" is the new owner of the file.

To change the group of a file to "newgroup", you can use the following command:

![image](Images/image-7XZIL83F.png)

In this example, "newgroup" is the new group that the file belongs to.

![image](Images/image-KOJIXABG.png)

## Reading, Writing, And Executing

![image](Images/image-8OLLAO0U.png)

In Linux, file permissions control who can read, write, and execute files and directories on the system. Each file and directory has a set of permissions that are represented by three types of access: read, write, and execute.

The read permission allows users to view the contents of a file or directory. The write permission allows users to modify the contents of a file or directory. The execute permission allows users to run programs or scripts.

There are three levels of access: owner, group, and other. The owner is the user who owns the file or directory, the group is a set of users who share access to the file or directory, and other refers to all users who are not the owner or a member of the group.

To modify file permissions in Linux, you can use the "chmod" command. The "chmod" command allows you to add or remove permissions for the owner, group, or other users. For example, to add write permission for the owner of a file, you can use the following command:

![image](Images/image-QWX5GGRT.png)

In this example, "u" represents the owner of the file, and "+w" adds write permission.

To remove execute permission for other users of a directory, you can use the following command:

![image](Images/image-LK6FOIJG.png)

In this example, "o" represents other users, and "-x" removes execute permission.

![image](Images/image-KOJIXABG.png)

## chmod – Change File Mode

![image](Images/image-8OLLAO0U.png)

In Linux, the "chmod" command is used to change the file mode or permissions of a file or directory. The file mode or permissions specify who can read, write, and execute the file or directory. There are two ways to specify the file mode: symbolic mode and absolute mode.

Symbolic mode uses symbols to represent the file mode. The symbols used are "u" for user, "g" for group, "o" for others, "a" for all, "+" for add permission, "-" for remove permission, and "=" for set permission. For example, to add write permission for the owner of a file, you can use the following command:

![image](Images/image-GWI97ZLZ.png)

In this example, "u" represents the owner of the file, and "+w" adds write permission.

To remove execute permission for other users of a directory, you can use the following command:

![image](Images/image-LOY1SJ87.png)

In this example, "o" represents other users, and "-x" removes execute permission.

Absolute mode uses numbers to represent the file mode. Each permission is assigned a number: read is 4, write is 2, and execute is 1\. The numbers are added together to create the file mode. For example, to give the owner read, write, and execute permissions and the group and other users only read and execute permissions, you can use the following command:

![image](Images/image-G9A3FO7Z.png)

In this example, the first digit "7" represents the owner's permissions, which are read, write, and execute (4+2+1=7), the second digit "5" represents the group's permissions, which are read and execute (4+1=5), and the third digit "5" represents other users' permissions, which are also read and execute (4+1=5).

![image](Images/image-KOJIXABG.png)

## Setting File Mode With The GUI

![image](Images/image-8OLLAO0U.png)

In Linux, file mode or permissions can also be set using the graphical user interface (GUI) of your file manager.

To set file mode using the GUI:

Open your file manager and navigate to the file or directory whose mode you want to modify.

Right-click the file or directory and select "Properties" or "Permissions" from the menu.

In the "Properties" or "Permissions" window, you can see the current file mode or permissions.

To modify the file mode, select the checkboxes next to the permissions you want to allow or remove.

Click "Apply" or "OK" to save the changes.

You can also modify the file mode by changing the permissions for the owner, group, and other users. To do this, click the drop-down menu next to each user type and select the permissions you want to allow or remove.

Keep in mind that the GUI file manager may not have all the options available with the "chmod" command, and some file managers may have different options or menus. If you need more advanced permissions, it is recommended to use the "chmod" command from the command line.

![image](Images/image-KOJIXABG.png)

## umask – Set Default Permissions

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, the "umask" command is used to set the default file mode or permissions for new files and directories created by a user. The default file mode is the permissions that are automatically set when a new file or directory is created.

The "umask" command works by subtracting the file mode from a default value of 777 (for directories) or 666 (for files). For example, if the umask is set to 022, the file mode for new files will be 644 (666 - 022 = 644) and the file mode for new directories will be 755 (777 - 022 = 755).

To set the umask, you can use the following command:

![image](Images/image-ONNS0DNU.png)

In this example, the umask is set to 022, which means that the write permission is removed for group and other users.

The umask can be set in the shell startup file (such as .bashrc or .bash_profile) to make it persistent across sessions. It can also be set in the system-wide configuration file (/etc/profile or /etc/bashrc) to apply the default file mode for all users.

![image](Images/image-KOJIXABG.png)

## Changing Identities

![image](Images/image-8OLLAO0U.png)

In Linux, you can change the identity of a process or command using the "su" and "sudo" commands. Changing identity can be useful when you need to run a command as a different user or with elevated privileges.

The "su" command is used to switch to another user's account. By default, the command will switch to the root user's account. To switch to another user's account, you can use the following command:

![image](Images/image-5W3TDSJN.png)

In this example, "username" is the name of the user account you want to switch to. You will be prompted to enter the password for the user account. After entering the correct password, you will switch to the user's account and the command prompt will change to reflect the new identity.

The "sudo" command is used to run a command with elevated privileges. By default, the command will run with root privileges. To run a command with elevated privileges as another user, you can use the following command:

![image](Images/image-FC6NS0GD.png)

In this example, "username" is the name of the user account you want to run the command as, and "command" is the command you want to run. You will be prompted to enter your password. After entering the correct password, the command will run with the specified user's identity.

Changing identity can be useful for performing administrative tasks or running commands that require elevated privileges. However, it is important to use caution when switching to another user's account or running commands with elevated privileges, as it can potentially compromise the security of the system.

![image](Images/image-KOJIXABG.png)

## su – Run A Shell With Substitute User And Group IDs

![image](Images/image-8OLLAO0U.png)

In Linux, the "su" command is used to switch to another user's account or to run a shell with substitute user and group IDs. The command is commonly used to run commands as the root user or to switch to another user's account for administrative tasks.

To use the "su" command, open a terminal window and type:

$ su

This will switch you to the root user's account, prompting you to enter the root user's password. After entering the password, you will be logged in as the root user and the command prompt will change to reflect the new identity.

To switch to another user's account, you can use the following command:

![image](Images/image-5W3TDSJN.png)

In this example, "username" is the name of the user account you want to switch to. You will be prompted to enter the password for the user account. After entering the correct password, you will switch to the user's account and the command prompt will change to reflect the new identity.

You can also use the "su" command to run a shell with substitute user and group IDs. This can be useful for running a shell with a different set of permissions or running a command with elevated privileges. To run a shell with substitute user and group IDs, use the following command:

![image](Images/image-XXSDFJTQ.png)

In this example, "command" is the command you want to run with substitute user and group IDs. You will be prompted to enter the password for the current user's account. After entering the correct password, the command will run with substitute user and group IDs.

![image](Images/image-KOJIXABG.png)

## sudo – Execute A Command As Another User

![image](Images/image-8OLLAO0U.png)

In Linux, the "sudo" command is used to execute a command as another user, typically the root user. The command is commonly used to perform administrative tasks that require elevated privileges.

To use the "sudo" command, open a terminal window and type:

![image](Images/image-2HVGUIJ5.png)

In this example, "command" is the command you want to run with elevated privileges. You will be prompted to enter your password. After entering the correct password, the command will run with elevated privileges.

By default, the "sudo" command will run the command as the root user. However, you can specify a different user by using the "-u" option, as shown below:

![image](Images/image-Z1V0CY59.png)

In this example, "username" is the name of the user you want to run the command as.

The "sudo" command can also be used to run a shell with elevated privileges, as shown below:

![image](Images/image-3371N3V8.png)

This will open a shell with elevated privileges. You will be prompted to enter your password. After entering the correct password, you will be logged in as the root user.

The "sudo" command is a powerful tool that can be used for performing administrative tasks or running commands with elevated privileges. However, it should be used with caution, as it can potentially compromise the security of the system. It is important to only use the "sudo" command when necessary and to ensure that you understand the implications of the commands you are running.

![image](Images/image-KOJIXABG.png)

## Ubuntu And sudo

![image](Images/image-8OLLAO0U.png)

In Ubuntu, the "sudo" command is used extensively to perform administrative tasks that require elevated privileges. The use of "sudo" is recommended over using the root account directly, as it provides better security and auditing.

When you install Ubuntu, the first user account that is created is given sudo privileges by default. This means that the user can execute commands with elevated privileges by prefixing the command with "sudo".

To use the "sudo" command in Ubuntu, open a terminal window and type:

![image](Images/image-EJJQYE5U.png)

In this example, "command" is the command you want to run with elevated privileges. You will be prompted to enter your password. After entering the correct password, the command will run with elevated privileges.

By default, the "sudo" command will prompt you for your password every 15 minutes. However, you can change this behavior by modifying the "/etc/sudoers" file using the "visudo" command.

The "sudo" command can also be used to run a shell with elevated privileges, as shown below:

![image](Images/image-94UWN8WP.png)

This will open a shell with elevated privileges. You will be prompted to enter your password. After entering the correct password, you will be logged in as the root user.

![image](Images/image-KOJIXABG.png)

## chown – Change File Owner And Group

![image](Images/image-8OLLAO0U.png)

In Linux, the "chown" command is used to change the owner and group of a file or directory. This command is typically used when you need to transfer ownership of a file or directory to a different user or group.

To use the "chown" command, open a terminal window and type:

![image](Images/image-1OBIQHDE.png)

In this example, "owner" is the name of the user you want to set as the owner of the file, "group" is the name of the group you want to set as the group owner of the file, and "file" is the name of the file you want to change the ownership of. You need to prefix the command with "sudo" to run the command with elevated privileges.

To change the owner of a directory and all its contents recursively, you can use the "-R" option, as shown below:

![image](Images/image-MJYSH1HK.png)

In this example, "directory" is the name of the directory you want to change the ownership of.

The "chown" command is a powerful tool that can be used for transferring ownership of files and directories. However, it should be used with caution, as it can potentially compromise the security of the system. It is important to only use the "chown" command when necessary and to ensure that you understand the implications of the ownership changes you are making.

![image](Images/image-KOJIXABG.png)

## chgrp – Change Group Ownership

![image](Images/image-8OLLAO0U.png)

In Linux, the "chgrp" command is used to change the group ownership of a file or directory. This command is typically used when you need to transfer group ownership of a file or directory to a different group.

To use the "chgrp" command, open a terminal window and type:

![image](Images/image-KSNU8RN1.png)

In this example, "group" is the name of the group you want to set as the group owner of the file, and "file" is the name of the file you want to change the group ownership of. You need to prefix the command with "sudo" to run the command with elevated privileges.

To change the group ownership of a directory and all its contents recursively, you can use the "-R" option, as shown below:

![image](Images/image-ZCWWQHBQ.png)

In this example, "directory" is the name of the directory you want to change the group ownership of.

![image](Images/image-KOJIXABG.png)

## Exercising Our Privileges

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, certain operations require elevated privileges to execute, such as installing software, modifying system settings, and accessing certain directories. These privileges are typically reserved for the root user or users with administrative privileges.

To exercise these privileges, you can use the "sudo" command. The "sudo" command allows you to temporarily escalate your privileges to perform specific actions that require elevated permissions.

For example, to install a software package using the "apt-get" package manager, you need to run the command with elevated privileges. To do this, you can use the "sudo" command, as shown below:

![image](Images/image-F3CVWFHH.png)

In this example, "package-name" is the name of the package you want to install.

Similarly, to modify system settings, you need to run the command with elevated privileges. For example, to change the system timezone, you can use the "timedatectl" command with the "sudo" prefix, as shown below:

![image](Images/image-XV4CWHSU.png)

In this example, "timezone-name" is the name of the timezone you want to set.

To access certain directories, you may also need elevated privileges. For example, to access the system logs, you need to be a member of the "adm" group or have sudo privileges.

![image](Images/image-KOJIXABG.png)

## 10 – Processes.

![image](Images/image-8OLLAO0U.png)

In Linux, a process is a running instance of a program. When you start a program, the operating system creates a new process to run that program. The process has a unique process ID (PID), which is used to identify and manage the process.

A process is made up of one or more threads, which are individual paths of execution within the process. Each thread is associated with a stack, which is a region of memory used for storing local variables and function calls.

When a process is started, it is loaded into memory and given access to system resources, such as memory, input/output devices, and the CPU. The process can then execute its instructions and interact with the system.

Processes can communicate with each other using various interprocess communication (IPC) mechanisms, such as pipes, sockets, and shared memory. This allows different processes to exchange data and work together to perform complex tasks.

Processes can also be managed and controlled using various commands and tools. For example, you can use the "ps" command to list all the processes running on the system, the "kill" command to terminate a process, and the "nice" command to change the priority of a process.

![image](Images/image-KOJIXABG.png)

## Viewing Processes

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, you can use several commands to view the processes running on the system, such as:

ps - This command shows a snapshot of the processes running on the system at the time you run the command. It can be used to display a variety of information about each process, including the process ID (PID), the parent process ID (PPID), the user running the process, the CPU and memory usage, and the command that launched the process. The "ps" command can be customized using various options to display only specific information.

![image](Images/image-CJJTTG07.png)![image](Images/image-SQ5BQB08.png)

top/htop - These commands provide a real-time view of the system's processes, sorted by CPU or memory usage. They can be used to monitor the system's performance and identify processes that are consuming excessive resources.

![image](Images/image-G3MK1XC5.png)

or

![image](Images/image-LBIDQKL8.png)

pstree - This command shows a tree of processes, with each process's parent displayed above it. This can be useful for understanding how processes are related to each other.

![image](Images/image-ASKCAYNK.png)

pgrep - This command can be used to find the process IDs of processes that match a specific name or pattern. It is useful when you want to identify the process ID of a running process without using the "ps" command.

![image](Images/image-CJJTTG07.png)![image](Images/image-37XXQ8T5.png)

In this example, "process-name" is the name of the process you want to find the PID for.

![image](Images/image-KOJIXABG.png)

## Viewing Processes Dynamically With top

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

"top" is a powerful command in Linux that allows you to view the system's processes dynamically in real-time. It displays a list of processes sorted by their CPU usage, and it updates this list continuously. Here are some steps to use "top" command:

Open a terminal window.

Type "top" and press Enter.

You will see a list of processes displayed, sorted by CPU usage. The top process is the one using the most CPU.

You can press "q" at any time to quit "top."

You can use various options to customize the output of "top." For example, you can use the "-d" option to specify the update interval in seconds, the "-u" option to show only processes owned by a specific user, and the "-p" option to show only specific process IDs.

You can also use various keyboard shortcuts to interact with "top." For example, you can press "k" to send a signal to a process, "r" to change the priority of a process, and "h" to display the help screen.

You can press "h" at any time to display the list of available keyboard shortcuts.

In summary, "top" is a powerful command for viewing processes in real-time on a Linux system. It can be used to monitor the system's performance, identify resource-hungry processes, and troubleshoot issues on your system. Understanding how to use "top" effectively can help you become a more efficient system administrator.

![image](Images/image-KOJIXABG.png)

## Controlling Processes

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, you can control processes in various ways using commands and tools. Here are some common ways to control processes:

kill - This command is used to terminate a process. You can specify the process ID (PID) of the process you want to kill or use a signal to terminate the process. For example, to terminate a process with a specific PID, you can use the following command:

![image](Images/image-Q26X7LEX.png)

pkill - This command is similar to "kill," but it allows you to specify the process name or pattern instead of the PID. It can be useful when you want to terminate multiple processes at once. For example, to terminate all processes with a specific name, you can use the following command:

![image](Images/image-RSIS8XLW.png)

killall - This command is similar to "pkill," but it terminates all processes with a specific name, rather than just one. For example, to terminate all processes with the name "process-name," you can use the following command:

![image](Images/image-JOSGACDQ.png)

renice - This command is used to change the priority of a process. You can use it to increase or decrease a process's priority, which determines how much CPU time it is allocated. For example, to increase the priority of a process with a specific PID, you can use the following command:

![image](Images/image-DTD9PW9H.png)

fg/bg - These commands are used to move a process to the foreground or background. When a process is in the foreground, it receives input from the keyboard, and when it is in the background, it does not. For example, to move a process with a specific PID to the background, you can use the following command:

![image](Images/image-1C4DSV4L.png)

jobs - This command is used to display a list of the processes running in the background. You can use it to identify the process ID of a process that is running in the background. For example, to display a list of all background processes, you can use the following command:

![image](Images/image-8WRSECM0.png)

In summary, controlling processes is an important aspect of system administration and troubleshooting in Linux. Understanding how to use commands like "kill," "pkill," "killall," "renice," "fg/bg," and "jobs" can help you manage and control the processes running on your system.

![image](Images/image-KOJIXABG.png)

## Interrupting A Process

![image](Images/image-8OLLAO0U.png)

In Linux, you can interrupt a process that is currently running using the keyboard interrupt signal "Ctrl + C." This signal sends an interrupt signal to the process, which causes it to terminate gracefully.

For example, if you are running a command that is taking too long to complete, you can interrupt it using "Ctrl + C" to stop it. This can be useful in situations where a command is stuck or unresponsive and needs to be terminated immediately.

It's important to note that not all processes can be interrupted using "Ctrl + C." Some processes, such as system services, may not respond to this signal and require other methods to stop them. In such cases, you can use other tools like "kill" or "pkill" to terminate the process.

![image](Images/image-KOJIXABG.png)

## Putting A Process In The Background

![image](Images/image-8OLLAO0U.png)

In Linux, you can put a process in the background using the "bg" command. When you run a command or start a process, it runs in the foreground, and you can interact with it using the terminal. However, if you want to run another command or process simultaneously, you can move the current process to the background, so it continues to run, but doesn't require your attention.

To put a process in the background, you first need to suspend it using the "Ctrl + Z" keyboard shortcut. This will stop the process and return you to the shell prompt. Then, you can use the "bg" command to move the process to the background, as follows:

![image](Images/image-0JZADRWE.png)

This will start the suspended command in the background, and you will see a message showing the job ID and process ID of the background job.

You can also use the "&" operator when running a command to start it in the background directly, without having to suspend it first. For example:

![image](Images/image-3834LLIB.png)

This will start the command in the background immediately, and you can continue to use the terminal for other tasks.

![image](Images/image-KOJIXABG.png)

## Returning A Process To The Foreground

![image](Images/image-8OLLAO0U.png)

In Linux, you can bring a process that is running in the background back to the foreground using the "fg" command. This command brings the most recent background process to the foreground, where you can interact with it directly.

To bring a background process to the foreground, you can use the "fg" command, followed by the job ID or process ID of the process you want to bring to the foreground. For example, if you have a process running in the background with job ID 1, you can bring it to the foreground as follows:

![image](Images/image-4N6ROID9.png)

Alternatively, you can use the process ID of the background process as follows:

![image](Images/image-DDAXKCTQ.png)

This will bring the background process to the foreground, and you can interact with it directly using the terminal. If the process is currently paused, you can resume it using the "bg" command or "fg" command with the "-s" option, as follows:

![image](Images/image-9LDIGL2L.png)

or

![image](Images/image-9YST7LWF.png)![image](Images/image-KOJIXABG.png)

## Stopping (Pausing) A Process

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In Linux, you can stop a running process temporarily using the "Ctrl + Z" keyboard shortcut. This sends a signal to the process, which suspends it and returns you to the shell prompt. The process remains in the memory, but its execution is paused until you resume it.

To stop a process, you can press "Ctrl + Z" while the process is running in the foreground. This will suspend the process and display a message showing the job ID and process ID of the suspended process. The process is not terminated, but its execution is paused, and it will remain in the memory until you resume it or terminate it.

You can resume a suspended process using the "fg" or "bg" commands. The "fg" command brings the most recent suspended process to the foreground, while the "bg" command starts the most recent suspended process in the background.

To resume a suspended process in the foreground, use the "fg" command, followed by the job ID or process ID of the suspended process, as follows:

![image](Images/image-BX1WP9EW.png)

or

![image](Images/image-97WQNX41.png)

To start a suspended process in the background, use the "bg" command, followed by the job ID or process ID of the suspended process, as follows:

![image](Images/image-22LRV69R.png)

or

![image](Images/image-L6ZQ450I.png)![image](Images/image-KOJIXABG.png)

## Signals

![image](Images/image-8OLLAO0U.png)

In Linux, signals are a way for the operating system to communicate with running processes. Signals are software interrupts that are sent to a process to indicate events or actions that have occurred. A signal can be used to request that a process terminate, pause, or perform some other action.

There are many different types of signals that can be sent to a process, but some of the most commonly used signals include:

SIGTERM: This signal is used to request that a process terminate gracefully. When a process receives a SIGTERM signal, it should clean up any resources it is using and then terminate.

SIGKILL: This signal is used to force a process to terminate immediately, without giving it a chance to clean up resources. When a process receives a SIGKILL signal, it is terminated immediately, and any resources it was using are released.

SIGSTOP: This signal is used to pause a process temporarily. When a process receives a SIGSTOP signal, it is suspended, and its execution is paused. The process can be resumed later using the "fg" or "bg" commands.

SIGCONT: This signal is used to resume a process that has been paused using SIGSTOP. When a process receives a SIGCONT signal, its execution is resumed from where it left off.

SIGINT: This signal is used to interrupt a process that is running in the foreground. When a process receives a SIGINT signal, it should terminate gracefully.

To send a signal to a process, you can use the "kill" command, followed by the signal name or number and the process ID of the process you want to send the signal to. For example, to send a SIGTERM signal to process ID 1234, you can use the following command:

![image](Images/image-0X7FZ84W.png)![image](Images/image-KOJIXABG.png)

## Sending Signals To Processes With kill

![image](Images/image-8OLLAO0U.png)

In Linux, you can use the "kill" command to send signals to running processes. The "kill" command sends a signal to the process with the specified process ID (PID), asking it to perform a certain action or respond to a particular event.

The basic syntax of the "kill" command is as follows:

![image](Images/image-LJPNTTKH.png)

Where [signal] is the name or number of the signal you want to send, and [PID] is the process ID of the process you want to send the signal to.

For example, to send a SIGTERM signal to process ID 1234, you can use the following command:

![image](Images/image-JD9R7X9V.png)

Here are some common signals that you can use with the "kill" command:

SIGTERM: This signal is used to request that a process terminate gracefully. When a process receives a SIGTERM signal, it should clean up any resources it is using and then terminate.

SIGKILL: This signal is used to force a process to terminate immediately, without giving it a chance to clean up resources. When a process receives a SIGKILL signal, it is terminated immediately, and any resources it was using are released.

SIGSTOP: This signal is used to pause a process temporarily. When a process receives a SIGSTOP signal, it is suspended, and its execution is paused. The process can be resumed later using the "fg" or "bg" commands.

SIGCONT: This signal is used to resume a process that has been paused using SIGSTOP. When a process receives a SIGCONT signal, its execution is resumed from where it left off.

You can also send signals using their numerical values instead of their names. For example, to send a SIGKILL signal to process ID 1234, you can use the following command:

![image](Images/image-4GRTOAM4.png)![image](Images/image-KOJIXABG.png)

## Sending Signals To Multiple Processes With killall

![image](Images/image-8OLLAO0U.png)

The killall command is similar to the kill command, but instead of sending signals to a specific process ID (PID), it sends signals to all processes that match a given name. This can be useful when you want to send a signal to multiple processes at once.

The basic syntax of the killall command is as follows:

![image](Images/image-RA4Q7EI7.png)

Where [signal] is the name or number of the signal you want to send, and [process_name] is the name of the process or processes you want to target.

For example, to send a SIGTERM signal to all processes named myprocess, you can use the following command:

![image](Images/image-HIBGYPR8.png)

Here are some common signals that you can use with the killall command:

![image](Images/image-RNWUNTQC.png)

This signal is used to request that a process terminate gracefully.

![image](Images/image-Z5WRM6I2.png)

This signal is used to force a process to terminate immediately.

![image](Images/image-DO5OMW6P.png)

This signal is used to request that a process reload its configuration.

It's important to use the killall command with caution, as it can easily kill unintended processes. You should always double-check the process names and signal types before using this command.

![image](Images/image-KOJIXABG.png)

## More Process Related Commands

![image](Images/image-8OLLAO0U.png)

In addition to the kill and killall commands, there are several other useful commands for managing processes in Linux:

ps: This command is used to display information about currently running processes. By default, ps shows information about processes running in the current shell session. You can use various options to filter and display different types of information.

top: This command provides a real-time view of system processes and their resource usage. top is interactive, allowing you to sort and filter processes based on various criteria, and to send signals to individual processes.

nice: This command is used to adjust the scheduling priority of a process. By default, processes run with a priority of 0, but you can use nice to lower or raise the priority of a process, which can affect how much CPU time it receives.

renice: This command is used to change the priority of a process that is already running. You can use renice to adjust the priority of a process that is using too much CPU time, or to give higher priority to a process that requires more resources.

bg and fg: These commands are used to move processes between the foreground and background. When a process is in the foreground, it receives input from the user and displays output to the screen. When a process is in the background, it continues to run, but does not interact with the user. You can use bg to move a process to the background, and fg to move it back to the foreground.

jobs: This command is used to display a list of jobs running in the background. Each job is assigned a job number, which can be used with the bg and fg commands to move the job between the foreground and background.

![image](Images/image-KOJIXABG.png)

## 11 – The Environment

![image](Images/image-8OLLAO0U.png)

The environment in Linux refers to a collection of system variables, settings, and preferences that are available to all processes and users on the system. These variables can be used to configure the behavior of various system tools and applications, and to customize the user's working environment.

![image](Images/image-KOJIXABG.png)

## What Is Stored In The Environment?

![image](Images/image-8OLLAO0U.png)

The Linux environment is a collection of variables and settings that are available to all processes and users on the system. Some of the most commonly used environment variables in Linux include:

PATH: This variable specifies a list of directories where the system should search for executable files. When you enter a command in the terminal, the system looks for the executable file in each of the directories listed in the PATH variable, in order.

HOME: This variable specifies the path to the user's home directory. This is the default location where many programs store user-specific configuration files and data.

USER: This variable stores the name of the current user.

SHELL: This variable specifies the path to the user's default shell.

EDITOR: This variable specifies the path to the user's preferred text editor.

LANG: This variable specifies the user's default language.

In addition to these system-wide environment variables, users can also define their own custom environment variables to store data or settings that are specific to their workflow. For example, a developer might define an environment variable called PROJECT_HOME to store the path to their project directory, or a sysadmin might define an environment variable called SERVER_NAME to store the name of their server.

By default, environment variables are inherited from the parent process when a new process is created. This means that environment variables set in a parent shell session will be available in any child processes spawned from that session, unless explicitly overwritten or unset.

![image](Images/image-KOJIXABG.png)

## Examining The Environment.

![image](Images/image-8OLLAO0U.png)

To examine the environment in Linux, you can use the env command. This command will print out all of the environment variables currently set in your shell session.

For example, to see the value of the PATH environment variable, you can run:

![image](Images/image-E4RBZGSH.png)

To view all of the environment variables currently set in your shell session, you can run:

![image](Images/image-BOKDX3ZH.png)

This will output a list of all the environment variables, along with their values.

You can also use the printenv command to display the values of specific environment variables. For example:

![image](Images/image-LYWO3LX6.png)

This command will print out the value of the HOME environment variable, which specifies the path to the user's home directory.

![image](Images/image-KOJIXABG.png)

## How Is The Environment Established?

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

The Linux environment is established when a user logs in to the system. During the login process, the system reads configuration files and executes scripts that set up the environment for the user's session.

There are several files that are involved in setting up the environment in Linux:

/etc/profile: This file contains system-wide environment settings that are applied to all users. It is executed when a user logs in to the system, and sets up the default environment variables and paths.

/etc/bashrc: This file contains system-wide settings for the Bash shell. It is executed every time a new Bash shell is opened, and sets up global environment variables and aliases.

~/.bash_profile: This file contains user-specific environment settings that are applied only to the user who owns the file. It is executed when the user logs in to the system, and sets up environment variables and paths specific to that user.

~/.bashrc: This file contains user-specific settings for the Bash shell. It is executed every time a new Bash shell is opened, and sets up aliases and other user-specific settings.

In addition to these files, there are also system-wide and user-specific configuration files for other shells, such as /etc/csh.cshrc and ~/.cshrc for the C shell, and /etc/zshrc and ~/.zshrc for the Z shell.

![image](Images/image-KOJIXABG.png)

## What's In A Startup File?

![image](Images/image-8OLLAO0U.png)

A startup file, also known as a startup script, is a shell script that is executed when a user logs in to the system. It is responsible for setting up the environment for the user's session, including environment variables, aliases, and shell options.

The specific contents of a startup file can vary depending on the shell being used, but most startup files perform the following tasks:

Set environment variables: The startup file will set environment variables that are used by the shell and other programs. This includes variables like PATH that determine where the shell will look for executable files.

Define aliases: The startup file can define aliases that provide shortcuts for frequently used commands. For example, alias ll='ls -l' defines an alias ll that will execute the ls -l command.

Configure shell options: The startup file can configure options for the shell, such as whether to show hidden files or whether to use color output.

Execute other scripts: The startup file can execute other shell scripts or commands that are needed to set up the environment. This might include scripts that set up system-wide variables or configure network settings.

Display messages: The startup file can display messages to the user to provide information about the environment or to alert the user to potential issues.

Some common startup files in Linux include .bash_profile and .bashrc for the Bash shell, .zprofile and .zshrc for the Z shell, and .tcshrc and .cshrc for the C shell.

![image](Images/image-KOJIXABG.png)

## Which Files Should We Modify?

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

The specific files that should be modified to set up the environment can vary depending on the specific Linux distribution and shell being used. However, here are some common files that are often modified to set up the environment:

~/.bashrc: This file is executed by Bash every time a new interactive shell is started. It is a good place to put aliases, functions, and environment variables that should be set for all Bash shells.

~/.bash_profile or ~/.profile: These files are executed by Bash when the user logs in. They are a good place to put environment variables that should be set for all login shells.

~/.bash_logout: This file is executed by Bash when the user logs out. It is a good place to put commands that should be executed when the user logs out, such as cleaning up temporary files.

/etc/environment: This file is used by many Linux distributions to set system-wide environment variables.

/etc/profile: This file is executed by many shells (including Bash) when the user logs in. It is a good place to put system-wide environment variables and aliases.

It is important to be cautious when modifying these files, as incorrect modifications can cause problems with the system. It is recommended to make a backup of any file before modifying it, and to test any modifications in a non-production environment before deploying them to a live system.

![image](Images/image-KOJIXABG.png)

## Using A Text Editor

![image](Images/image-8OLLAO0U.png)

To modify the environment files, a text editor can be used. There are many text editors available on Linux, ranging from simple ones like nano to more advanced ones like vim or emacs.

Here are some basic steps for using a text editor to modify a file:

Open a terminal window.

Navigate to the directory where the file is located, using cd and ls commands if needed.

Open the file in the text editor. For example, to open ~/.bashrc in nano, you would run the command nano ~/.bashrc.

Make the necessary modifications to the file.

Save the changes and exit the text editor. In nano, you would use the Ctrl+O key combination to save the file and Ctrl+X to exit the editor.

![image](Images/image-KOJIXABG.png)

## 12 –Introduction To vi

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

Vi is a powerful and popular text editor that is included with most Unix-based operating systems, including Linux. It is a modal editor, which means that it has different modes for different tasks, such as inserting text, navigating the file, and executing commands. Vi can be daunting to new users, but it is a powerful tool that can greatly increase productivity once its basics are mastered.

To open a file in Vi, simply type vi followed by the filename. For example, to open a file called example.txt, you would run the command vi example.txt. Vi opens the file in command mode, which is the mode for executing commands. To enter insert mode, which is the mode for inserting and editing text, press the i key. To exit insert mode and return to command mode, press the Esc key.

![image](Images/image-KOJIXABG.png)

## Why We Should Learn vi

![image](Images/image-8OLLAO0U.png)

Learning vi can be extremely beneficial for a number of reasons. Here are a few:

Vi is ubiquitous: vi is included on almost every Unix-based system, including Linux. This means that learning vi can be a valuable skill for system administrators, programmers, and anyone else who works with Unix-based systems.

Vi is powerful: vi has many features and commands that can greatly increase productivity once mastered. These include powerful search and replace functionality, the ability to work with multiple files at once, and support for regular expressions.

Vi is lightweight: because vi is a command-line text editor, it requires very few system resources compared to graphical editors. This can be particularly important when working with remote servers or low-power devices.

Vi can help you learn other command-line tools: learning vi requires familiarity with the command line, which can help you become more comfortable with other command-line tools and utilities.

Vi has a long history: vi has been around since the 1970s and has a large and active community of users and developers. Learning vi can help you become a part of this community and gain a deeper understanding of Unix-based systems and their history.

![image](Images/image-KOJIXABG.png)

## Starting And Stopping vi

![image](Images/image-8OLLAO0U.png)

To start vi, open a terminal and type vi followed by the name of the file you want to edit. For example, if you want to edit a file called myfile.txt, you would type:

![image](Images/image-LGXCTLSX.png)

Vi will open and display the contents of the file. By default, vi starts in command mode, which means that you cannot edit the text until you switch to insert mode.

To switch to insert mode, press the i key. You can now edit the text as you would in any other text editor.

When you are finished editing the file, press the Esc key to return to command mode. You can now save your changes and exit vi.

To save your changes and exit vi, type :wq and press Enter. This will write your changes to the file and quit vi.

If you do not want to save your changes, you can exit vi without saving by typing :q! and pressing Enter. This will quit vi without saving any changes.

If you want to save your changes but do not want to quit vi, you can save the changes by typing :w and pressing Enter. You can then continue editing the file in vi.

![image](Images/image-KOJIXABG.png)

## Editing Modes

![image](Images/image-8OLLAO0U.png)

There are two main editing modes in vi: command mode and insert mode.

In command mode, you can navigate the document, select text, and perform various editing tasks without actually inserting any new text into the document. Some of the most common commands in command mode include:

h, j, k, and l: move the cursor left, down, up, and right, respectively.

x: delete the character under the cursor.

dd: delete the current line.

yy: copy the current line.

p: paste the contents of the clipboard after the current line.

u: undo the last change.

To enter insert mode, press the i key while in command mode. In insert mode, you can insert new text into the document by typing on the keyboard. To return to command mode, press the Esc key.

In addition to command mode and insert mode, there are also other modes in vi, such as visual mode, which allows you to select and manipulate text visually, and ex mode, which provides a more powerful command-line interface for performing advanced editing tasks.

![image](Images/image-KOJIXABG.png)

## Moving The Cursor Around

![image](Images/image-8OLLAO0U.png)

In vi, you can move the cursor around the document using various commands. Some of the most commonly used cursor movement commands include:

h: move the cursor one character to the left.

j: move the cursor down one line.

k: move the cursor up one line.

l: move the cursor one character to the right.

0: move the cursor to the beginning of the current line.

$: move the cursor to the end of the current line.

gg: move the cursor to the beginning of the document.

G: move the cursor to the end of the document.

<n>G: move the cursor to the beginning of line number n.

Note that these commands are used in command mode. In insert mode, typing h, j, k, or l will insert those letters into the document. To return to command mode, press the Esc key.

![image](Images/image-KOJIXABG.png)

## Appending Text

![image](Images/image-8OLLAO0U.png)

In vi, there are several ways to append text to a document. One of the most common methods is to use the a command, which puts you into insert mode after the current cursor position. Here are the steps to append text using the a command:

Move the cursor to the point in the document where you want to start appending text.

Press the a key to enter insert mode after the current cursor position.

Type the text you want to append to the document.

Press the Esc key to return to command mode.

Another way to append text is to use the A command, which puts you into insert mode at the end of the current line. Here are the steps to append text using the A command:

Move the cursor to the end of the line where you want to start appending text.

Press the A key to enter insert mode at the end of the line.

Type the text you want to append to the document.

Press the Esc key to return to command mode.

Finally, you can also append text using the i command, which puts you into insert mode before the current cursor position. Here are the steps to append text using the i command:

Move the cursor to the point in the document where you want to start appending text.

Press the i key to enter insert mode before the current cursor position.

Type the text you want to append to the document.

Press the Esc key to return to command mode.

![image](Images/image-KOJIXABG.png)

## Opening A Line

![image](Images/image-8OLLAO0U.png)

In vi, you can open a new line above or below the current cursor position using the o and O commands, respectively.

To open a new line below the current cursor position, follow these steps:

Move the cursor to the point in the document where you want to add the new line.

Press the o key to open a new line below the cursor position.

Type the text you want to add to the new line.

Press the Esc key to return to command mode.

To open a new line above the current cursor position, follow these steps:

Move the cursor to the point in the document where you want to add the new line.

Press the O key to open a new line above the cursor position.

Type the text you want to add to the new line.

Press the Esc key to return to command mode.

![image](Images/image-KOJIXABG.png)

## Deleting Text

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In vi, you can delete text using various commands depending on the scope of deletion.

Here are some common commands for deleting text in vi:

x - Deletes the character under the cursor.

dd - Deletes the current line.

d0 - Deletes from the cursor to the beginning of the line.

d$ - Deletes from the cursor to the end of the line.

dw - Deletes the current word.

To use any of these commands, first ensure that you are in command mode by pressing the Esc key. Then, move the cursor to the beginning of the text you want to delete and press the appropriate deletion command. The text will be removed from the document and stored in the vi buffer, allowing you to paste it elsewhere if desired.

![image](Images/image-KOJIXABG.png)

## Cutting, Copying, And Pasting Text

![image](Images/image-8OLLAO0U.png)

In vi, the process of cutting, copying, and pasting text is accomplished using the yank, delete, and put commands.

Here are the basic steps to cut or copy text and paste it elsewhere in the document:

Move the cursor to the beginning of the text you want to cut or copy.

Press the v key to enter visual mode.

Move the cursor to the end of the text you want to cut or copy. This will highlight the text.

Press y to yank (copy) the text or d to delete (cut) the text.

Move the cursor to the desired paste location.

Press the p key to put (paste) the text after the cursor or P to put it before the cursor.

Note that when you use the y command to yank text, it is stored in the vi buffer and can be pasted multiple times. However, when you use the d command to delete text, it is only stored in the buffer until the next time you cut or copy text.

![image](Images/image-KOJIXABG.png)

## Joining Lines

![image](Images/image-8OLLAO0U.png)

In vi, joining lines can be accomplished using the J command. This command joins the current line with the next line by removing the newline character between them.

Here are the basic steps to join lines in vi:

Move the cursor to the first line you want to join.

Press the J key to join the current line with the next line.

Repeat this process for each additional line you want to join.

Alternatively, you can also use a range command to join multiple lines at once. For example, to join the next 3 lines, you can use the command :.,.+2J (assuming the cursor is currently on the first line you want to join).

![image](Images/image-KOJIXABG.png)

## Search-And-Replace

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

In vi, you can perform search-and-replace operations using the :s command. The syntax for this command is as follows:

less

:[range]s/pattern/replacement/[flags]

where [range] is an optional range of lines to search and replace in, pattern is the regular expression pattern to search for, replacement is the text to replace the pattern with, and [flags] are optional flags that modify the behavior of the command.

Here are some examples:

To replace the first occurrence of the word "apple" with "orange" on the current line:

![image](Images/image-CJJTTG07.png)![image](Images/image-NQQQ6B20.png)

To replace all occurrences of the word "apple" with "orange" on the current line:

![image](Images/image-CJJTTG07.png)![image](Images/image-RRF72091.png)

To replace all occurrences of the word "apple" with "orange" in the entire file:

![image](Images/image-CJJTTG07.png)![image](Images/image-1IOXITF1.png)![image](Images/image-CJJTTG07.png)

To replace all occurrences of the word "apple" with "orange" in lines 10 to 20 of the file:

![image](Images/image-14VQB9T5.png)

To replace all occurrences of the word "apple" with "orange" in the entire file, but prompt for confirmation before each replacement:

![image](Images/image-MB2YP2R7.png)

Note that the s command only replaces the first occurrence of the pattern on each line by default. To replace all occurrences on a line, use the g flag at the end of the command. Also, if the pattern or replacement contain any slashes, you can use a different delimiter character instead, such as | or #.

![image](Images/image-KOJIXABG.png)

## Editing Multiple Files

![image](Images/image-8OLLAO0U.png)

In vi, you can edit multiple files using the :args and :next commands. The :args command sets the argument list to the specified files, and the :next command goes to the next file in the argument list. Here's an example workflow:

Open vi with the files you want to edit:

![image](Images/image-CJJTTG07.png)![image](Images/image-ZHQKB4PD.png)

Check the current argument list:

![image](Images/image-CJJTTG07.png)![image](Images/image-F98W8BMR.png)

This will show the list of files you opened.

Go to the next file in the argument list:

![image](Images/image-CJJTTG07.png)![image](Images/image-T19XAQY0.png)

This will open the next file in the list.

Save and close the file:

![image](Images/image-CJJTTG07.png)![image](Images/image-7HDWNW2S.png)

Repeat steps 3 and 4 to edit the remaining files in the list.

Alternatively, you can use a loop to edit all the files in the list:

Open vi with the files you want to edit:

![image](Images/image-CJJTTG07.png)![image](Images/image-S57Q6SVR.png)

This will open all the files that match the pattern.

Edit the first file:

![image](Images/image-CJJTTG07.png)![image](Images/image-E15S7G3H.png)

Save and close the file:

![image](Images/image-CJJTTG07.png)![image](Images/image-7HDWNW2S.png)

Edit the next file:

![image](Images/image-CJJTTG07.png)![image](Images/image-T19XAQY0.png)

Repeat steps 3 and 4 to edit the remaining files in the list.

Note that you can use any pattern that matches the files you want to edit, such as *.txt or file?.txt. Also, you can use other commands such as :prev to go to the previous file in the list, or :args to set a new argument list.

![image](Images/image-KOJIXABG.png)

## 13 – Customizing The Prompt

![image](Images/image-8OLLAO0U.png)

The prompt is the text that appears in the terminal to indicate that the shell is ready to accept a command. By default, the prompt includes the username, hostname, and the current working directory. However, you can customize the prompt to display any information you like using special escape sequences.

![image](Images/image-KOJIXABG.png)

## Anatomy Of A Prompt

![image](Images/image-8OLLAO0U.png)

A prompt is a symbol or message that indicates to the user that the system is ready to receive commands. In Unix-like operating systems, the prompt is typically a text string that is displayed in the terminal or console window. The most common prompt is the shell prompt, which is displayed by the command shell (such as Bash or Zsh) and shows the current working directory, the username, the hostname, and the shell symbol (such as $ or #).

The prompt can be customized to suit the user's preferences or requirements. Users can change the prompt's appearance, add or remove information, and modify its behavior. This customization is done by setting the value of the PS1 environment variable, which defines the prompt string.

The PS1 string can include various escape sequences that represent different types of information. For example, \u represents the username, \h represents the hostname, \w represents the current working directory, and \n represents a new line. By combining these escape sequences with other text and symbols, users can create a prompt that suits their needs and preferences.

![image](Images/image-KOJIXABG.png)

## Trying Some Alternative Prompt Designs

![image](Images/image-8OLLAO0U.png)

Sure, let's try some alternative prompt designs using the PS1 environment variable. Here are a few examples:

Basic prompt with just the current directory:

![image](Images/image-CJJTTG07.png)![image](Images/image-Z9ZS7J5B.png)

This will display the current working directory followed by a space and a dollar sign.

Prompt with the current directory and Git branch name (if applicable):

![image](Images/image-CJJTTG07.png)![image](Images/image-GDZPDEPB.png)

This will display the current working directory followed by the Git branch name (in parentheses) if the current directory is a Git repository.

Prompt with colors and user/host information:

![image](Images/image-CJJTTG07.png)![image](Images/image-2DGZCUAP.png)

This will display the username and hostname in green, followed by the current working directory in blue, and a dollar sign.

Prompt with a custom symbol and the exit status of the last command:

![image](Images/image-C0ATE5RL.png)

This will display a sun symbol, followed by the current working directory, and the exit status of the last command in red.

![image](Images/image-KOJIXABG.png)

## Adding Color

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

Sure, adding color to your prompt can help to make it more visually appealing and easier to read. Here's an example of how you can add color to your prompt:

![image](Images/image-CJJTTG07.png)![image](Images/image-VKSDJTH4.png)

In this example, the prompt starts with the username and hostname in bold green, followed by a colon in bold white, then the current working directory in bold blue, and finally a dollar sign in the default text color.

Here's a breakdown of the color codes used in this example:

\[\033[ is the start of an escape sequence.

1;32m sets the color to bold green.

\u displays the username.

@ displays the @ symbol.

\h displays the hostname.

: displays a colon in bold white.

1;34m sets the color to bold blue.

\w displays the current working directory.

\[\033[0m\] resets the color to the default text color.

\$ displays a dollar sign.

![image](Images/image-KOJIXABG.png)

## Terminal Confusion

![image](Images/image-8OLLAO0U.png)

Terminal confusion can occur when you are using multiple terminal windows or tabs at the same time, and you lose track of which terminal is running which command or process. Here are a few tips to avoid terminal confusion:

Use different colors for each terminal: Most terminal emulators allow you to change the color of the prompt or background of each terminal window or tab. You can assign a different color to each terminal to help you distinguish them more easily.

Rename your terminal tabs: Many terminal emulators allow you to rename your terminal tabs. You can use this feature to give a descriptive name to each terminal tab, so you can quickly identify which terminal is running which command or process.

Use a terminal multiplexer: A terminal multiplexer, such as GNU Screen or tmux, allows you to split your terminal window into multiple panes, each running a different command or process. You can switch between panes or resize them as needed, making it easier to manage multiple processes in the same terminal window.

Use job control: In the terminal, you can use job control commands to manage running processes. For example, you can use jobs to list all running processes, fg to bring a process to the foreground, or bg to run a process in the background. These commands can help you keep track of your running processes and switch between them more easily.

![image](Images/image-KOJIXABG.png)

## Moving The Cursor

![image](Images/image-8OLLAO0U.png)

Moving the cursor refers to changing the position of the text input cursor in the command line interface. This allows you to insert or delete text at a specific location in the input line, rather than just appending to the end.

There are several ways to move the cursor in the command line interface, including:

Arrow keys: On most systems, you can use the up, down, left, and right arrow keys to move the cursor in the corresponding direction.

Home/End keys: The Home key moves the cursor to the beginning of the current line, while the End key moves the cursor to the end of the line.

Ctrl + A/Ctrl + E: On Unix-based systems, you can use the Ctrl + A and Ctrl + E shortcuts to move the cursor to the beginning and end of the line, respectively.

Ctrl + Left/Right arrow keys: This shortcut allows you to move the cursor one word to the left or right, rather than one character at a time.

Mouse click: On some systems, you can use the mouse to click on a specific location in the command line interface, which will move the cursor to that location.

![image](Images/image-KOJIXABG.png)

## Saving The Prompt

![image](Images/image-8OLLAO0U.png)

Saving the prompt refers to customizing and saving the command prompt in a way that is persistent across terminal sessions. This allows you to have a personalized prompt that appears every time you open a new terminal window or log in to your system.

To customize and save the prompt, you will need to modify your shell configuration file. The location and name of this file can vary depending on your operating system and shell, but it is often called .bashrc, .bash_profile, or .zshrc.

Here's an example of how to customize and save the prompt in a Linux system running the Bash shell:

Open your shell configuration file in a text editor. For example, enter the following command in a terminal window:

![image](Images/image-CJJTTG07.png)![image](Images/image-77YNTLU2.png)

Find the line that sets the PS1 variable. This variable controls the prompt format. The default value of PS1 is usually set to '\s-\v$ ', which displays the name and version of the shell.

Modify the PS1 variable to create a custom prompt. You can add text, colors, and special characters to the prompt. Here's an example:

![image](Images/image-CJJTTG07.png)![image](Images/image-JWY6J5VR.png)

This prompt displays the username, hostname, and current directory in green and blue colors.

Save the file and exit the text editor.

Reload your shell configuration file by entering the following command:

![image](Images/image-CJJTTG07.png)![image](Images/image-2YMYT6K1.png)

Now, every time you open a new terminal window or log in to your system, you will see your custom prompt.

![image](Images/image-KOJIXABG.png)

14 – Storage Media

![image](Images/image-8OLLAO0U.png)![image](Images/image-KOJIXABG.png)

## Mounting And Unmounting Storage Devices

![image](Images/image-8OLLAO0U.png)

Mounting and unmounting storage devices is an essential task when working with a Linux system. When you connect a storage device to your computer, such as a USB flash drive or an external hard drive, you need to mount it in order to access its contents. Conversely, you need to unmount the device before unplugging it to prevent data loss.

The mount command is used to mount a device, and the umount command is used to unmount it. To mount a device, you need to specify the device's file system type, its device file name, and the mount point, which is the location in the file system where you want to mount the device.

For example, to mount a USB flash drive with the ext4 file system on the mount point /mnt/usb, you can use the following command:

![image](Images/image-NBLHZP9H.png)

Here, /dev/sdb1 is the device file name of the USB flash drive, and sudo is used to run the command with administrative privileges.

To unmount the device, you can use the following command:

![image](Images/image-VTJUAA9J.png)

This will unmount the device from the file system, and you can safely unplug it from your computer.

It's important to note that you should always unmount a device before unplugging it, as it ensures that all data has been written to the device and prevents data loss or corruption.

![image](Images/image-KOJIXABG.png)

## Viewing A List Of Mounted File Systems

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

To view a list of mounted file systems in Linux, you can use the mount command without any arguments. Open a terminal and enter the following command:

![image](Images/image-90791SUW.png)

This will display a list of currently mounted file systems along with their device names, mount points, file system types, and other information.

If you want to see more detailed information about the mounted file systems, you can use the -v option to enable verbose output:

![image](Images/image-ULKHSYEK.png)

This will display additional information about each mounted file system, such as mount options and file system labels.

You can also use the -t option to filter the output to show only file systems of a specific type. For example, to show only mounted ext4 file systems, you can use the following command:

![image](Images/image-DPDB5JZY.png)![image](Images/image-KOJIXABG.png)

## Determining Device Names

![image](Images/image-8OLLAO0U.png)

To determine the device name of a storage device in Linux, you can use various commands depending on the type of device.

For example, if you want to determine the device name of a USB drive that you just plugged into your system, you can use the dmesg command to view the kernel messages related to the device. Open a terminal and enter the following command immediately after plugging in the USB drive:

![image](Images/image-77D4BM2T.png)

This will display the last few kernel messages, including information about the USB drive such as its device name. The device name usually begins with /dev/sd followed by a letter indicating the drive and a number indicating the partition, such as /dev/sdb1.

Alternatively, you can use the lsblk command to list all the available storage devices and their associated device names. Open a terminal and enter the following command:

![image](Images/image-TR7CF8W4.png)

This will display a hierarchical view of all storage devices and their partitions along with their device names, mount points, and other information.

If you are looking for the device name of a specific partition that is already mounted, you can use the df command to display the file system information for the mounted partition, which includes the device name. Open a terminal and enter the following command:

![image](Images/image-MPTGP3BA.png)

Replace /path/to/mount/point with the actual mount point of the partition that you are interested in. This will display the file system information for the partition, including the device name.

![image](Images/image-KOJIXABG.png)

## Creating New File Systems

![image](Images/image-8OLLAO0U.png)

Creating a new file system involves several steps, including partitioning the disk, creating a file system on the partition, and mounting the file system. Here's an overview of the steps:

Identify the disk: Use the fdisk command to identify the disk that you want to partition. For example, fdisk -l will list all the disks that are connected to the system.

Create a new partition: Use the fdisk command to create a new partition on the disk. For example, fdisk /dev/sdb will allow you to create a new partition on the /dev/sdb disk.

Create a file system: Use the appropriate command to create a file system on the partition you just created. For example, if you want to create an ext4 file system, you can use the mkfs.ext4 command. The command syntax is mkfs.<file system type> <device>. For example, mkfs.ext4 /dev/sdb1.

Mount the file system: Create a directory to serve as the mount point for the file system, then mount the file system on the directory. For example, if you create a directory called /mnt/mydrive, you can mount the file system on that directory using the mount command: mount /dev/sdb1 /mnt/mydrive.

![image](Images/image-KOJIXABG.png)

## Manipulating Partitions With fdisk

![image](Images/image-8OLLAO0U.png)![image](Images/image-CJJTTG07.png)

fdisk is a command-line utility used for creating and manipulating disk partitions on Linux systems. Here's an example of how to use fdisk to create a new partition:

Open a terminal and run the fdisk command with the name of the device you want to partition. For example, to partition /dev/sdb, run the command:

![image](Images/image-CJJTTG07.png)![image](Images/image-UB61XEIN.png)

Use the m command to display a list of available commands. This will help you navigate the fdisk interface.

Use the p command to display the partition table for the device. This will show you any existing partitions on the device.

Use the n command to create a new partition. fdisk will prompt you for information about the new partition, such as the starting and ending sectors.

Use the t command to set the partition type. fdisk will prompt you for the partition number and the new partition type code.

Use the w command to write the changes to the partition table and exit fdisk.

![image](Images/image-KOJIXABG.png)

## Creating A New File System With mkfs

![image](Images/image-8OLLAO0U.png)

To create a new file system on a block device, you can use the mkfs command followed by the device name and the desired file system type. For example, to create an ext4 file system on /dev/sdb1, you would use the following command:

![image](Images/image-8Z42CGY4.png)

Note that this will destroy any existing data on the device, so be careful to select the correct device. Additionally, you may want to specify additional options to mkfs to fine-tune the file system's characteristics. You can use the man mkfs command to learn more about the available options.

![image](Images/image-KOJIXABG.png)

## Testing And Repairing File Systems

![image](Images/image-8OLLAO0U.png)

Testing and repairing file systems is an important aspect of managing storage devices. Here are some tools and techniques that can be used for this purpose:

fsck - The fsck (file system check) command is used to check and repair file systems. It can detect and fix a variety of errors, including bad blocks, orphaned inodes, and incorrect file types.

badblocks - The badblocks command is used to scan a device for bad blocks. Bad blocks are areas of the disk that are physically damaged and cannot be used to store data. If bad blocks are found, they can be marked as unusable so that the file system does not attempt to write data to them.

SMART - SMART (Self-Monitoring, Analysis and Reporting Technology) is a technology built into modern hard drives that can provide information about the health of the drive. SMART can be used to detect problems early, before they cause data loss.

ddrescue - The ddrescue command is used to recover data from damaged disks. It works by copying the undamaged parts of the disk to a new disk or file, skipping over any damaged areas. This can help to recover as much data as possible from a damaged disk.

dd - The dd command is a powerful tool that can be used for a variety of disk-related tasks. It can be used to copy disks or partitions, create disk images, and write data to specific areas of a disk. However, it is also a dangerous tool, as it can overwrite data without warning, so it should be used with caution.

![image](Images/image-KOJIXABG.png)

## Formatting Floppy Disks

![image](Images/image-8OLLAO0U.png)

In Linux, formatting a floppy disk can be done using the mkfs command followed by the name of the floppy disk device. The floppy disk device in Linux is typically /dev/fd0, but may vary depending on the system configuration.

To format a floppy disk, first insert it into the floppy drive and ensure that it is not mounted. Then, run the following command:

![image](Images/image-92L3ZDL6.png)

This will format the floppy disk using the VFAT file system, which is compatible with both Windows and Linux. The sudo command is used to run the mkfs command with elevated privileges, as formatting a disk requires superuser permissions.

Once the formatting process is complete, the floppy disk can be mounted using the mount command and accessed like any other file system. To unmount the floppy disk, use the umount command followed by the mount point.

![image](Images/image-KOJIXABG.png)

## Moving Data Directly To/From Devices

![image](Images/image-8OLLAO0U.png)

Moving data directly to/from devices is a low-level operation that requires special care and knowledge to avoid damaging the device or the data. In general, it is not recommended for most users, as there are more user-friendly and safer ways to work with devices.

However, for advanced users or system administrators, it may be necessary to move data directly to/from a device in certain situations, such as recovering data from a damaged drive, creating a backup image of a drive, or testing the read/write speed of a device.

To move data directly to/from a device, the dd command can be used. dd stands for "data duplicator" or "disk duplicator," and it can copy data from one location to another, block by block. It can also be used to convert the format of data, such as converting between ASCII and EBCDIC.

The basic syntax of dd is as follows:

![image](Images/image-O21JITAU.png)

if specifies the input file or device, and of specifies the output file or device. bs specifies the block size, which can be used to optimize the transfer speed.

For example, to create a backup image of a hard drive located at /dev/sda and save it to a file called backup.img, the following command can be used:

![image](Images/image-JP4OLSYB.png)

This command will copy the entire contents of /dev/sda to backup.img, using a block size of 4 megabytes.

![image](Images/image-KOJIXABG.png)

## Creating CD-ROM Images

![image](Images/image-8OLLAO0U.png)

To create a CD-ROM image, you can use the dd command along with the if and of options. Here's an example:

![image](Images/image-9R6R1555.png)

This command reads the contents of the CD-ROM from the device file /dev/cdrom and writes it to the file mycdrom.iso. You can then burn the image to a CD-ROM using a CD-burning program.

Note that the device file name /dev/cdrom may differ depending on your system configuration. You can use the dmesg command to determine the correct device file name if you're not sure.

![image](Images/image-KOJIXABG.png)

## Writing CD-ROM Images

![image](Images/image-8OLLAO0U.png)

To write a CD-ROM image, you need a CD burner and a software application that supports the writing of CD-ROM images. One such application is the "cdrecord" command-line tool.

Assuming you have a CD-ROM image file named "image.iso" and your CD burner is located at "/dev/cdrom", you can use the following command to write the image to the CD:

![image](Images/image-TRVF94Y8.png)

This command tells cdrecord to use the device located at "/dev/cdrom" as the target for writing the CD. The "image.iso" file is specified as the source for the data to be written.

Congratulations on finishing the book! We hope that it has given you a solid understanding of the Linux command line and its many powerful features. Remember that the command line is a tool that can be used to greatly increase your productivity and control over your system. Don't be afraid to experiment and try new things, and always keep learning. Thank you for reading, and happy command lining!