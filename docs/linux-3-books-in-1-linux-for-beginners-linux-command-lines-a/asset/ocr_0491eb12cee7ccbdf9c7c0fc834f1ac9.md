mv command has an alternate function as well. If you are using the mv command within the same directory, it will merely perform a rename operation on the source file. If you are specifying the destination as a different directory, the source file will be moved under the destination directory.

The move operation from one directory to another may take more time if the file size is huge.

```
[student@desktop ~]$ ls

Hello.txt

[student@desktop ~]$ mv Hello.txt Bye.txt

[student@desktop ~]$ ls

Bye.txt
```

The mv operation is taking place within the same directory. The file is just renamed from Hello.txt to Bye.txt

```
[student@desktop ~]$ ls

Hello.txt

[student@desktop ~]$ mv Hello.txt Documents

[student@desktop ~]$ ls Documents

Hello.txt
```

The mv operation is not taking place within the same directory. The file is moved from Hello.txt to under the Documents directory.

# Deleting Files and Directories

The **rm** command is used to delete files and directories in Linux. Combine is with **-r** , and it will delete everything recursively in the specified path.

Note that Linux does not have a concept like Recycle Bin in Windows. So when you delete something in Linux, it is deleted permanently. There is no way of restoring it again.