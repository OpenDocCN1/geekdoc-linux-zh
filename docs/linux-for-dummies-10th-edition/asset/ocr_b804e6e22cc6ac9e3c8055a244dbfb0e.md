When you find a program you want to download, follow these steps:

+   1. **From the program's web page, click the Download link.**
+   2. **Locate and download the most specific version matching your distribution.**
+   You may be offered, say, Windows, UNIX, and Linux options. You would choose Linux in that case. If offered Linux amd64 versus Linux x86, choose amd64 unless you're using Linux on an older 32-bit workstation. If you're offered an RPM or a tarball (see the beginning of this chapter for more information on these), choose an RPM.
+   3. **After you have the program downloaded, install it as follows:**
+   * If it's an RPM or DEB package, open your file manager and double-click the download to install it. You can also install it from a command line (see Chapter 7 for how to open a command line terminal). When you have the terminal window open, type su and press Enter. You're asked for your root password. Enter it, press Enter, and use the filesystem navigation commands in Chapter 7 to go to where you saved the RPM file, and then type `rpm -Uvh filename`. This command installs or updates the program as needed.
+   * If it's a tarball, open your file manager. Double-click the file to open it and look at its contents. There should be a file in there called README or INSTALL. This file contains instructions on what you need to do, and there may be more instructions available on the website itself. Working with tarballs just requires practice; it gets easier over time, so extract the file and get to it!

# Upgrading Your OS

Typically, Ubuntu and openSUSE users upgrade by downloading the new version of the distribution, starting the installation, and selecting Upgrade rather than a new install. By selecting the Upgrade option, you should be able to keep your personal data files and only upgrade the OS files. If you perform a new install, all your existing data will be lost. However, even with the Upgrade option, as with any major change to a system, it's always best to have a backup copy of your important files “just in case.”

![](bbox=[0.16, 0.85, 0.22, 0.91])

Many Linux distributions allow you to create a separate partition for the /home directory. That way you can leave it untouched when upgrading to a new version of the operating system.