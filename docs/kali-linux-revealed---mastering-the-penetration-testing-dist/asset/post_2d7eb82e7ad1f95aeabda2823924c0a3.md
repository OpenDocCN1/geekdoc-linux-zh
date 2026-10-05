
## 8.2.1. Initializing APT

APT is a vast project and tool set, whose original plans included a graphical interface. From a client perspective, it is centered around the command-line tool apt-get as well as apt, which was later developed to operate graphical alternatives by third parties, including synaptic and aptitude, which we will discuss later. We tend to prefer apt, which we use in the examples that follow. We will, however, detail some of the major syntax differences between tools, as arise.

When working with APT, you should first download the list of currently available packages with apt update. Depending on the speed of your connection, this can take some time because various packages' list, sources' list and translation files have grown in size alongside Debian development. Of course, CD/DVD installation sets install much more quickly, because they are local to your machine.

## 8.2.2. Installing Packages

Thanks to the thoughtful design of the Debian package system, you can install packages, with or without your dependencies, fairly easily. Let's take a look at package installation with dpkg and apt.

### Installing Packages with dpkg

dpkg is the core tool that you will use (either or indirectly through APT) when you need to install a package. It is also a go-to if you are operating offline, since it doesn't require an Internet connection. Remember, dpkg will not install any dependencies that the package might require. To install a package with dpkg, simply provide the -i or --install option and the path to the .deb. This implies that you have downloaded (or obtained in some other way) the .deb file of the package to install.

```
# dpkg -i man-db_2.7.0.2-5_amd64.deb
(Reading database ... 86425 files and directories currently installed)
Preparing to unpack man-db_2.7.0.2-5_amd64.deb ...
Unpacking man-db (2.7.0.2-5) over (2.7.0.2-4) ...
Setting up man-db (2.7.0.2-5) ...
Updating database of manual pages ...
Processing triggers for mime-support (3.58) ...
```

We can see the different steps performed by dpkg and see at what point any error may have occurred. The -i or --install option performs two steps automatically: it unpacks the package and runs the configuration scripts. You can perform these two steps independently (as apt does behind the scenes) with the --unpack and --configure options, respectively:

```
# dpkg --unpack man-db-2.7.0.2-amd64.deb
(Reading database ... 86425 files and directories installed.)
Preparing to unpack man-db-2.7.0.2-amd64.deb ...
Unpacking man-db (2.7.0-2) over (2.7.0-5) ...
Processing triggers for mime-support (3.58)
# dpkg --configure man-db
Setting up man-db (2.7.0-2) ...
Updating database of manual pages ...
```

Note that the "Processing triggers" line refer to code that is automatically executed whenever a package adds, removes or modifies files in monitored directories. For instance, the mime-support package monitors /usr/lib/mime/packages and executes the update-mime command whenever something changes in that directory (/usr/lib/mime/packages/man-db in the specific case of man-db).

Sometimes dpkg will fail to install a package and return an error. However, you can order dpkg to ignore this and only issue a warning with various --force- options. Using the dpkg --force help will display you a list of these options. For example, you can use dpkg to forcibly install zsh:

```
# dpkg -i --overwrite zsh_5.2-5+b1_amd64.deb
```

A frequent error, when you are bound to encounter sooner or later, a file collision: When a package contains a file that is already installed by another package, dpkg will refuse to install it. The following types of messages will then appear:

- - Unpacking libgdm from .../libgdm3.8.3-2_amd64.deb ...
- dpkg: error processing /var/cache/apt/archives/libgdm3.8.3-2_amd64.deb (--unpack):
- trying to overwrite /usr/bin/gdmlexiserver/, which is also in package gdm3
- 3.4.1-9

In this case, if you are replacing this file is not a significant risk to the stability of your system (which is usually the case), you can use --force-overwrite to overwrite the file.

While there are many --force-* options, only --force-overwrite is likely to be used regularly. These options exist for exceptional situations, and it is better to leave them alone as much as possible in order to respect the rules imposed by the packaging mechanism. Do not forget, these rules ensure the consistency and stability of your system.

