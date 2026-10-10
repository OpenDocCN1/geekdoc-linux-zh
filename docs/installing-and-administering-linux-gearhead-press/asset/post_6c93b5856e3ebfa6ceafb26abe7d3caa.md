
## Directory Contents

Although it is customary to refer to a directory as a type of envelope that contains entire subdirectories, files, and their contents, in truth a directory is a unique type of file that is used to organize other files into a hierarchical structure. Thus, it contains only the information that is needed to access the files or other directories that are affiliated with it according to (hopefully, generally) some sort of logical order. As a result, a directory occupies less space than other types of files.

A directory resembles a table of contents. It lists the names of files and subdirectories and their corresponding inode numbers. When users execute a command to access a file, they use the filename. The system consults the directory to match the filename with its corresponding inode number and then accesses the inode table, which holds information about the file's characteristics (including its location). Then, once the system knows the location of the file, the data can be located. See Figure 4.1 for a partial listing of contents of the quoted directory, which is shown in its entirety in Figure 4.2, as well as an illustration of the corresponding inode table entries.

![](img/cae5c706c216875d12d4b7d28144cc71_118_0.png)

The following categories of information are stored in the inode table:

- The file type (directory or file)
- The mode (directory or file permissions; see Chapter 6, “Linux File Permissions,” for details)
- Links (which enable you to refer to a file by more than one name; for more information about linking, see Chapter 5)
- The userid of the file’s owner
- Group permissions
- The date the file was last accessed and modified
- The file size
- The file’s location

Remember that the filename is stored in a directory, *not* in the inode table. You might ask, “Why not store the inode information in the directory and dispense with the inode table?” Our answer is as follows: restricting information in the directory to filenames and inode numbers simplifies directory management and allows for the efficient use of disk space.

## Hierarchical Structure

The file structure depicted in Figure 4.2, called *a directory tree*, represents only part of a typical Linux file system. In this depiction, directory names appear in boxes and filenames are unboxed words.

The top of the structure is the root ( / ) directory. The root contains many directories that are critical in system operations. Root subdirectories depicted in Figure 4.2 are described in Table 4.1.

You can also access files on other computers on the network. The details of that process are beyond the scope of this book. For now, just remember that from a user’s perspective, the network is configured such that remote files appear to behave just like local files. The /home, /usr, /tmp, and /var directories are examples of directories whose files can be accessed by local and remote systems.

## Path Names

The purpose of a path name is to tell you the location of a file. You write a path name as a string of names separated by forward slashes ( / ). The rightmost name is the filename and can represent any type of file; the other names must be directories. A full path name, which is also referred to as an absolute path name, always begins with a forward slash ( / ) to indicate that it begins at the root directory. Path names that do not begin with a forward slash are termed relative. The path names in Example 4.1 refer to the files depicted in Figure 4.2. In the full path name, the first forward slash represents the root directory. In the relative path names, the current directory is presumed.

![](img/cae5c706c216875d12d4b7d28144cc71_120_0.png)

Figure 4.2 Linux directory tree.

### Table 4.1 Root Subdirectories

| SUBDIRECTORY | DESCRIPTION |
| :--- | :--- |
| /usr | System programs such as /usr/bin, which in turn contain user commands such as ls, cat, and date. Because the /usr directory generally contains system-related rather than user-related commands and utilities (despite its name), users do not have write access to this directory. In addition, because the files in this directory are system related, the directory is not considered very dynamic. |
| /dev | Special files that represent devices |
| /home | User login directories and files. When a user is added to the system, he or she is allocated an individual subdirectory, the name of which is the same as the user's login name. When users log in, they are put in their own directory and they can do whatever they want with it, such as create subdirectories within it and create, delete, move, copy, and rename files. Because users generally change their files regularly, the /home directory is considered quite dynamic. |
| /sbin | System utilities for system startup |
| /etc | System configuration files used by system administrators |
| /var | An abbreviation of variable, the var directory contains files that change with system activity. For example, this directory is typically used by or for many user-oriented programs, such as mail or printing. |
| /tmp | Holds files that are temporarily needed or created by applications and programs. For example, the vi editor (discussed in detail in Chapter 10, "The vi Editor") uses the /tmp directory as a buffer space until the file being worked on is written to disk. Compiler programs use /tmp to hold files written during compilation. When the compiler is finished, the files created there are eliminated. |
| /root | The top of the directory structure belonging to the root user |

### Example 4.1 Absolute and Relative Path Names

Let's look at the full or absolute path name for Don Quixote's weekly report, typically submitted to Lady Dulcinea on Monday morning:

```
/home/quixoted/admin/mon_rept
```

Now, let's look at the relative path names of other files in the Rueful Figures, Inc. directory structure. Let's presume that our current directory is Don Quixote's home directory, /home/quixoted:

```
admin/mon_rept
./test1
../dulcinea/pgms/suba
```

> **NOTE** Notice that this example contains two special files (one begins with a single dot; the other begins with a double dot). Both types were mentioned previously.

In `/test1`, the dot ( . ) represents the current directory; in other words, it says "start in this directory and look for the file called `test1`." In the last example, `../dulcinea/pgms/suba`, the leading two dots represent the parent directory to the current directory—in effect, saying "go back up one level to the home directory, look in Lady Dulcinea's home directory (`dulcinea`) for a directory called `pgms`, and then look there for a file called `suba`."

When you are trying to find a file, particularly in a complex, multi-layered structure, the single dot ( . ) and the double dot ( . . ) special files can save time by eliminating the need to describe the location of the file in relation to the root directory. They can be helpful also when programming an application if you do not know the absolute tree structure where the application might eventually be installed, but you do have a good idea where files are with respect to one another or with respect to an executable.

## Navigating the Directory Structure

Now that we know something about how directories are structured in Linux/UNIX, let's see how we can move around in the structure. Prior to knowing how to get around, though, it's best to know where you are to begin with. So the first command we'll show you is `pwd`. Then, to enable you to move around, we'll introduce `cd`.

### Locate the Working Directory Path: The `pwd` Command

The `pwd` (print working directory) command is a Linux/UNIX command for finding out which directory you are in; that is, where you are in the directory tree. This command always returns the full or absolute path name of the current working directory, as shown in Example 4.2. Without `pwd`, you would have no way of knowing which directory you are in. (Such information can be added to the command prompt, which we will discuss later.)
