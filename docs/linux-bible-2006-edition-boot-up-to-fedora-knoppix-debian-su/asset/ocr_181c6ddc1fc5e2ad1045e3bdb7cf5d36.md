# Linux File Systems Versus Windows-Based File Systems

Although similar in many ways, the Linux file system has some striking differences from file systems used in MS-DOS and Windows operating systems. Here are a few:

+   * MS-DOS and Windows file systems, drive letters represent different storage devices (for example, A: is a floppy drive and C: is a hard disk). In Linux, all storage devices are fit into the file hierarchy. So, the fact that all of /usr may be on a separate disk or /mnt/rem1 is a file system from another computer is invisible to the user.
* Slashes, rather than backslashes, are used to separate directory names in Linux. So, C:\home\chris in an MS system is /home/chris in a Linux system.
* Filenames always have suffixes in DOS (such as .txt for files or .doc for word-processing). Although at times you can use that convention in Linux, three-character suffixes have no required meaning in Linux. They can be useful for identifying a file type. Many Linux applications and desktop environments use suffixes to determine the contents of a file.
* Every file and directory in a Linux system has permissions and ownership associated with it. Security varies varies among Microsoft systems. Because DOS and MS Windows began as single-user systems, file ownership was not built into those systems when they were designed. Later releases added features such as file and folder attributes to address this problem.

# Creating Files and Directories

As a Linux user, most of the files you save and work with will probably be in your home directory. Table 2-9 shows commands to create and use files.

| Table 2-9 Commands to Create and Use Files |
| Command | Result |
| cd | Change to another current working directory. |
| pwd | Print the name of the current working directory. |
| mkdir | Create a directory. |
| chmod | Change the permission on a file or directory. |
| ls | List the contents of a directory. |