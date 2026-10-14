| Field | Meaning |
|---|---|
| -rw-r--r-- | Access rights to the file. The first character indicates the type of file. Among the different types, a leading dash means a regular file, while a d indicates a directory. The next three characters are the access rights for the file’s owner, the next three are for members of the file’s group, and the final three are for everyone else. Chapter 9 discusses the full meaning of this in more detail. |
| 1 | File’s number of hard links. See “Symbolic Links” on page 21 and “Hard Links” on page 22. |
| root | The username of the file’s owner. |
| root | The name of the group that owns the file. |
| 32059 | Size of the file in bytes. |
| 2017-04-03 11:05 | Date and time of the file’s last modification. |
| oo-cd-cover.odf | Name of the file. |

# Determining a File’s Type with file

As we explore the system, it will be useful to know what files contain. To do this, we will use the file command to determine a file’s type. As we discussed earlier, filenames in Linux are not required to reflect a file’s contents. While a filename like picture.jpg would normally be expected to contain a JPEG-compressed image, it is not required to in Linux. We can invoke the file command this way:

```
file filename
```

When invoked, the file command will print a brief description of the file’s contents. For example: