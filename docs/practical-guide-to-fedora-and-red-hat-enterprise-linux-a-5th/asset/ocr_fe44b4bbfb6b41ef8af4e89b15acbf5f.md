# HARD LINKS

A hard link to a file appears as another file. If the file appears in the same directory as the linked-to file, the links must have different filenames because two files in the same directory cannot have the same name. You can create a hard link to a file only from within the filesystem that holds the file.

# ln: CREATES A HARD LINK

The ln (link) utility (without the -s or --symlink option) creates a hard link to an existing file using the following syntax:

```
ln existing-file new-link
```

The next command makes the link shown in Figure 6-14 by creating a new link named /home/alex/letter to an existing file named draft in Jenny’s home directory:

```
$ pwd
/home/jenny
$ ln draft /home/alex/letter
```

The new link appears in the /home/alex directory with the filename letter. In practice, Alex may need to change the directory and file permissions so that Jenny will be able to access the file. Even though /home/alex/letter appears in Alex’s directory, Jenny is the owner of the file because she created it.

The ln utility creates an additional pointer to an existing file but it does not make another copy of the file. Because there is only one file, the file status information—such as access permissions, owner, and the time the file was last modified—is the same for all links; only the filenames differ. When Jenny modifies /home/jenny/draft, for example, Alex sees the changes in /home/alex/letter.

![](bbox=[0.34, 0.65, 0.75, 0.89])

Figure 6-14  Two links to the same file: /home/alex/letter and /home/jenny/draft