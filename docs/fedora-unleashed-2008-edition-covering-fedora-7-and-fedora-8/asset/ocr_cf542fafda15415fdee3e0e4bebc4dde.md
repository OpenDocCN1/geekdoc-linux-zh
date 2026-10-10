by accessing the database and having their applications display information about the music CD, including the artist and song title, the CD's track list, and so on. The database server at cddb .org, or, when contacted by the appropriate software, identifies the appropriate CD and sends the information to be displayed locally. Many CD player applications provide this functionality. The service is interactive: If you have a CD that is not in the CDDB database, the website tells you how you can add the information to the database.

![](bbox=[0.08, 0.23, 0.92, 0.58])

**FIGURE 7.13**  Use GnomeBaker to back up your CD or photo collection.

# ## Creating CDs from the Command Line

In Linux, creating a CD at the command line is a two-step process. You first create the `iso9660`-formatted image, and you then burn or write the image onto the CD. The `iso9660`, as you will learn in Chapter 35, “Managing the File System,” is the default file system for CD-ROMs.

Use the `mkisofs` command to create the ISO image. The `mkisofs` command has many options (see the man page for a full listing), but use the following for quick burns:

```
$ mkisofs -r -v -J -o /tmp/our_special_cd.iso /source_directory
```