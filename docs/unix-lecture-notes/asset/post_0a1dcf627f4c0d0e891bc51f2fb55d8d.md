
## 1.7 Learning System Programming by Example

The number of system calls and library functions is so large that mere mortals cannot remember them all. Trying to learn all of the intricacies and details of the UNIX API by reading through reference manuals and user documentation would be a painstaking task. Fortunately, people often learn well by example. Rather than studying the reference manuals and documentation, we can learn the API little by little by writing programs that use it. One starts out simple, and over time adds complexity.

Bruce Molay [1] uses an excellent strategy for learning how to write system programs and discover the UNIX API:

- 1. Pick an existing program that uses the API, such as a shell command;
- 2. Using the system man pages and other information available online, investigate the system calls and kernel data structures that this program most likely uses in its implementation; and
- 3. Write a new version of the program, iteratively improving it until it behaves just like the actual command.

By repeating this procedure over and over, one can familiarize oneself with the relevant portions of the API as well as the resources needed to learn about it. When it is time to write a full-fledged application, the portions of it that must communicate with the kernel should be relatively easy to write. We will partly follow this same paradigm in this sequence of notes on UNIX.

## 1.8 The UNIX File Hierarchy

The typical UNIX file hierarchy has several directories just under the root. Figure 1.4 shows part of a typical, but hypothetical, file hierarchy. The following directories should be present in most UNIX systems, but they are not all required. The only required directories are /dev and /tmp.

| Directory | Purpose |
|-----------|---------|
| bin | The repository for all essential binary executables including those shell commands that must be available when the computer is running in "single-user mode" (something like safe mode in Windows.) |
| boot | Static files of the boot loader |
| dev | The directory containing essential device files, which will be explained later. |
| etc | Where almost all host configuration files are stored. It is something like the registry file of Windows. |
| home | The directory where all user home directories are located, but not always. |
| lib | Essential shared libraries and kernel modules |
| media | Mount point for removable media |
| mnt | Mount point for mounting a file system temporarily |
| opt | Add-on application software packages |
| sbin | Essential system binaries |
| srv | Data for services provided by this system |
| tmp | Temporary files |

For example, /home/fac/sweiss is the absolute pathname to the directory sweiss in Figure 1.4 as is /home//fac///sweiss. The extra slashes are ignored. Observe that UNIX (actually POSIX) uses slashes, not backslashes, in pathnames: /usr/local, not \usr\local.

If a pathname does not begin with "/" it is called a relative pathname. When a process must resolve a relative pathname so that it can access the file, the pathname is assumed to start in the current working directory. In fact, the definition of the current working directory, also called the present working directory, is that it is the directory that a process uses to resolve pathnames that do not begin with a "/". For example, if the current working directory is /home/fac, then the pathname sweiss/testdata refers to a file whose absolute pathname is /home/fac/sweiss/testdata. The convention is to use pwd as a shorthand for the current working directory.

The environment variable PWD contains the absolute pathname of the current working directory. The command pwd prints the value of the PWD.

### 1.8.1.1 Working with Directories

This section may be skipped if you have experience working with directories at the user level. You do not need to know many commands in order to do most directory-related tasks in UNIX. This is a list of the basic commands. The principal tasks are navigation and displaying and altering their contents. The tables that follow give the command name and the simplest usage of it. They do not describe the various options or details of the command's usage.

| Command | Explanation |
|---|---|
| pwd | print the path of the current working directory (pwd) |
| ls [<dir1>] [<dir2>] ... | list the contents of the pwd, or <dir1>, <dir2> ... if supplied |
| cd [<dir>] | change pwd to HOME directory, or <dir> if it is supplied |
| mkdir <dir> [<dir2>] ... | create new directories <dir> (and <dir2> ...) in the pwd; |
| rmdir <dir> [<dir2>] ... | remove the EMPTY directory <dir> (and <dir2> ...) |
| rm -r <dir> | remove all contents of <dir> and <dir> itself. Dangerous!! |
| mv | see the explanation in Section 1.8.2 |

### Notes

- 1. The "p" in "pwd" stands for print, but it does not print on a printer. In UNIX, "printing" means displaying on the screen.
- 2. mkdir is the only way to create a directory
- 3. You cannot use rmdir to delete a directory if it is not empty.
- 4. You can delete multiple directories and their contents with rm -r, but this is not reversible, so be careful.
- 5. Commands that create and delete files are technically modifying directories, but these will be covered separately.

> 20 That is why the C instruction printf sends output to the display device, not the printer. In FORTRAN, by contrast, the print instruction sent output to the printer.
