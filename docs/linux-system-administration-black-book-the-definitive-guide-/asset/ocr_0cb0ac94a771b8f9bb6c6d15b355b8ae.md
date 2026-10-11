Add rules that let the traffic into the machine that it needs. For example, if you need to be able to **telnet** from your machine in another part of the office to this one, add a line such as this:

```
in.telnetd:192.168.170.12
```

+   11. When you are finished, press the Esc key, and then type “ZZ” to save and close the file.

> **NOTE:** Do not open too many holes right away. Sometimes, instead of poking your security full of holes, it is better to see what you explicitly need to add.

# # Obtaining And Installing ssh

To get and then install the secure shell software—which must be done on both client and server machines—do the following:

+   1. Go to the URL **www.ssh.org/download.html**.
+   2. Read this Web page. Two different versions of ssh are available, ssh and ssh2. These instructions are for ssh, because it has the less-restrictive version license.
+   3. Click the appropriate mirror site's URL to enter that site's FTP folder.
+   4. Click the newest version of ssh available. At the time of this writing, the version to download was ssh-1.2.27.tar.gz. Do not be fooled by newer-looking versions that start with ssh-2. These files are ssh2.

> **TIP:** You can also use FTP to go directly to one of the mirror sites after you get the URL address from the main ssh Web page.

+   5. Close the Web browser or FTP connection.
+   6. Move the file to your preferred source location (for example, **mv ssh-1.2.27.tar.gz /usr/src**).
+   7. **gunzip** the file (for example, **gunzip ssh-1.2.27.tar.gz**).
+   8. Unpack the file with **tar** (for example, **tar -xvf ssh-1.2.27.tar**).
+   9. Change into the source directory with the **cd** command (for example, **cd ssh-1.2.27**).

> **TIP:** If the newest series 1 version is higher than 1.2.27, see the INSTALL file to make sure that the installation instructions have not changed.