### Installing Packages with APT

Although APT is much more advanced than dpkg and does a lot behind the scenes, you will find that interacting with packages is quite simple. You can add a package to the system with simple apt install package. APT will automatically install the necessary dependencies:

```
# apt install kali-linux-gpu
Reading lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
oclgaussrack oclhashcat
The following NEW packages will be installed:
kali-linux-gpu oclgaussrack oclhashcat
0 upgraded, 3 newly installed, 0 to remove and 416 not upgraded.
Need to get 2,294 KB of archives.
After this operation, 51.5 MB of additional disk space will be used.
Do you want to continue? [Y/n]
Get://archive-2.kali.org/kali-rolling/non-free amd64 oclhashcat amd64 2.01+
- git201600114-0kali2 [2,451 kb]
- kali2 [37.2 kb]
Get://archive-2.kali.org/kali-rolling/main amd64 oclgaussrack amd64 1.3-1
Get://archive-2.kali.org/kali-rolling/main amd64 kali-linux-gpu amd64
- 2016.3.2 [6,412 kb]
Fetched 2,294 KB in 0s (3,060 kB/s)
Selecting previously unselected package oclhashcat.
(Reading database ... 317084 files and directories currently installed)
Preparing to unpack .../-oclhashcat-0.1+git201600114-0kali2_amd64.deb ...
Unpacking oclhashcat (0.1+git201600114-0kali2) =
Selecting previously unselected package oclgaussrack.
Preparing to unpack .../1-oclgaussrack.1.3-kali2_amd64.deb ...
Unpacking oclgaussrack (1.3-kali2)
Selecting previously unselected package kali-linux-gpu.
Preparing to unpack .../2/kali-linux-gpu_2016.3.2_amd64.deb ...
Unpacking kali-linux-gpu (2016.3.2-1+git201600114-0kali2)
```

You can use apt-get install package, aptitude install package. For simple installation, they essentially do the same thing. As you will see later, the differences are more meaningful for upgrades. If sources lists several distributions, you can specify the distribution with -target-release, by the name of the distribution you want (for example: apt -t kali-rolling upgrade). To avoid specifying every time you use apt, you can add APT:Default-Release kali-rolling; in the file /etc/apt/conf.d/.
With dpkg, you can also try to install a package and overwrite files with --force-overwrite:

```
# apt -o Dpkg::Options="--force-overwrite" install zsh
```

## 8.2.3. Upgrading Kali Linux

As a rolling distribution, Kali can receive upgrades several times a day. However, that might not be the best strategy. So, how often should you upgrade Kali Linux? There is no hard rule but there are some guidelines that can help you. You should upgrade:

We recommend regular upgrades, because they will install the latest security updates. To upgrade, use apt update followed by apt upgrade, apt-get upgrade, or aptitude. These commands look for installed packages that can be upgraded without removing any packages. In other words, the goal is the least intrusive upgrade. The apt-get command line tool is slightly more demanding than aptitude because it will refuse to install packages that were not installed. The apt tool will generally select the most recent version number (except for packages from kali-bleeding-edge, which are ignored by default).

For more important upgrades, such as major version upgrades, use apt full-upgrade. With this instruction, apt will complete the upgrade even if it removes obsolete packages or install new dependencies. This is also the command that you should use for regular upgrades of your Kali Rolling system. It is so simple that it hardly needs explanation: Unlike apt and aptitude, apt-get doesn't know the full-upgrade command. Instead, you should use apt-get dist-upgrade (distribution upgrade), a well-known command that apt and aptitude also accept for backwards compatibility.

Be Aware of Important Changes: To anticipate some of these problems, you can install the apt-listchanges package, which displays information about possible problems at the beginning of a package upgrade. This information is compiled by the package maintainers and put in /usr/share/doc/package/NEWS.Debian files for your benefit. Reading these files (possibly through apt-listchanges) should help you avoid nasty surprises.

- When you are aware of a security issue that is fixed in update
- When you suspect that an updated version might fix a bug that you are experiencing
- Before reporting a bug to make sure it is still present in the latest version that you have available
