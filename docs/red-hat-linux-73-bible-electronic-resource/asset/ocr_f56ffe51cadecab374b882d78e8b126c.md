# Testing your passwords with Crack

In a previous section, I described the importance of choosing good passwords. If you are the only person who uses your Red Hat Linux box, it is obviously not a big problem to verify the robustness of the passwords used on it. You, after all, are the person who assigned all those passwords.

On a multiuser system, however, the task of ensuring good passwords is more complex. If you have many people with accounts on your Red Hat Linux server, the likelihood that some users will pick weak passwords is almost certain. How can you be certain that your users are not using passwords that are easily cracked? The best approach is to use tools that are similar to the ones that crackers use and try to “break” the passwords on your system. Probably the best tool for this is the apply named Crack utility.

# Obtaining the Crack package

For general information about the Crack software, read the Frequently Asked Questions Web page at www.users.dircon.co.uk/~crypto/download/c50-faq.html. Crack can be downloaded via FTP from the /pub/tools/unix/pwdutils/crack/ directory at ftp.cerias.purdue.edu. At the time of this writing, 5.0 is the current version of Crack. In this case, the file crack5.0.tar.gz is the one to download. If you find a higher version number when you look in the directory, download that newer version instead.

Alternatively, you can download the file Crack_5.0a.tar.gz from the directory /pub/tools/password/Crack/ on the server ftp.cert.dfhn.de.

After you have downloaded the file, extract it using the tar command. From the same directory that contains the downloaded file, type the following command

```
# tar -xzvf crack5.0.tar.gz
```

to uncompress and extract the Crack package. It will create a directory called c50a in the current directory. That directory will contain the Crack program as well as the other files and directories that the Crack package requires.

To use the Crack 5.0a package, follow these steps:

+   1. Using a Web browser, go to the page
+       www.users.dircon.co.uk/~crypto/download/c50-linux-util-
+       makefile.txt and save the page to the file c50a/src/util/Makefile in the
+       directory to which you extracted the Crack package. Your browser should prompt you to
+       replace the existing Makefile.

+   2. Click Yes to overwrite the old Makefile with the version that fixes the compile problem.

+   3. Next, compile the Crack package. Change your current directory to the c50a directory
+       (using the cd command) and then type the following:

```
# ./Crack   -makeonly
```