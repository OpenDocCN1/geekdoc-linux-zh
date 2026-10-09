# optional

# # HARD LINKS

A hard link to a file appears as another file. If the file appears in the same directory as the linked-to file, the links must have different filenames because two files in the same directory cannot have the same name. You can create a hard link to a file only from within the filesystem that holds the file.

# ## ln: CREATES A HARD LINK

The ln (link) utility (without the -s or — symbolic option) creates a hard link to an existing file using the following syntax:

```
```
ln existing-file new-link
```
```

The next command shows Zach making the link shown in Figure 6-14 by creating a new link named /home/max/letter to an existing file named draft in Zach's home directory:

```
```
$ pwd
/home/zach
$ ln draft /home/max/letter
```
```

The new link appears in the /home/max directory with the filename letter. In practice, Max may need to change directory permissions so Zach will be able to create the link. Even though /home/max/letter appears in Max's directory, Zach is the owner of the file because he created it.

The ln utility creates an additional pointer to an existing file but it does not make another copy of the file. Because there is only one file, the file status information—such as access permissions, owner, and the time the file was last modified—is the same for all links; only the filenames differ. When Zach modifies /home/zach/draft, for example, Max sees the changes in /home/max/letter.

![](bbox=[0.16, 0.65, 0.84, 0.93])