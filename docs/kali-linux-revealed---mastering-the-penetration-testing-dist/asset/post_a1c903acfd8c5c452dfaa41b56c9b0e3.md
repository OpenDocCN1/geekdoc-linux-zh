
easily be added to a file in /etc/apt/apt.conf/. The name of this file is somewhat arbitrary, but a common convention is to use local or 99local:

```
$ cat /etc/apt/apt.conf/99local
Dpkg::Options {
  "--force-overwrite";
}
```

There are many other configuration options and we certainly can't cover them all, but one we will touch on network connectivity. For example, if you can only access the web through a proxy, a line like Acquire::proxy="http://yourproxy:3128". For an FTP proxy, use Acquire::ftp:proxy="ftp://yourproxy".

To discover more configuration options, read the apt.conf (5) manual page with the man apt.conf command (for details on manual pages, section 6.1.1, "Manual Pages" [page 124]).

## 8.3.2. Managing Package Priorities

One of the most important aspects in the configuration of APT is the management of the priorities with each package source. For instance, you might want to extend your Kali Rolling system with one or two newer packages from Debian Stable or Debian Experimental. It is possible to assign a priority to each available package (the same package can have several priorities depending on its version or the distribution providing it). These priorities influence APT behavior: for each package, it will always select the version with the highest priority (except if this version is older than the one installed and its priority is less than 1000).

APT defines default priorities. Each installed package version has a priority of 100. A non-installed version has a priority of 500 by default but it can jump to 990 if it is the part of the target release (defined with the -t command-line option or APT::Default-Release configuration direction).

You can modify priorities by adding entries in the /etc/apt/preferences file with the names of the affected packages, their version, origin and their new priority.

APT will never install an older version of a package (that is, a package whose version number is lower than the one of the currently installed package) except when its priority is higher than 1000. APT will always install the highest priority package that follows this constraint. If two packages have the same priority, APT installs the newest one (whose version number is the highest). If two packages of same version have the same priority but different in their content, APT installs the version that is newest without the increment of the revision number, which is usually required).

In more concrete terms, a package whose priority is less than 0 will never be installed. A package with a priority ranging between 0 and 100 will only be installed if no other version of the package is already installed. With a priority between 100 and 500, the package will only be installed if is no newer version installed or available in another distribution. A package of priority between 501 and 990 will only be installed if there is no newer version installed or available in the target distribution. With a priority between 990 and 1000, the package will be installed except if the installed version is newer. A priority greater than 1000 will always lead to the installation of the package even if it forces APT to downgrade to an older version.

When apt /etc/apt/preferences, it first takes account the most specific entries (often specifying the concerned package), the more generic ones (including all packages of a distribution). If several generic entries exist, the first it is used. The available selection criteria include the package name and the source providing it. Every package source is identified by the information contained in a Release file that APT downloads together with the Packages files. These files specify the origin, unless "Kali" for the packages from Kali's official mirrors or "Debian" for the packages from Debian's official mirrors, the origin can also be a person or an organization's name for third-party repositories. The Release file also provides the name of the distribution together with its version. Let's have a look at its syntax through some realistic cases of this mechanism.

