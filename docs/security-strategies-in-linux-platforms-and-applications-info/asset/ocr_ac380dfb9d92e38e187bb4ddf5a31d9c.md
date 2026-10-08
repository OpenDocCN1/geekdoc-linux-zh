# CHAPTER 14 | Detecting and responding to Security Breaches

+   1. Download and unpack the tarball with the Sleuth Kit files. It's normally available in tar.gz format. Verify the download with the GNU Privacy Guard (GPG) key available from http://www.sleuthkit.org/

+   2. Unpack the sleuthkit-*.gz with the following command. The version number is represented by *; the * character works in the command. The files from the archive should appear in the sleuthkit- directory.

```
$ tar xzf sleuthkit-.tar.gz
```

+   3. Navigate to the sleuthkit-* directory. As noted in the INSTALL .txt file, three additional steps are required to compile and build the required commands.

+   4. Run the ./configure script to configure the packages with locally available libraries.

+   5. Run the make command to build the packages.

+   6. Run the make install command to compile the packages; by default, the commands are written to the /usr/local/bin/

Of course, you'll want to execute the executable files from the /usr/local/bin/ directory to read-only media like CDs or DVDs. Ensure appropriate commands and media libraries are written, you can then mount media on a compromised system and use the commands built by this process. Some of the commands available from the Sleuth Kit are described in Table 14-2. As you can see from the commands, many of them are also well suited to analyze after a system is powered down.

# Master Key Linux

One of the issues with the Sleuth Kit is that it is currently distributed as a tarball. It's still up to you to configure, compile, and copy the commands from the appropriate media. If that seems a lot of trouble, one option is Master Key Linux. It's a live CD with the commands described earlier (and a few more) already set up. All you need is to mount the CD and run the commands from the appropriate subory. Currently, development is led by students at Coventry University (UK), no commercial support is available. But if this is of interest to, the software is available from http://www.masterkeylinux.com/

# Build Your Own Media

It may be best to build your own media. When compiled from source code, you can set up commands on read-only media like CDs or DVDs with all the libraries required to run commands reliably. As noted in article by Mariusz Burdach of Symantec Web site at http://www.symantec.com/connect/articles/forensic-analysis-live-linux-system-pt-1, you may want to include the commands listed in Table 14-3 in that media. Be aware when downloading packages, many of the associated servers do not organize packages by date. So the latest version of a package may be somewhere in the middle of the listing.

![](bbox=[0.95, 0.69, 0.99, 0.81])