Like gzip, gunzip takes as an argument the name of the file or files to work on. It expands the specified files, writing the output to new files without the `.gz` extensions, and then deletes the compressed files.

+   To expand the file `war-and-peace.gz`, type:

```
$ gunzip war-and-peace.gz RET
```

This command expands the file `war-and-peace.gz` and puts it in a new file called `war-and-peace`; gunzip then deletes the compressed file, `war-and-peace.gz`.

NOTE: You can view a compressed text file without uncompressing it by using zless. This is useful when you want to view a compressed file but do not want to write changes to it. (For more information about zless, see section Perusing Text).

# 9.6 File Archives

An archive is a single file that contains a collection of other files, and often directories. Archives are usually used to transfer or make a backup copy of a collection of files and directories—this way, you can work with only one file instead of many. This single file can be easily compressed as explained in the previous section, and the files in the archive retain the structure and permissions of the original files.

Use the tar tool to create, list, and extract files from archives. Archives made with tar are sometimes called "tar files," "tar archives," or—because all the archived files are rolled into one—"tarballs."

The following recipes show how to use tar to create an archive, list the contents of an archive, and extract the files from an archive. Two common options used with all three of these operations are `-f` and `-v`: to specify the name of the archive file, use `-f` followed by the file name; use the `-v` ("verbose") option to have tar output the names of files as they are processed. While the `-v` option is not necessary, it lets you observe the progress of your tar operation.

NOTE: The name of this tool comes from "tape archive," because it was originally made to write the archives directly to a magnetic tape device. It is still used for this purpose, but today, archives are almost always saved to a file on disk.

See Info file `tar.info`, node `Top`, for more information about managing archives with tar.

+   9.6.1 Creating a File Archive
+   Creating an archive of files.
+   9.6.2 Listing the Contents of an Archive
+   Listing the contents of an archive.
+   9.6.3 Extracting Files from an Archive
+   Extracting the files from an archive.