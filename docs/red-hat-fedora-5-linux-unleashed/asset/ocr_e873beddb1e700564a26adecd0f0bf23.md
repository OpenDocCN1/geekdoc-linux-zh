for your system if you understand shell scripting and regular expressions. It is an excellent choice for file management on servers not running X.

![](bbox=[0.19, 0.16, 0.85, 0.48])

**FIGURE 17.4** The Midnight Commander is a highly versatile file tool. If it does not display properly on your screen, launch it with the `-a` argument to force ASCII mode.

# Copying Files Using scp

The traditional way to copy files from one computer to another is to use `uucp`, the UNIXto-UNIX copy program, or to use one of the `rtools`, `rcp`. The `rtools` are not secure over a public network and are subject to several exploits. It is best not to use them at all because they have been supplanted by more secure tools based on the secure shell, `ssh`.

> **NOTE**
> 
> The file transfer protocol known as FTP can be used to copy files from one computer to another, but this requires that an FTP server be running, and the server is subject to security problems of its own.
> 
> See Chapter 24, “Remote File Serving with FTP,” for more details on FTP.

The `scp` command uses `ssh` for file copying. Useful arguments for this command include

+   - `p`—Preserves modification times, access times, and modes from the original file
+   - `r`—Recursively copies entire directories