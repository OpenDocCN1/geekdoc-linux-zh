
[content]files vulnerable, including to malicious software that might get in. Instead of using a root account, use the word sudo before a command on the Raspberry Pi to indicate that you want to carry it out with the authority of the root user. You can't use it before all commands, it's essential for installing software.

If you ever get an error message that tells you something can be done only with the authority of the root, try repeating the command but putting sudo front of it.

![](img/df9a01bf057d58c2401b5edabd6e8829_129_0.png)

## Updating the cache

The first step in installing software is to update the cache, which is the list of packages the package manager knows about. You do that by entering the following command:

```
sudo apt-get update
```

You need to have a working Internet connection for this work, and it's likely to take some time. Consider leaving the Raspberry Pi to get on it while you have a cup of tea — or a slice of raspberry pie, perhaps.

![](img/df9a01bf057d58c2401b5edabd6e8829_129_1.png)

## Finding the package name

The package manager cache (the apt cache, in Linux terminology) contains an index of all the software packages available. You can search it to find the software you want using a tool called apt-cache. For example, you can find all the software by using

```
sudo apt-cache search game
```

The list is huge, so you might want to use less to browse it, like this:

```
sudo apt-cache search game | less
```

The screen output looks like this (I left out a couple of additional packages near the top of this list relating to @ad):

```
@raspberrypi ~ sudo apt-cache search game
@ad - Real-time strategy game of ancient warfare
2048-qt - mathematics puzzlegame
3dchess - Play chess across 3 boards!
4digits guess-the-number-game, aka Bulls and Cows
7kaa-data - Seven Kingdoms Ancient Adversaries - game data
a7xpg - chase action game
a7xpg-data - chase action game - game data
ab - Side-scrolling game named "Abe's Amazing Adventure"
abe-data - Side-scrolling game named "Abe's Amazing Adventure"
[list continues...]
```

The before the hyphen tells you the name of the package, which is what you need to be able to install it. That might not be the same as the game's title or its popular name. For example, there are lots of solitaire card games you can install, but none of them has the package name solitaire. To find the package name for solitaire game, you would use

```
sudo apt-cache search solitaire
```

This search returns 22 results, and the first one is

```
ace-of-penguins - penguin-themed solitaire game
```

## Installing software

If you know the name of the package you would like to install, the following command downloads it from the Internet and installs it, together with any other packages it needs to work correctly (known as dependencies):

```
sudo apt-get install ace-of-penguins
```

The last bit is the name of the package we found by searching the cache.

When you're searching the cache, you use apt-cache in the command, and when you're installing software, you use apt-get. It's easy to get these two commands mixed up, so if your instruction doesn't work, double-check that you're using the right one.

![](img/df9a01bf057d58c2401b5edabd6e8829_130_0.png)

Note that not all of the software available in the packages works well on the berry Pi. It's easy enough to try, though, and remove it again if it doesn't work for you.

## Running software

Some programs can be run directly from the command line by just typing names, such as

```
penguinspuzzle
```

which runs the Penguins game. (See Chapter 19.) This game doesn't show up on the menus in the desktop environment.

Most-end user applications require the X server, which means you need to be in the desktop environment to run them. After installing them, you can find them on the Applications menu.

Whether a program should be run from the command line or in the desktop environment depends on the program, so consult its instructions if you can't work how to start it.

## Upgrading the software

The package manager's responsibility doesn't end once it has installed software. It can also be used to keep software up to date, installing the latest enhancements and security improvements. You can issue a single command to update all the software on your Raspberry Pi:

```
sudo apt-get update
```

Update the cache to sure apt installs the latest updates to your installed packages. You can combine both commands into a single line, like:

```
sudo apt-get update && sudo apt-get upgrade
```

The && means that the second command should be carried out only if the first succeeds. If the update to the cache doesn't work, it won't attempt to upgrade all the software.

The upgrading process often ties up your Raspberry Pi for some time.

If you want to update just one application, you do that by issuing its install command again. Imagine that you've already installed Ace of Penguins and you enter

```
sudo apt-get install ace-of-penguins
```

That prompts apt to check for any updates to that package and install them. If there are none, it tells you that you're already running the latest version.

## Removing software and freeing up space

The package manager can also be used to remove software from your Raspberry Pi. For example:

```
sudo apt-get remove ace-of-penguins
```

This particular command leaves traces of the applications, which might include user files and any files containing settings. If you're sure you won't need any of this information, you can completely remove and clean up an application using

```
sudo apt-get purge ace-of-penguins
```

You can do two other things to free up some space on your SD or MicroSD card and clean up your system. First, you can automatically remove packages that are no longer required. When a package is installed, other packages it requires are usually installed alongside it. These packages can remain after the original program has been removed, so there's a command to automatically remove packages that are no longer required. It is

```
sudo apt-get autoremove
```

It lists the packages that will be removed and tells you how much space it will free before prompting you to enter A to confirm that you want to continue.

When you install a package, the first step is to download its installation file to your Raspberry Pi. After the package has been installed, its installation remains in the directory /var/cache/apt/archives. Over time, as you try out and more packages, this can amount to a lot of space on your SD or MicroSD card. Take a look in that directory to see what's built up there. These files aren't doing much. If you reinstall a program, you can always download the installation file.

The second thing you can do to clean up your SD card is remove these files using

```
sudo apt-get clean
```

## Finding out what’s installed

To find out what software is installed on your Raspberry Pi, you can use

```
dpkg --list
```

This command doesn't need root authority to run, so it doesn't require you to use sudo at the start.

If you want to find out whether a specific package is installed, use

```
dpkg --status packagename
```

For applications that are installed, this also provides a longer description than the short apt-cache description, which might include a web link for further documentation.

![](img/df9a01bf057d58c2401b5edabd6e8829_133_0.png)

The Raspberry Pi includes many packages that come with the Linux operating system and are required for it. If you didn't deliberately install a package, exercise caution before removing it.

## Managing User Accounts on Your Raspberry Pi

If you want to share the Raspberry Pi with different family members, you could create a user account for each one so that all have their own home directory. The robust permissions in Linux help to ensure that people can't accidentally delete each other's files, too.

When we looked at the long listing format earlier in this chapter, we discussed permissions. You might remember that users can be members of groups. On the Raspberry Pi, groups control access to resources like the audio and video hard-ware, before you can create a new user account, you need to understand which groups belong to. To find out, use the groups command to see which groups default pi user is a member of:

```
pi@raspberry ~ $ groups pi
im dialout cdrom sudo audio video plugdev games input
netdev gpio i2c spi
```
