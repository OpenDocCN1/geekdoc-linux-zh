**Table 4.3** Flags used with tar to create archives.

| Flag | Purpose |
| :--- | :--- |
| `--exclude=file` | Does not include a specific file. Useful when you are archiving directories. |
| `<Tab>-c` | Creates an archive. |
| `-f` | Saves the archive to the file stated in the command. |
| `-M` | Breaks the **tar** archive into multiple volumes. Used to store the archive on multiple media. |
| `-P` | Uses absolute paths instead of relative. Not recommended unless you have a very specific reason. |
| `-v` | Prints file names during the archiving process. |
| `-z` | **gzips** the files before placing them in the archive. |

# ## Examining The Contents Of tar Files

To view the contents of a **tar** archive without unpacking it, use the format **tar -tf name.tar**.

# ## Opening tar Files

To unpack a **tar** file, use the format **tar -xvf name.tar**. Although the **v** is not an essential flag, it is useful for keeping track of progress.

# ## Opening Or Creating Tarballs

A *tarball* is a packaging combination commonly used in the Linux and Unix worlds. You can recognize one of these files by either a *.tar.gz* extension, or a *.tgz* extension. Either way, there are two steps to creating or opening one of these files. To open one of these files, follow the instructions in the section “Opening **gzipped** Files” and then “Opening **tar** Files”. To create a tarball, first create the **tar** archive as discussed in “Creating **tar** Files,” and then **gzip** the archive as discussed in “Creating **gzipped** Files.”

> **TIP:** You can also create a tarball by using the *-z* flag when you create a *tar* archive; for example, **tar -zcvf homearchive.tar /home**. To fully open a tarball, try **tar -zxvf homearchive.tar**.