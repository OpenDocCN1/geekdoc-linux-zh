source files, and creates the executable files and libraries needed to run XMMS. You'll see a lot of messages scroll by as each file is compiled. These messages show the commands used to compile and link the files.

The `make` command can take 10 to 15 minutes to complete. After `make` is done, you can install the XMMS software with the following command:

```
make install
```

This command also runs GNU `make`, but the `install` argument instructs GNU `make` to perform a specific set of commands from the `Makefile`. These instructions essentially go through all the subdirectories and copy various files to their final locations. For example, the binary executable files `xmms`, `gnomexmms`, `wmxmms`, and `xmms-config` are copied to the `/usr/bin` directory.

Now that you have installed XMMS, try running it from the GNOME or KDE desktop by typing `xmms` in a terminal window or by choosing Main Menu→Sound & Video→Audio Player. XMMS already comes with Red Hat Linux, but now you should get the new version of XMMS (the difference is that the newly built version can play MP3 files without any add-ons). From the XMMS window, press L to get the Load File dialog and select an MP3 file to play. Your PC must have a sound card, and the sound card must be configured correctly for XMMS to work. Figure 4-1 shows a typical view of XMMS playing an MP3 music clip.

Figure 4-1:
You can play MP3 music with the version of XMMS you built from source files.

![](bbox=[0.25, 0.68, 0.5, 0.8])

Here's an overview of the steps you follow to download, unpack, build, and install a typical software package:

+   1. Use a Web browser to download the source code, usually in the form of a `.tar.gz` file, from the anonymous FTP site or Web site.
+   2. Unpack the file with a `tar zxvf filename` command.
+   3. Change the directory to the new subdirectory where the software is unpacked, with a command such as `cd software_dir`.