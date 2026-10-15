this chapter. The group name indicates the group permitted to access the file object. In Figure 10-1, the file type for mydata is that of an ordinary file. Only one link exists, indicating the file has no other names and no other links. The owner’s name is chris, the same as the login name, and the group name is weather. Others probably also belong to the weather group. The size of the file is 207 bytes and it was last modified on February 20, at 11:55 A.M. The name of the file is mydata.

If you want to display this detailed information for all the files in a directory, simply use the ls -l command without an argument.

```
$ ls -l
-rw-r--r-- 1 chris weather 207 Feb 20 11:55 mydata
-rw-r--r-- 1 chris weather 568 Feb 14 10:30 today
-rw-r--r-- 1 chris weather 308 Feb 17 12:40 monday
```

All files in Linux have one physical format—a byte stream. A byte stream is just a sequence of bytes. This allows Linux to apply the file concept to every data component in the system. Directories are classified as files, as are devices. Treating everything as a file allows Linux to organize and exchange data more easily. The data in a file can be sent directly to a device such as a screen because a device interfaces with the system using the same byte-stream file format as regular files.

This same file format is used to implement other operating system components. The interface to a device, such as the screen or keyboard, is designated as a file. Other components, such as directories, are themselves byte-stream files, but they have a special internal organization. A directory file contains information about a directory, organized in a special directory format. Because these different components are treated as files, they can be said to constitute different file types. A character device is one file type. A directory is another file type. The number of these file types may vary according to your specific implementation of Linux. Five common types of files exist, however: ordinary files, directory files, first-in first-out pipes, character device files, and block device files. Although you may rarely reference a file’s type, it can be useful when searching for directories or devices. Later in the chapter, you see how to use the file type in a search criterion with the find command to search specifically for directory or device names.

Although all ordinary files have a byte-stream format, they may be used in different ways. The most significant difference is between binary and text files. Compiled programs are examples of binary files. However, even text files can be classified according to their different uses. You can have files that contain C programming source code or shell commands, or even a file that is empty. The file could be an executable program or a directory file. The Linux file command helps you determine what a file is used for. It examines the first few lines of a file and tries to determine a classification for it. The file command looks for special keywords or special numbers in those first few lines, but it is not always accurate. In the next example, the file command examines the contents of two files and determines a classification for them:

```
$ file monday reports
monday: text
reports: directory
```

If you need to examine the entire file byte by byte, you can do so with the od (octal dump) command. The od command performs a dump of a file. By default, it prints every