```
-rw-rw-r-- paol/paol 840 2003-09-01 19:27:59
~fedoratest/fedora_guideline.txt
-rw-rw-r-- paol/paol 1485 2003-09-01 18:14:23 fedoratest/style-sheet.txt
-rw-rw-r-- paol/paol 931 2003-09-01 19:02:00 fedoratest/fedora_TOC.txt
```

Note that because the pathnames do not start with a backslash, they are relative pathnames and will install in your current working directory. If they were absolute pathnames, they would install exactly where the paths state.

# **NOTE**

Two of the oldest and most primitive Unix applications are the dump and restore commands. dump examines files on an ext2 and ext3 file system and determines which files need to be backed up. The backups can span multiple media and levels (dump levels determine the amount of data to be backed up). The dump archives are restored using the restore program. You can use restore across a network and use it to restore full and incremental backups. These bare-metal Unix applications are feature-rich but awkward to use, even for some Unix old-timers; for that reason, we do not cover their use in this chapter. Most users prefer the simpler GUI network backup utilities, such as those you learn about in "Alternative Backup Software," later in this chapter, or prefer to use tar.

# # The GNOME File Roller

The GNOME desktop file archiving graphical application File Roller (file-roller) will view, extract, and create archive files using tar, gzip, bzip, compress, zip, rar, lha, and several other compression formats. Note that File Roller is only a front-end to the command-line utilities that actually provide these compression formats; if they are not installed, File Roller cannot use that format.

# **CAUTION**

File Roller will not complain if you select a compression format that is not supported by installed software until after you attempt to create the archive. Install any needed compression utilities first.

File Roller is well-integrated with the GNOME desktop environment to provide convenient drag-and-drop functionality with the Nautilus file manager. To create a new archive, select Archive, New to open the New Archive dialog box and navigate to the directory where you want the archive to be kept. Type your archive's name in the Selection: /root text box at the bottom of the New Archive dialog box. Use the Archive type drop-down menu to select a compression method. Now, drag the files that you want to be included from Nautilus into the empty space of the File Roller window, and the animated icons will show that files are being included in the new archive. When you are done, a list of files will be shown in the previously blank File Roller window (see Figure 16.1). To save the archive, simply select Archive, Close. Opening an archive is as easy as using the Archive, Open dialog to select the appropriate archive file.