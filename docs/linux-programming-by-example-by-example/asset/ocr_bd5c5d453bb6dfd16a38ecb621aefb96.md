# ## Using tar and gzip

`tar` and `gzip` were for many years the standard UNIX utilities for creating and distributing source code. For many people, they still are. They have limitations, however, when it comes to maintaining system integrity, particularly because they don't have a built-in facility for managing version control or checking software dependencies. This should not be seen, however, as `tar` or `gzip`'s shortcoming. The assumption behind software distribution using `tar`, `gzip`, and `install` is that the user or system administrator will take care of versioning and dependencies.

# ## tar Usage

`tar`, which stands for *Tape ARChiver*, creates, manages, and extracts multfile archives, known as *tarfiles*, or, more affectionately and idiomatically, *tarballs*. `tar` is the traditional utility used to create archives. `tar` is blessed (or plagned, depending on your perspective) with a bewildering variety of command-line options and switches.

> NOTE
> Long-time UNIX users will notice the absence of the `cpio` command. Why? The Linux idiom is to use `tar` (and `gzip`) to create multiple file archives for distributing software. `cpio`, when it is used at all, is used to create and manage system backups. Indeed, in the seven years I have been using Linux, I have never encountered any software that was packaged using `cpio`. That is not to say it does not happen, of course. I just have not run across it.

This chapter attempts to manage the confusion by focusing on simple, typical usage as related to the creation and management of software distribution. Table 21.1 lists some of `tar`'s command-line options, which subsequent sections discuss in more detail.

Table 21.1: `tar` Command-Line Options

| Option | Description |
| :----- | :---------- |
| c | Creates an archive |
| f *archive_name* | A required argument, f *archive_name* tells tar the name of the tarball with which to work |
| r | Appends files to the archive |
| u | Updates existing files in the archive |
| t | Lists the contents of the archive |
| v | Generates verbose output |
| z | Creates or works with a compressed archive (`gzip` is the default compression utility) |