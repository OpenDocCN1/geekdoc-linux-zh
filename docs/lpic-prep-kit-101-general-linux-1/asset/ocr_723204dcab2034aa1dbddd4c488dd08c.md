then both the owner of the file and the members of the specified group have the permission to read and write to the file. Everyone else has only the permission to read the file.

# File Access

The r (read) permission means you can see the contents of that file, including opening the file with an application such as vi if it is a text file.

If you do not have the w (write) permission to a file when opening it in vi, the file will be opened as read-only. If you make changes to it, you will have to save the file using a new name.

The write permission means that you can modify the file by changing its contents. However, the write permission does not give you the permission to delete that file.

If you have write permission to a file but do not also have read permission, you will not be able to open that file with a text editor such as vi. Instead, you will get an access denied error message.

The x (execute) permission means you can run that file by typing its name at a command prompt, providing it is a binary file or script. If you try to execute a text file, you will get an error message.

Your effective access permissions to a file are determined by summing the individual permissions that have been granted to you. These are represented by the three positions that are always in the order read, write, and execute. If you do not have a particular permission, it will be represented by a hyphen (-). If the permission has been granted, the appropriate letter will appear in its correct position, as in the following:

```
```text
-rw-rw-r--    1 hadden    hadden    39 Oct 19 18:30 Abill
-rw-rw-r--    1 hadden    hadden    35 Sep  6 19:47 AlphaFilelist
```
```

The permission block r-- means you can read that file but you cannot change or delete it. Nor will you be allowed to execute it if it is a binary or script. The hyphens in the second and third positions indicate that the write permission (second position) and the execute permission (third position) are not granted.

The permission block -w- gives you the permission to change the file, but you can't read the file. For example, if you had only the permission to write to a file called File1, you would not be able to open the file in an editor; however, you could change its attributes by using the touch command. You also could overwrite the file, as in

```
```text
cat file2 > File1
```
```