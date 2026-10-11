link count, user ID, group ID, size in bytes, time of last access, and so on. (See “The stat and lstat Functions” in Section 16.1.12.)

A directory is a specific file type maintained by the UNIX kernel. It is composed of a list of filenames. Each filename has a corresponding number that points to the information about the file. The number, called an **inode number**, is a pointer to an inode. The inode contains information about the file as well as a pointer to the location of the file’s data blocks on disk. The following functions allow you to manipulate directories, change permissions on files, create links, and so forth.

| Directory Entry |  |
| --- | --- |
| Inode # | Filename |

**Windows.** Files and directories contain data as well as meta information that describes attributes of a file or directory. The five basic attributes of Win32 files and directories are **ARCHIVE**, **HIDDEN**, **READONLY**, and **SYSTEM**. The attributes of a file or directory are stored in a byte, with the bit value either on or off. Each bit value is added to the file type so that if you have a hidden, readonly directory, the attribute value is 00010011. See Table 16.2.

**Table 16.2** Basic File and Directory Attributes

| Attribute | Description | Bit Value |
| :--- | :--- | :--- |
| ARCHIVE | Set when file content changes | 00100000 |
| HIDDEN | A file not shown in a directory listing | 00000010 |
| DIRECTORY | A special tag to indicate a folder/directory | 00010000 |
| READONLY | A file that cannot be changed | 00000001 |
| SYSTEM | Special system files, such as **IO.SYS** and **MS-DOS.SYS** | 00000100 |

To retrieve and set file attributes, use the standard Perl extension **Win32::File**. All of the functions return **FALSE** (0) if they fail, unless otherwise noted. The function names are exported into the caller’s namespace by request. See Table 16.3.

**Table 16.3** Win32::File Functions

| Function | What It Does |
| :--- | :--- |
| GetAttributes(*Filename*, *ReturnedAttributes*) | Gets attributes of a file or directory. *ReturnedAttributes* will be set to the **or**-ed combination of the filename attributes. |
| SetAttributes(*Filename*, *NewAttributes*) | Sets the attributes of a file or directory. *newAttributes* must be an **or**-ed combination of the attributes. |