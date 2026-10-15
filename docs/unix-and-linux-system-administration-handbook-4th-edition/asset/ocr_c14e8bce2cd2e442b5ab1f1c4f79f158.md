Distributions commonly include dummy packages that exist only to claim other packages as prerequisites. apt-get downloads and upgrades prerequisite packages as needed, so the dummy packages make it easy to install or upgrade several packages as a block. For example, installing the gnome-desktop-environment package obtains and installs all the packages necessary to run the GNOME UI.

Once you have set up your /etc/apt/sources.list file (described in detail below) and know the name of a package that you want, the only remaining task is to run apt-get update to refresh apt-get’s cache of package information. After that, just run apt-get install package-name as a privileged user to install the package. The same command updates a package that has already been installed.

Suppose we want to install a new version of the sudo package that fixes a security bug. First, it’s always wise to do an apt-get update:

```
ubuntu$ sudo apt-get update
Get:1 http://http.us.debian.org stable/main Packages [824kB]
Get:2 http://non-us.debian.org stable/non-US/main Release [102B]
...
```

Now we can actually fetch the package. Note that we are using sudo as we fetch the new sudo package—apt-get can even upgrade packages that are in use!

```
ubuntu$ sudo apt-get install sudo
Reading Package Lists... Done
Building Dependency Tree... Done
1 packages upgraded, 0 newly installed, 0 to remove and 191 not upgraded.
Need to get 0B/122kB of archives. After unpacking 131kB will be used.
(Reading database ... 24359 files and directories currently installed.)
Preparing to replace sudo 1.6.1-1 (using .../sudo_1.6.9p10-1ubuntu3.4_i386.deb)
...
Unpacking replacement sudo ...
Setting up sudo (1.6.2p2-2) ...
Installing new version of config file /etc/pam.d/sudo ...
```

# apt-get configuration

Configuring apt-get is straightforward; pretty much everything you need to know can be found in Ubuntu’s community documentation on package management:

help.ubuntu.com/community/AptGet/Howto

The most important apt-get configuration file is /etc/apt/sources.list, which tells apt-get where to get its packages. Each line specifies the following:

+   - A type of package, currently deb or deb-src for Debian-style packages or rpm or rpm-src for RPMs
+   - A URL that points to a file, CD-ROM, HTTP server, or FTP server from which to fetch packages