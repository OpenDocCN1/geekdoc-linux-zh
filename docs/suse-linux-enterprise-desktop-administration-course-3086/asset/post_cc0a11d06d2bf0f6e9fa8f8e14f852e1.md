
6. Verify that the directory was removed by entering
```
ls
```
7. Remove the `~/my_dir/login` file by entering
```
rm ~/my_dir/login
```
8. You see a message warning you that the file is write-protected. Confirm the warning by entering `y`.
9. Verify that the file has been removed by entering
```
ls ~/my_dir/login
```
10. Remove all files with names that begin with “a” in the `/home/geeko/my_dir/` directory by entering
```
rm -i ~/my_dir/a*
```
11. Confirm every warning by entering `y`.
12. Remove the `/home/geeko/my_dir/` directory including its content by entering
```
rm -r ~/my_dir
```
13. Confirm every warning by entering `y`.
14. Verify that the directory has been removed by entering
```
ls ~/my_dir
```
15. Close the terminal window.

## Link Files

File system formats in Linux keep data and administration information separate. How data is organized differs from one file system format to another.

Each file is described by an inode (index node or information node). To see the inode number, you can enter `ls -i`.

Each inode is 128 bytes and contains all the information about this file apart from the filename. This includes information such as details of the owner, access permissions, the size, various time details (time of modification, time of access, time of modification of the inode), and the links to the data blocks of this file.

The ln command creates a link. A link is a reference to a file. Through a link, you can access a file from anywhere in the file system using different names for the file. The file itself exists only once on the system, but it can be found under different names.

Linux recognizes two kinds of links:

- Hard links
- Symbolic links

You create a *hard link* by using the `ln` command, which points to the inode of an already existing file. Thereafter, the file can be accessed under both names—that of the file and that of the link, and you can no longer discern which name existed first or how the original file and the link differ.

The following is an example of using the ln command:

```text
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
geeko@da10:~/sell > ln old new
geeko@da10:~/sell > ls -li
total 8
88658 -rw-r--r-- 2 geeko users 82 2004-04-06 14:21 old
88658 -rw-r--r-- 2 geeko users 82 2004-04-06 14:21 new
geeko@da10:~/sell >
```

Hard links can only be used when both the file and the link are in the same file system (on the same partition), because inode numbers are only unique within the same file system.

You can create a symbolic link with the ln command and the option -s. A symbolic link is assigned its own inode—the link refers to a file, so a distinction can always be made between the link and the actual file.

The following is an example of creating a symbolic link:

```text
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
geeko@da10:~/sell > ln -s old new
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
88657 lrwxrwxrwx 1 geeko users 3 2004-04-06 14:27 new -> old
geeko@da10:~/sell >
```

With symbolic links, the limits of the file system can be overcome, because the name of the object is shown, not the object itself. The disadvantage is that a symbolic link can point to a non-existing object if the object and its corresponding name no longer exist.

If you erase the file old in the above example, new will point to a nonexistent file. You cannot see in the ls output that the link is broken:

```text
geeko@da10:~/sell > rm old
geeko@da10:~/sell > ls -li
total 0
88657 lrwxrwxrwx 1 geeko users 3 2004-04-06 14:27 new -> old
geeko@da10:~/sell >
```

An advantage of symbolic links is that you can create links to directories.

![](img/9129877170834ca9d5fdac5319bf5f12_235_0.png)

## Exercise 7-5: Link Files

In this exercise, create a symbolic link to the ~/my_file file and a hard link to the ~/my_file1 file with the ln command.

## Detailed Steps to Complete This Exercise

To link a file, do the following:

1. Open a terminal window.
2. To create a symbolic link to the my_file file in your home directory, enter
```bash
ln -s ~/my_file softlink
```
3. To create a hard link to the my_file1 file in your home directory, enter
```bash
ln ~/my_file1 hardlink
```
4. Display the links by entering
```bash
ls -l
```
Notice that the symbolic link identifies the file it is linked to, and that the link counter (the number listed between the permissions and the owner of the file) is 2 for the my_file1 files and hard link.
5. Close the terminal window.

## Objective 6—Find Files on Linux

In this objective, you learn how to find files and programs.

If the name of the file is not completely known, you can use the two wildcards “?” (for any character) and “*” (for none, one, or several characters).

Suppose the following files exist:

- File
- file
- File1
- File1a
- File1b
- File2
- File2a
- MyFile

Table 7-18 shows the results of three different search strings.

| Search String | Files Found |
|---|---|
| `File?` | File1<br>File2 |
| `File*` | File<br>File1<br>File1a<br>File1b<br>File2<br>File2a |
| `?ile*` | File<br>file<br>File1<br>File1a<br>File1b<br>File2<br>File2a |

Table 7-18

The following tools are introduced:

- Graphical Search Tools
- find
- which
- type

## Graphical Search Tools

Sometimes you need to find a file so you can edit it, but you do not know exactly where it is located in the file system. You might know the name of this file or only a part of the name.

At another time, you might need a list of all files that have been modified in the last two days or that exceed a certain size.

If you enter search in the More Application search bar, two applications are found—the Desktop Search Tool (Search) and the GNOME Search Tool (Search for Files).

![](img/9129877170834ca9d5fdac5319bf5f12_236_0.png)

- *Search (Search)*—When you enter a search term into the Desktop Search Tool, a list of documents that contain the search term appears as soon as you stop typing. The results include different kinds of files on your desktop, from OpenOffice.org files, to PDFs, to Web sites visited. See Figure 7-3.

![](img/9129877170834ca9d5fdac5319bf5f12_237_0.png)

**Figure 7-3**

The Desktop Search Tool can be configured by selecting Search > Preferences. The Search tab allows you to configure when the indexing takes place. See Figure 7-4.

![](img/9129877170834ca9d5fdac5319bf5f12_238_0.png)

The Indexing tab allows you to configure what is included in or excluded from the search index. See Figure 7-5.

![](img/9129877170834ca9d5fdac5319bf5f12_239_0.png)

**Figure 7-5**

- *Search for Files (GNOME Search Tool)—*This tool allows you to search for information such as file size, date, or file owner.

When you select the GNOME Search Tool from the application browser, the dialog shown in Figure 7-6 appears.

In the Name Contains field, enter a part of the filename you want to find. Select the directory you want to search from the Look in folder drop-down list. Select Find to start the search process. All matching files and directories are shown in the lower window with details of their locations.

Further settings can be made when you open the menu under **Select more options**. Select a search rule from the **Available options** drop-down list. See Figure 7-7.

When you select **Add**, a new text field is added allowing you to enter the information the option needs. To remove a search rule, select the **Remove** button next to the rule.

![](img/9129877170834ca9d5fdac5319bf5f12_240_0.png)

Figure 7-6

![](img/9129877170834ca9d5fdac5319bf5f12_240_1.png)

Figure 7-7
