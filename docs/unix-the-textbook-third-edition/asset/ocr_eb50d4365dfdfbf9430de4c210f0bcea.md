# TABLE 9.1 (Continued) Redirection Operators and Their Meaning in the Bourne, Korn, and C Shells

| Operator | Bourne Shell | Korn Shell | C Shell |
|---|---|---|---|
| cmd1 | &cmd2 |  | Connect standard output and standard error of command cmd1 to standard input of command cmd2 |
| (cmd>/dev/tty)>&file | | | Redirect standard error of the cmd command to file. |
| | & | | Allow stdout and stderr of a command to be attached to stdin of another command |

communicating with FIFOs do not have to have this kind of relationship—they can be independently executed programs on one system. For the command line use of pipes and FIFOs, this means that pipes can be used only for communication between commands connected via a pipeline and FIFOs can be used for communication between separately run commands. Another difference between pipes and FIFOs is that whereas a pipe is a main memory buffer maintained by the UNIX kernel and has no name, a FIFO is created on disk and has a name like a filename. This means that, like files, FIFOs have to be created and opened before they can be used for communication between processes. Thus, accessing a FIFO requires an access to the secondary storage device where it resides.

Pipes are process persistent, which means that they exist as long as the process that creates them exists. FIFOs on most UNIX systems are filesystem persistent, meaning that they exist on the system until they are explicitly removed/deleted or the relevant file system is unmounted (i.e., removed from the system).

You can use the mk nod() system call or the mkfifo() library call to create a FIFO in a program and the mkfifo command to create a file in a shell session. We discuss the command line use of FIFOs in this section. We discuss the use of FIFOs, pipes, and the related system calls and library calls in the chapters on system programming (Chapters 18 through 21). Here is a brief description of the mkfifo command.

# SYNTAX

```
mkfifo [option] file-list
```

+   **Purpose:** Create FIFOs with pathnames given in file-list
+   **Output:** FIFOs for the pathnames given in file-list are created in the relevant directories
+   **Commonly used options/features:**
+   - -m mode Set access permissions for newly created FIFOs to “mode”, the access permissions are specified in “mode” as they are with the chmod command, such as 666, meaning read and write permissions for everyone and execute permission for nobody

In the following session, we use the first command to create a FIFO, called myfifo1, with default permissions based on the current value of umask (see discussion in Chapter 5). We