
your screen. To remove it from the list of packages to be installed, press - on your keyboard while it is selected.

Pressing “u” will have Aptitude download the latest package information from your APT servers (equivalent to an apt-get update), then pressing “U” (capital “U”) will have it select for upgrade any packages for which updates are available. Once you have done that, as well as used + and – to select any other packages you want to install or remove, press “g” to have Aptitude show you a summary of what will change. This summary is color-coded so that packages to be removed are colored purple, packages to be installed are colored green, and packages to be upgraded are coloured cyan. Press “g” again to confirm the plan and have Aptitude start up apt-get to make your changes. If the summary is incorrect, press “q” to go back to the menu screen.

![](img/e464b828c497c99e41f61d4c55f1c0db_795_0.png)

FIGURE 34.1 The Aptitude package manager is text-based, but lets you use your mouse to access its menu bars.

You can at any time press ? to bring up a short list of common commands for Aptitude. The most popular commands are listed across the top, such as the Ctrl+T shortcut to get to the menu bars.

### NOTE

Aptitude, like apt-get, is not entirely devoid of humor. Whereas apt-get has Super Cow Powers, running aptitude moo prints out a short message that Aptitude has no such Easter eggs. However, if you run aptitude -v moo you'll see something else, if you run aptitude -v -v moo you'll see something else, and so on—just keep adding more -v parameters!

Once you are in Aptitude, you can while away some time by playing Minesweeper—it is under the Actions > Play Minesweeper menu option.

## The dpkg Back-End

The apt-get program we looked at in Chapter 7 is a tool that is designed to download packages and their dependencies so that you can avoid doing that tedious task yourself. However, when it comes to actually installing the packages, apt-get relies on the low-level dpkg command, which is what does the actual job of installation and tracking what is installed.

So, if you have a .deb package and need to install it, apt-get will not be able to help you. Instead, you need to use dpkg directly, by invoking it like this:

```
dpkg -i yourfile.deb
```

That will extract the package and install it on your system. If you just want to extract the contents of the package without installing them to your system, you can use the --unpack parameter, like this:

```
dpkg --unpack yourfile.deb
```

Rather than extracting a package, you can just have dpkg list its contents by running it with the -c parameter, like this:

```
dpkg -c yourfile.deb
```

Once a package is installed, you can uninstall it by using the -r switch and providing the package name. Note: you need to provide the package name, not the filename of the .deb you installed. For example:

```
dpkg -i libgtk2.0-0.deb
dpkg -r libgtk2.0-0
```

You can get a complete list of all the packages you have currently installed by running this command:

```
dpkg --get-selections
```

This is commonly used with grep to check whether a very specific program is installed. For example:

```
dpkg --get-selections | grep gnumeric
```

If you see a line "gnumeric INSTALL", that means you have Gnumeric installed. The --get-selections parameter is also good for installing a predefined selection of packages. The software list that --get-selections exports can also be imported back into dpkg on another machine, thus making sure the two machines have the same software. To export your package selections to a file, run this:

```
dpkg --get-selections > packages.txt
```

To then import that list back into a system, run this:

```
dpkg --set-selections < packages.txt
```

Note that that does not actually install any software; it merely sets the “selection state” inside dpkg, meaning that you have asked for those packages to be installed. You need to use Aptitude to go ahead and install those packages—just press “g” and it will show you the missing packages that have been marked for install by dpkg, and then press “g” again to go ahead and install them.

## Configuring APT

If you do not have access to a graphical tool such as Synaptic, you can hand-edit the servers that you want APT to read from using a console-based editor. This also is helpful if you want to add a custom repository, if you want to use a particular version of Ubuntu (such as a newer version than you first installed), or if you want to use a local repository to save downloading packages repeatedly.

APT’s sources are stored in the /etc/apt/sources.list file, so you’ll need to launch your editor through sudo to make changes. Reading the sources.list file can be baffling at first, but it is actually quite easy—particularly as people running custom repositories will often tell you exactly what to type in.

The two types of line you will find in sources.list are “deb” and “deb-src”. The first is downloaded program packages that can be installed and run as normal, but the second offers pre-packaged source code. Admittedly, the deb-srcs are very rarely used, but there is no harm having them around. Comments—lines starting with #—are ignored by APT. So, if you want to temporarily disable a repository, just insert a # at the start of its line, save the file, and re-run apt-get update.

Each line is made up of the following parts:

```
[deb/deb-src]  url  distribution  [components...]
```

The URL will look something like “http://gb.archive.ubuntu.com/ubuntu/”, and points to the location where the APT index and packages are stored. This URL is the same for all versions of Ubuntu; what changes is the “distribution” part of the line, which comes next. This is set to the first part of the Ubuntu code-name for the distro you are using—“warty” for 4.10, “Warty Warthog”; “hoary” for 5.04, “Hoary Hedgehog”; “breezy” for 5.10, “Breezy Badger”; and “dapper” for 6.06, “Dapper Drake”. Incidentally, the next code-name for Ubuntu is “Edgy Eft”, so if you want to upgrade to that you need to use the distribution name “edgy”.

After the distribution comes the individual components you want to select. By default this is usually “main restricted,” which means you want to download the main Ubuntu packages, as well as any restricted copyright material. Packages under restricted copyright things are things like binary drivers, so it is best to leave “restricted” enabled. You may—probably on a different deb line—have the same URL and distribution, this time with the
