If you installed Linux on the machine yourself, you should have a boot disk from the installation process. Otherwise whoever did the installation for you likely has given you or sent with your system a boot disk. If you don't have one, see the chapter on Linux boot and shutdown for instructions on making a boot disk.

When you upgrade your entire distribution, you will definitely want to back up at least the / (root) and /usr file systems, and probably your whole machine, as well. It doesn't happen often, but it is possible for a critical library or program not to upgrade properly, crippling your machine. You should probably back up your /etc directory and /home directories.

The upgrading process for RedHat Linux and distributions based on it is usually an across-the-board upgrading of all the RPM files. Thus it is possible to perform essentially the same operations gradually by FTPing the RPM files from their FTP sites or a mirror as desired or needed.

# 22.4 Summary

As Linux has moved further into the commercial and public eye, the need for easy upgrading has grown and been answered. Most distributions allow you to upgrade easily from previous versions with only an hour or two of down time.

With package management tools, it is also straightforward to upgrade specific programs or groups of programs. Of course it is always possible to simply obtain the source code and upgrade various programs "manually.",