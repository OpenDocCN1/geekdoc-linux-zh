+   - Directories are organized in a hierarchy, with the **root directory** at the top
+   - The root directory is referred to as /

ii. **Directory and File Names**

+   - Files and directories are organized into a **filesystem**
+   - User can refer to files in directories and sub-directories by separating their names with / , for example:

```
/bin/ls
/usr/dict/words
/home/venky/receipe
```

+   - Paths to files either start from / (absolute) symbol or from some current directory

iii. **File Extensions**

+   - A filename always has an extension, beginning with a dot.
+   - An extension indicates the type of the file.
+   - On Unix and Linux, file extensions are entirely a matter of convention, the operating system itself ignores them.
+   - Only a few specific programs use extensions to identify the type of a file.

**Table 1: Basic File Extensions**

| File Extension | Description |
| :--- | :--- |
| .txt | Refers to text file |
| .gif | Refers to Graphics Interchange Format image |
| .jpg | Refers to Joint Photographic Experts Group image |
| .mp3 | Refers to MPEG-2 Layer 3 audio |
| .gz | Refers to compressed file |
| .tar | Refers to Unix 'tape archive' file |
| .tar.gz, .tgz | Refers to compressed archive file |

iv. **Visiting Directories with cd**

+   - You can change to other directory from the current working directory by using the cd command. For example if you want src to be your current directory, then type the following

```
$ cd /usr/src
```

+   - If you do not give the directory name as an argument, the cd command navigates you to the home directory.

You can use pwd command to find out the current directory. Syntax for finding the current directory is: $ pwd

v. **Filename Completion**

+   - Modern shells provides you one of the most useful features of the Linux command line that is automatic file name completion. You do not have to type the complete file