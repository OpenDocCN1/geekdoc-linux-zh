```
Installed-Size: 144
Maintainer: Debian Games Team pkg-games-devel@lists.alioth.debian.org
Architecture: i386
Version: 0.8.1-6
Depends: libc6 (>= 2.7-1), libx11-6, libxext6, libxmu6, libxpm4, libxt6, xav3dg
(>= 1.5+R-1)
Size: 34932
Description: 3D Chess for X11
 3 dimensional chess game for Xl1R6. There are three boards, stacked
 vertically. 96 pieces of which most are the traditional chess pieces with
 just a couple of additions; 26 possible directions in which to move. The
 AI isn't wonderful, but provides a challenging enough game to all but the
 most highly skilled players.
```

Likewise, you could uninstall the 3dchess package using the dpkg -r 3dchess command, as shown here:

```
root@Ubuntu-Desktop:/home/rtracey/Downloads# dpkg -r 3dchess
(Reading database ... 138218 files and directories currently installed.)
Removing 3dchess ...
Processing triggers for man-db ...
Processing triggers for desktop-file-utils ...
root@Ubuntu-Desktop:/home/rtracey/Downloads#
```

Now that you know how to manage packages with dpkg, let's next look at the apt-cache command.

# ## Viewing Package Information with apt-cache

In addition to dpkg, you can also use several apt (Advanced Package Tool) tools to manage packages on a Debian-based system. The first apt tool that you need to be familiar with is apt-cache. This command is comparable to the rpm -q command in that it is used to query package information from the Debian package database (called the *package cache*). Common apt-cache commands are shown in Table 8-5.

| Common apt-cache Command | Description |
| --- | --- |
| apt-cache showpkg *package_name* or apt-cache show *package_name* | Displays information about the package. |
| apt-cache stats | Displays the number of packages installed, dependency information, and other package cache statistics. |
| apt-cache unmet | Reports any missing dependencies in the package cache. |
| apt-cache depends *package_name* | Displays all of the package's dependencies. |
| apt-cache pkgnames *package_name* | Checks to see whether a package is installed on the system or not. Leaving out the package name displays a list of all of the packages installed on the system. |
| apt-cache search *keyword* | Searches package descriptions for the specified keyword. |

Table 8-5 Common apt-cache Commands