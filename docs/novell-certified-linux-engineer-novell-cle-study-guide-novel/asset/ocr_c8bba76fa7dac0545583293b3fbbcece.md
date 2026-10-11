For example, you could enter `locate gnome-term-linux.png` to locate the graphic file you used for your terminal icon in GNOME.

+   - **ls**—This command is similar to the **dir** command. It is used to display the contents of a directory. The syntax is **ls *directory_name***. If no directory name is provided, it will display the contents of the current directory. If you append the -1 switch, the owners and permissions assigned to the files in the directory will also be displayed.

+   - **mkdir**—This command is used to create a directory in the file system. It is similar to the MD command in DOS. The syntax is **mkdir *path/directory_name***. If you omit the path, the directory will be created in the current directory.

+   - **more**—This command is similar to the **less** command. It is used in conjunction with another command, such as **dir**, **ls**, or **cat**, to pause long displays one screen at a time. For example, if you were to enter **dir /usr/bin -o | more**, the output will pause at each screen, allowing you to read the text.

+   - **mv**—The **mv** command is similar the **MOVE** command under DOS. It is used to move files within the file system. It can also be used to rename a file in place. The syntax for this command is **mv *source_path/file* *destination_path***.

+   - **pwd**—This command displays the current directory.

+   - **rm**—This command is similar to the **DEL** command under DOS. It is used to delete a file in the file system. The syntax is **rm *file_name***.

+   - **rmdir**—This command is similar to the **RD** command under DOS. It's used to delete a directory from the file system. The syntax is **rmdir *directory_name***.

+   - **tail**—This is a very useful command for viewing entries in text files, such as a log file. Log files can become quite large over time. There will be many times when you will actually only need to view the last few entries in the file. The **tail** command is used in these circumstances—it displays the last 10 lines of a text file (although you can configure it to display more). The syntax is **tail *file_name***. When troubleshooting a Linux system, one of the most useful tools I've found is to use **tail** on the */var/log/messages* file. By using the -f parameter, you can continuously monitor the file.

The preceding commands are very useful when you're maintaining a Linux system, especially one with NNSL installed. At this point, we need to discuss in depth several utilities that you must know how to use in order to install and configure NNS on your Linux system. These include **mount**, **tar**, **gunzip**, and **vi**.