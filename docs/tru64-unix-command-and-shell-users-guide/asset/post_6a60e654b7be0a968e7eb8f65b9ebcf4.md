
- Dollar sign (`$`)
- Left bracket (`{`)
- Asterisk (`*`)
- Tilde (`~`)
- Vertical bar or pipe symbol (`|`)

You may use a period or dot (`.`) in the middle of a file name, but never at the beginning of the file name unless you want the file to be hidden when doing a simple listing of files. For information about characters with special meanings to your shell, refer to Section 8.2.2 and Section 8.3.2. For information about listing hidden files, see Section 3.1.3.

**Note:** Unlike some operating systems, this operating system distinguishes between uppercase and lowercase letters in file names (that is, it is case sensitive). For example, the following three file names represent three distinct files: `filea`, `Filea`, and `FILEA`.

Use file names that reflect the actual contents of your files. For example, a file name such as `memo.advert` might indicate that the file contains a memo about advertising. On the other hand, file names such as `filea`, `fileb`, or `filec` tell you nothing about the contents of that file.

It is also a good idea to use a consistent pattern to name related files. For example, suppose you have an advertising report that is divided into chapters, with each chapter contained in a separate file. You might name these files in the following way:

```
chap1.advert
chap2.advert
chap3.advert
```

**Note:** Many programs that you invoke use the portion of the file name following the dot (`.`), called the extension, as an indicator of the file's purpose.

The maximum length of a file name depends upon the file system used on your operating system. For example, your file system may allow a maximum file name length of 255 characters (the default), or it may allow a maximum file name length of only 14 characters. Because knowing the maximum file

This information indicates that you are currently working in a directory named `msg` that is located under the `/usr` directory.

The `/usr/msg` notation is known as the **pathname** of your working directory. See Section 2.3.4 for information about pathnames. See the `pwd(1)` reference page for further information on the `pwd` command.

### 2.3.4 The Tree-Structure File System and Pathnames

The files and directories in the file system are arranged hierarchically in a structure that resembles an upside-down tree with the root at the top and the branches at the bottom. This arrangement is called a **tree** structure. You can find more detailed information about the directory structure in the `hier(5)` reference page.

Figure 2–1 shows a typical file system arranged in a tree structure. The names of directories are printed in **bold**, and the names of files are printed in *italics*.

**Figure 2–1: A Typical File System**

![](img/47f3b48f0999ddf70574ce85cbaaf942_44_0.png)

1. At the top of the file system shown in Figure 2–1 (that is, at the root of the inverted tree structure) is a directory called the root directory. The symbol that represents this first major division of the file system is a slash (`/`).
2. At the next level down from the root of the file system are eight directories, each with its own system of subdirectories and files. Figure 2–1, however, shows only the subdirectories under the directory named `usr`. These are the login directories for the users of this system.
3. The third level down the tree structure contains the login directories for two of the system's users, `smith` and `chang`. It is in these directories that `smith` and `chang` begin their work after logging in.
4. The fourth level of the figure shows three directories under the `chang` login directory: `plans`, `report`, and `payroll`.
5. The fifth level of the tree structure contains both files and subdirectories. The `plans` directory contains four files, one for each quarter. The `report` directory contains three files comprising the three parts of a report. Also on the fifth level are two subdirectories, `regular` and `contract`, which further organizes the information in the `payroll` directory.

A higher level directory is frequently called a parent directory. For example, in Figure 2–1, the directories `plans`, `report`, and `payroll` all have `chang` as their parent directory.

A pathname specifies the location of a directory or a file within the file system. For example, when you want to change from working on File A in Directory X to File B in Directory Y, you enter the pathname to File B. The operating system then uses this pathname to search through the file system until it locates File B.

A pathname consists of a sequence of directory names separated by slashes (`/`) that ends with a directory name or a file name. The first element in a pathname specifies where the system is to begin searching, and the final element specifies the target of the search. The following pathname is based on Figure 2–1:

```
/usr/chang/report/part3
```

The first slash (`/`) represents the root directory and indicates the starting place for the search. The remainder of the pathname indicates that the search is to go to the `usr` directory, then to the `chang` directory, next to the `report` directory, and finally to the `part3` file.

Whether you are changing your current directory, sending data to a file, or copying or moving a file from one place in your file system to another, you use pathnames to indicate the objects you want to manipulate.

A pathname that starts with a slash (`/`) (the symbol representing the root directory) is called a full pathname or an absolute pathname. You can also think of a full pathname as the complete name of a file or a directory. Regardless of where you are working in the file system, you can always find a file or a directory by specifying its full pathname.

The file system also lets you use relative pathnames. Relative pathnames do not begin with the `/` that represents the root directory because they are relative to the current directory.

You can specify a relative pathname in one of several ways:

- As the name of a file in the current directory.
- As a pathname that begins with the name of a directory one level below your current directory.
- As a pathname that begins with `..` (dot dot, the relative pathname for the parent directory).
