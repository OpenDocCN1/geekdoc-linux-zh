audio and video typically rely on other software packages for decoding different kinds of content. To handle software dependency issues (along with the fact that it includes many other valuable features), Fedora has based its packaging tools on the yum facility.

# Downloading and installing applications with yum

The yum command lets you install and update selected software packages in RPM format from software repositories on the Web. Once you know the software package that you want, yum is probably the best way to download and install that package. There are also features in yum for listing and managing RPMs after they are installed.

Yum is the foundation for software updates in Fedora. Besides the yum command, the PackageKit facility and even the Fedora installer itself (anaconda) now use yum as the underlying mechanism for getting and updating software in Fedora.

The yum package is included on the Fedora DVD that comes with this book. To use yum to install RPM software packages, follow these basic steps:

+   1.  **Determine the software package you want.** Yum is delivered with the current Fedora repository already configured. Use yum or PackageKit search tools (described later) to find packages you want. Or add more repositories for yum to search to your `/etc/yum.conf` file or `/etc/yum.repos.d/` directory (also described later). (Many software repositories offer RPM packages that automatically configure entries in the `yum.repos.d` directory to point to those repositories.)
+   
+   2.  **Configure yum.** You have the option to configure the `/etc/yum.conf` file to set options that relate to how you use your yum repositories, as described in the next section. Then add any repositories, in addition to the Fedora repository, that you want to get packages from.
+   
+   3.  **Run yum.** The yum command can be used to download and install any package from the yum repository, including any packages the one you want depends on.

> CAUTION: The Fedora Project has gone to great lengths to ensure that software it provides is of good quality and unimpaired by legitimate patent claims. When you download packages that are not official packages for Fedora, you are on your own to check the quality and legality of that software. Some users refuse to configure yum to access non-official repositories. In addition, the yum command informs you which repository it intends to download packages and lets you choose whether to go forward with downloading and installing.

In addition to downloading and installing new software packages, yum can also be used to check for available updates and list various kinds of information about available packages.

# Configuring yum (/etc/yum.conf)

The /etc/yum.conf file already comes preconfigured to include options that affect how you download and use RPM packages with yum. All necessary, basic repository listings are