# 1484

# unzip

-C

Match file names case insensitively. Because some file systems are fully case sensitive (notably those under the UNIX operating system) and because ZIP archives and unzip itself are portable across platforms, the default behavior is to match wild-card and literal file names case sensitively. That is, specifying makefile in the archive, not Makefile or MAKEFILE (and similarly for wild-card specifications). Because this behavior does not match that of many other operating/file systems (for example, OS/2 HPFS, which preserves mixed case but is not sensitive), you can use the -C option to force all file names to match case. In the example above, all three files match makefile (or make*, or similar form). The -C option affects files in both the normal-file list and the excluded-file list (xlist).

-j

Junk paths. Do not recreate the archive's directory structure. Deposit all files in the extraction directory (by default, the current one).

-L

Convert to lower case name originating on an uppercase-only operating system or file system (This was the behavior in releases before 5.11. The new default behavior is identical to the old behavior with the -U option, which is now obsolete and will be removed in a future release.) Depending on the archiver, store files archived under single-case file systems (like V and MS-DOS FAT) as uppercase names. The default behavior can be ugly or inconvenient when extracting to a case-preserving file system as OS/2 HPFS or a case-sensitive one as UNIX. By default, unzip lists and extracts file names exactly as they are (except truncation, conversion of unsupported characters, and so on).

-M

Pipe all output through an internal pager similar to the UNIX less(1) command. At the end of a screen of output, pause with a prompt. You can view the next screen by pressing the Enter (Return) key or the space bar. You can quit unzip with the q key, and on systems, the Enter/Return key. Unlike UNIX unzip does not allow you to search for or edit. Also, unzip doesn't detect if long lines wrap at the edge of the screen, effectively resulting in the printing of two or more lines or that some text scrolls off the top of the screen being viewed. On some systems, the number of available lines on the screen is not detected, in which case unzip assumes the height is 24 lines.

-n

Never overwrite existing files. If a file already exists, skip without prompting. By default, unzip queries before extracting any file that already exists; you can choose to overwrite only the current file, overwrite all files, skip extraction of the current file, skip extraction of all existing files, or rename the current file.

-N

Extract file comments as Amiga file notes. Create file comments with the -c option of zip or with the -N option of zip, which stores file notes as comments (Amiga).