| Priority | Description |
| :--- | :--- |
| 1 | The corresponding packages will almost never be installed because their default APT priority is 1. This is of course a specific case, designed to keep users from installing bleeding packages by mistake. The packages can only be installed by typing apt package=Kali-bleeding-edge assuming that you are aware of the risks and potential boundaries of life on the edge. It is still possible (though not recommended) to treat packages of kali-bleeding-edge/experimental like those of other distributions by giving them a priority of 500. |
| Priority of Kali-Bleeding-edge and Debian | Package: *<br>Pin: release=kali-bleeding-edge<br>Pin-Priority: 500 |
| Let's suppose that you only want to use packages from Kali and that you only want Debian installed when explicitly requested. You could write the following entries in /etc/apt/preferences (or in any file /etc/apt/preferences.d):<br>Package: *<br>Pin: release o=Kali<br>Pin-Priority: 900<br><br>Package: *<br>Pin: release o=Debian<br>Pin-Priority: -10 |
| In the last two examples, you have seen a=kali-bleeding-edge, which defines the name of the distribution and o=Kali and o=Debian, which limit the scope to packages whose origin are Kali and Debian, respectively. Let's now assume that you have a server with several local programs depending on version 5.22 of Perl and you want to ensure that upgrades will not install version of it. You could use this entry:<br>Package: perl<br>Pin: version=5.22<br>Pin-Priority: 1001 |
| Adding Comments in /etc/apt/preferences | There is no official syntax for comments in /etc/apt/preferences, but some textual descriptions can be provided by prepending one or more Explanation fields into each entry:<br>Explanation: The package xserver-xorg-video-intel provided in experimental can be used safely<br>Package: xserver-xorg-video-intel<br>Pin: release=experimental<br>Pin-Priority: 500 |

## 8.3.3. Working with Several Distributions

Given that apt is such a marvelous tool, you will likely like to dive in and start experimenting with packages from other distributions. For example, after installing a Kali Rolling system, you might try to install a software package available in Kali Dev, Debian Unstable, or Debian Experimental without diverging too much from the system's state.

Even if you occasionally encounter problems while mixing packages from different distributions, apt manages well and limits risks very effectively (provided that the package dependencies are correct). First, list all distributions used in /etc/apt/sources.list and define your reference distribution with the APT::Default-Release parameter (section 8.2.3, Upgrading Kali Linux [page 179]).

Let's suppose that Kali Rolling is your reference distribution that Kali Dev and Debian Unstable are also listed in your sources list. In this case, you can use apt install package/unstable to install a package from Debian Unstable. If the installation fails due to some unsatisfiable dependencies, let it solve those dependencies within Kali

In this situation, upgrades (upgrade and full-upgrade) are done within Kali Rolling except for packages already upgraded to another distribution: these follow updates available in the other distributions. We will explain this behavior with the help of the default priorities set by apt below. Do not hesitate to use apt-cache policy or see "Using apt-cache policy" [page 199] to verify the given priorities.

Everything relies on the fact that apt only considers packages of higher or equal value than the installed package (assuming that /etc/apt/preferences has not been used to force priorities higher than 1000 for some packages).

| Using apt-cache policy | To gain a better understanding of the mechanism of priority, do not hesitate to use apt-cache policy to display the default priority associated with each package source. You can also use apt-cache policy to display the priorities of all available versions of a given package. |

Let's assume that you have installed version 1 of a package from Kali Rolling and that version 2 are available respectively in Kali Dev and Debian Unstable. The installed version has a priority of 100 but the version available in Kali Rolling (the very same) has a priority of 990 (because it is part of the target release). Packages in Kali Dev and Debian Unstable have a priority of 500 (the default priority of a non-installed version). The winner is version 1 with a priority of 990. The package stays in Kali Rolling.

Let's take the example of another package whose version 2 has been installed from Kali Dev. Version 1 is available in Kali Rolling and version 3 in Debian Unstable. Version 1 (of priority 990—lower than 1000) is discarded because it is lower than the installed version. This only leaves version 2 and 3, both of priority 500. Faced with this alternative, apt selects the newest version, the one from Debian Unstable. If you don't want a package installed from Kali Dev to migrate to Debian Unstable, you have to assign a priority lower than 500 (490 for example) to packages coming from Debian Unstable. You can modify /etc/apt/preferences for this effect:

```
Package: *
Pin: release=unstable
Pin-Priority: 490
```

## 8.3.4. Tracking Automatically Installed Packages

One of the essential functionalities of apt is the tracking of packages installed only through dependencies. These packages are called automatic and often include libraries.

With this information, when packages are removed, the package managers can compute a list of automatic packages that are no longer needed (because there are no manually installed packages depending on them). The command apt autoremove will get rid of these packages. Appetite does
