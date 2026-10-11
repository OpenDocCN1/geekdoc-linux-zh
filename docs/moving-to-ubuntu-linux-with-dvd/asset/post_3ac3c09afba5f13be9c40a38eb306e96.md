
of the time. You can, however, also search for a particular version number, the package maintainer's name, dependencies, and provided packages. Let's enter instant messaging in the search field, and click the Search button.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_181_0.png)

**Figure 8-8**
The easiest way to locate packages with Synaptic is to click the Search button and type in what you are looking for.

The result is a list of packages that have the words *instant messaging* somewhere in their description. Click each package individually to get a description of that package. Should you decide you want to install a particular package, right-click the package name and select Mark for Installation (see Figure 8-9).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_181_1.png)

**Figure 8-9** To install a package, right-click the package name and then select Mark for Installation from the drop-down menu.

Part of what makes Synaptic such a joy is that it takes all the work out of having to know what other packages might be needed when you choose to install something. If the software you want needs three additional packages, Synaptic knows and lets you know as well (see Figure 8-10). In my example, there are six additional packages required. Synaptic wants to know if I want to have them automatically marked for installation as well. If you accept—and generally speaking, you always do—click the Mark button to continue.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_182_0.png)

Figure 8–10    If additional packages are required, Synaptic lets you know about them before continuing.

At this point, you can go ahead and search for additional packages if you want. Synaptic remembers the packages you have chosen until you choose to install them or quit the program. When you are ready to install what you have selected, click Apply on the Synaptic icon bar. You get a final window telling you about all the packages that will be installed, how much space will be used, and how big the download itself will be (see Figure 8-11).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_183_0.png)

Figure 8-11 As a final step before installing your packages, Synaptic provides a summary of what it will do.

The install begins, first with the packages being downloaded over the Internet. This is followed by the system preparing the packages for upgrade and ends with the installation of the packages themselves. Throughout the process, a dialog alerts you to the various steps and provides a status bar (see Figure 8-12) so you have some idea of how long the whole thing will take.

Depending on the speed of your machine or the number of packages, this could take from several seconds to several minutes or more. The process bar gives you some clues as to how much time this will all take. When the process is done, you get a final dialog letting you know that all changes (installations, upgrades, package replacements) are done. Click Close and you go back at the main Synaptic window.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_184_0.png)

Figure 8–12  The final step in the process: Your packages are being installed.

## Keeping Ubuntu Up-to-Date

If your system is connected to an always up, Internet connection, Ubuntu regularly scans its update repositories for general patches and security fixes. When something becomes available, you see a message pop up at the top of your screen (see Figure 8-13). These updates may be anything from patches and fixes to security updates. The latter is a particularly good reason to stay on top of the latest updates.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_184_1.png)

Figure 8–13  From time to time, you may see a pop-up similar to this one, alerting you to software updates.

It is possible that you do not see the preceding pop-up. Depending on whether you've already seen the message, banished it earlier, or whether you’ve been busy installing packages, the red icon itself is a giveaway. If you pause your mouse cursor over it, you see a tooltip alerting you to the number of updates available (see Figure 8-14).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_185_0.png)

Figure 8-14  Watch for the update icon in the top panel.  Pausing your mouse over the icon generates a tooltip with additional information.

There are a couple of things you can do here. The first is to just click the icon. This starts the update manager. Right-click the icon and a pop-up menu appears with a number of options. You can choose to view the available updates, update the package list now, or go ahead and install the updates. There’s also an option here to change the update manager preferences.

Regardless of whether an update icon is present in the top panel, you can also start the update manager by clicking System on the top panel and selecting Update Manager from the Administration submenu. Remember that the system only checks for updates according to the schedule you selected earlier in the chapter. It is possible that there are updates you need to check on before the scheduled time (for example, you’ve heard about a security update and you want to check on it now). Either way, because this is an administrative function, you are asked for your password before continuing. Enter it and the Software Updates window appears (see Figure 8-15).

At the bottom of this window, there’s a Show Details label with a small arrow to the side. If you want to find out what a particular update does or what changes come with an update, click the arrow. The window splits into a top and bottom pane with an information pane at the bottom. Click a package name up top and the description of changes appears below.

Unless you have good reason not to, you can usually accept the changes. Click the Install Updates button and the packages start to download. If you have followed along up to this point, what happens next will be familiar to you. The installation of those packages follows the same approach you saw with Synaptic and the basic GNOME package installer.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_186_0.png)

Figure 8-15 The Software Updates window lists all of the current packages available for update.

## DEBs, the Shell Way

For most, using Synaptic, or the simple package installer I told you about earlier, is definitely the way to go. However, as with many things, there is another way to do it and this way involves working down at the shell. If you are interested in finding out what goes on beneath Synaptic’s slick exterior, take a look at this short introduction to package administration using the Linux shell.

In the Debian world, of which Ubuntu is a part, there are two useful commands for dealing with packages at the command line: `dpkg` and `apt-get`. The most basic method of installing a package is with this format of the `dpkg` command:

```
sudo dpkg --install ft1-transport_2.1-1ubuntu1.deb
```

`dpkg` is the basic package installation tool for Debian and Debian-based systems such as Ubuntu. The previous command installs the package. This one removes it:

```
sudo dpkg --remove ft1-transport
```

> **Note** If it looks like I am saving keystrokes here, there is a reason. I only indicate the package release number and subsequent extensions at installation time. To remove a package, you only need the package name itself.

You should be aware that there is another step to consider when removing a package. Although the program is now gone from your system, its configuration files remain (which can be a good idea). To get rid of those as well, you need to purge the package:

```
sudo dpkg --purge ft1-transport
```

Now that I have had you do it the long way, you could start with a purge to both remove the package and purge the configuration files in one step.

## Great, but Can You Tell Me What Is Already There?

Sure thing. If you want to get a list of every package on your system, use the `--list` option to `dpkg`. You might want to pipe that output to the more command:

```
dpkg --list | more
```
