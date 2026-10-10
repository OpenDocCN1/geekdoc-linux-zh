
-   RPMforge.net (http://rpmforge.net) — This site represents a merge of three separate repositories that offered Fedora RPM packages: dag.wiiers.com, www.freshrpms.net, and dries.ulyssis.org. They strive for compatibility with the Fedora repository in the packages they offer. See the site's manifest (http://rpmforge.net/manifest.php) for more on RPMforge's project goals. To configure your Fedora system to access RPMforge.net repositories, look for an rpmforge-release package (not yet available, but it may be when you read this) for Fedora 8:
    > http://rpmforge.net/user/packages/rpmforge-release

-   Livna.org (http://rpm.livna.org) — Begin as an extension of the Fedora.us site, rpm.livna.org contains RPM software packages that are outside of the Fedora Project. This is a good place to get audio and video players (such as xine, mplayer, ffmpeg, ogle, and so on) that may not meet the licensing requirements adhered to by Red Hat, Inc. By installing the livna-release RPM, yum is configured to access the rpm.livna.org repository. Look for the Fedora 8 livna-release RPM at the following URL:
    > http://rpm.livna.org/fedora/8/i386/

-   Dag (http://dag.wiiers.com/packages) — This site contains more than 45,000 RPMs from more than 2400 different projects. Currently, the repository has not been updated for the latest Fedora release and there is no RPM to automatically set up access that repository from yum. You can, however, look for Dag packages from the merged RPMForge.net site.

-   FreshRPMs (www.freshrpms.net) — Another site with a good selection of high-quality RPMs is FreshRPMs.net. This site has a good selection of audio and video players that are outside of the mainstream Fedora repositories. By installing the freshrpms-release RPM, yum is configured to access the FreshRPMs repository. Look for the Fedora 8 freshrpms-release RPM at the following URL:
    > http://ayo.freshrpms.net/fedora/linux/8/i386/RPMG.freshrpms/

-   Dribble (http://dribble.org.uk) — RPM packages focused on fun software are contained in the Dribble repository. Many of the packages are for games and console game emulators. Look for a dribble-release package, which you can use to automatically enable the Dribble repository for your Fedora system, at this URL:
    > http://dribble.org.uk/listrpm1.html

-   ATRPMs (http://atrpms.net/dist/f8) — This site has RPMs containing many drivers for video cards, wireless cards, and other hardware not included with Fedora. If you want to try out a personal video recorder, this site also has RPMs for the MythTV project. By installing the atrpms-package-config RPM, yum is configured to access the atrpms.net repository. Look for the Fedora 8 atrpms-package-config RPM at the following URL:

## Running yum to download and install RPMs

With the repositories identified, downloading and installing an RPM you want is as simple as running yum with the *install* option to request the RPM. With an active connection to the Internet, open a Terminal window as root user.

The first thing yum does is download metadata and headers for all packages you might want from each repository. Then, after presenting you with the list of dependencies it thinks you need, it asks if you want to install the necessary packages. Here is an example of using the yum command to download the *madwifii* media player:

```
# yum install madwifi
Setting up Install Process
Parsing package install arguments
fedora 100%|=========================| 2.1 kB 00:00
atrpms 100%|=========================| 951 B 00:00
Reading repository metadata in from local files
primary.xml.gz 100%|==========| 2.5 MB 00:04
.
.
.
Transaction Summary
===============================================
Install 4 Package(s)
Update 0 Package(s)
Remove 1 Package(s)
Total download size: 17M
Is this ok [y/N]: y
Downloading Packages
.
.
.
```

As you can see from this example, yum checked two different software repositories: Fedora and atrpms packages for Fedora 8. After listing the dependencies, yum asks if it is OK to install them. Type y and the package and all its dependencies are installed.

Some packages, including the madwifii package shown in the previous example, need to install a version that matches the kernel that you are running. For that reason, installing such a package might also bring an updated kernel package with it.

## Using yum to install packages locally

If you want to install RPM packages with yum that are available from your local system (by inserting the Fedora DVD or copying an RPM to a local directory), you can use the *localinstall* option to yum. For example, if you were to insert the Fedora DVD that comes with this book (and it was mounted on `/media/disk/`), you could type the following to install the gftp package:

```
# yum localinstall /media/disk/Fedora/Packages/gftp-*
yum localinstall /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
.
.
.
Resolving Dependencies
---> Running transaction check
---> Package gftp.i386 1:2.0.18-7.fc8 set to be updated
Dependencies Resolved
================================================================================
Package    Arch     Version                  Repository        Size
================================================================================
Installing:
gftp       i386     1:2.0.18-7.fc8           /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
  946 k

Transaction Summary
================================================================================
Install    1 Package(s)
Update     0 Package(s)
Remove     0 Package(s)

Total download size: 946 k
Is this ok [y/N]: y
```

A good reason for using `yum localinstall` instead of the `rpm` command to install RPM packages is that `yum` will check whether the package you are installing is dependent on any other packages being installed. If `yum` finds that it needs other packages, it will search any `yum` repositories you have configured (at least the main Fedora repository) to download and install what you need.

In this example, you found that gftp didn't require any additional packages be installed. So, typing `y` at the prompt caused only the one package to be installed.

## Using yum for listing packages

Besides downloading and installing new RPM packages, yum can also be used to list available packages as well as those that are already installed. The following examples illustrate some uses of yum.

If you want to see a list of all packages that are available for download from the repositories you have configured, type the following:

```
# yum list | less
```

Adding the `less` command to the end lets you scroll through the list of software (it could be long, depending on which repositories you point to). If you try to install a package and it fails with a message like `package xyzpackage needs xyzfile (not provided)`, you can check for packages that include the missing file using the `provides` option as follows:

```
# yum provides missingfile
```

With the `provides` option, yum will search your repositories for whatever file you enter (instead of `missingfile`) and return the name of any packages it finds that include that file. To search software descriptions in repositories for a particular string, use the `search` option. For example, the following command searches for `arcade` in any package description (this search will find some games):

```
# yum search arcade
```

Because yum packages are not automatically deleted after being installed, you might want to go through on occasion and clean them out. To clear out packages from subdirectories of the `/var/cache/yum` directory, type the following:

```
# yum clean packages
```

If you would like to check to see RPMs that were installed from repositories outside of the main Fedora repository, you can do so using the `list extras` option. Here is an example:

```
# yum list extras
Setting up repositories
Reading repository metadata in from local files
Extra Packages
AdobeReader_enu.i386
flash-plugin.i386 9.0.48.0-release installed
```

The list shown includes Acrobat Reader (which I got from the Adobe Web site), which does a nice job displaying PDF files. The other package is for running the Flash plug-in with the Firefox Web browser. Note that this list includes all packages from repositories configured for your system that are outside of Fedora. (For example, it would list packages installed from Livna and ATRPMs, if those repositories were configured.)

## Using yum-utils package

There are several utilities in the yum-utils package for working with yum repositories and managing software packages. To get these utilities, type the following yum command:

```
# yum install yum-utils
```

These utilities provide different ways of cleaning up repositories, getting packages without installing them, and doing different query types. Here are some examples:

-   **package-cleanup** — Check your local RPM database for dependency problems and packages that are not needed. Options include `--problems` (to check dependency problems in the RPM database), `--orphans` (to list packages that are not currently
