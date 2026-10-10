**TABLE 3.1 The ls command's commonly used options**

| Short | Long | Description |
|:------|:-----|:------------|
| -a    | --all | Display all file and subdirectory names, including hidden files' names. |
| -d    | --directory | Show a directory's own metadata instead of its contents. |
| -F    | --classify | Classify each file's type using an indicator code (*,/,=>,@, or |). |
| -i    | --inode | Display all file and subdirectory names along with their associated index number. |
| -l    | N/A | Display file and subdirectory metadata, which includes file type, file access permissions, hard link count, file owner, file's group, modification date and time, and filename. |
| -R    | N/A | Show a directory's contents, and for any subdirectory within the original directory tree, consecutively show their contents as well (recursively). |

# **Listing 3.2: Exploring the ls -lh command**

```
```
$ pwd
/home/Christine/Answers
$
$ ls -l
total 32
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 29000 Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Universee
$
$ ls -lh
total 32K
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 30K Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine  6 Aug 19 17:34 Universee
$
```
```

Be aware that some distributions include, by default, an *alias* for the `ls -l` command. It is `ll` (two lowercase $L$ characters) and is demonstrated on a CentOS distribution in Listing 3.3. An alias at the Linux command line is simply a short command that represents a longer one.