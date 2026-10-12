distribution. It works much the same as apt, but lacked a GUI tool. The Fedora developers have integrated support for Yum into the graphical Red Hat/Fedora package management tool. You can obtain Yum from the Fedora site as well as from FreshRPMs.net; the home page of Yum is at http://linux.duke.edu/projects/yum/.

Here’s how you install and configure Yum:

+   - Read the HOWTO and Users’ FAQ at the Fedora site: http://fedora.mplug.org/.
+   - Install the Fedora GPG key:
+     
+       ```text
+       # lynx -source http://fedora.mplug.org/FEDORA-GPG-KEY | gpg --import
+       ```
+   - Install the correct version of Yum:
+     
+       ```text
+       # rpm -ivh http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/2/yum/ \
+       yum-2.0.7-3.1.fc.fr.noarch.rpm
+       ```
+   - Review the man page for Yum to familiarize yourself with all available options:
+     
+       ```text
+       # man yum
+       ```

Once Yum is installed, the following commands are useful (remember that the Fedora graphical client is available if you configure it to use Yum repositories):

+   - yum list—A list of all packages available from the repository.
+   - yum list installed—A list of all packages installed on your computer.
+   - yum list updates—A list of all updates available for your computer.
+   - yum install package name—Installs package name.
+   - yum update—Run without a package name, Yum will update all installed packages.
+   - yum remove package name—Removes a package and dependencies.
+   - yum upgrade—Run without a package name, Yum will upgrade all packages and remove any obsoleted packages; yum update will not remove obsoleted packages.

You’ll find either apt or Yum to be useful additions to Fedora Core. We suggest that you use the one from FreshRPMs.net if you want to install some of the multimedia applications described in Chapter 10, “Multimedia Applications.” To learn more about yum, check out Chapter 36, “Advanced Yum.”

# ## Compiling Software from Source

Not all the software you might want to use is available in rpm packages or in the exact form that you desire. Many complicated programs have options that can only be selected at compile time and many smaller, special-purpose applications only exist as source code. Fedora Core provides all the tools necessary for you to compile source code into binary applications. First, we’ll cover building from source rpm files, and then manipulating source rpm files and finally, building from source tarballs.