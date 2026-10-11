most users outside the Ubuntu environment. This could eventually lead to Canonical mothballing Snap again, as has often been the case in the past with in-house developments such as Ubuntu Touch or the Mir display manager.

This situation has led some distributions to reject or even block snaps. One prominent example is Linux Mint, based on Ubuntu LTS, whose developers decided as early as 2020 not to deliver snaps [3]. They also announced that Linux Mint, starting in version 20, would actively prevent the installation of the Snap framework via the graphical package manager, preventing snaps from automatically ending up on the user's system through the background. Laptop manufacturers System76 [Pop!_OS] and Tuxedo (Tuxedo OS 1) also avoid shipping snaps with their Ubuntu derivatives. Even Ubuntu users have not rallied behind Snap, as suggested by many guides that describe installing Firefox in Ubuntu as a DEB.

# unsnap

Former Snap Co-developer Alan Pope, who left Canonical in 2021 after 10 years with the company, has developed unsnap [4], a script that replaces snaps with Flatpaks where available. The script, hosted on GitHub, has been tested by the developers for use on Ubuntu and all derivatives that offer snap and packages in the Snap format.

To test unsnap on a freshly installed Ubuntu 22.04 LTS, I set up a few more packages from the Snap Store in addition to the existing snaps via the Ubuntu Software package manager and then listed them just to be sure (Figure 2). I then downloaded the unsnap script from GitHub. To do this, I first had to install the git package and then run the command from Listing 1.

Before getting into the nitty gritty, let's take a look at how the script works. Immediately after startup, unsnap creates a log directory in which it generates six additional scripts tailored to the particular system (see Table 1). The applist.csv [5] file is used to find Flatpaks that match the installed snaps.

# Multiple Steps

To start the script, first change to the appropriate directory by typing cd unsnap.

![](bbox=[0.37, 0.09, 0.98, 0.25])

**Figure 2: The `snap list` command lists all snaps installed on the system.**

The `./unsnap` command (Figure 3) first informs you that various checks will be run to determine if Flatpak is already installed and Flathub is included, as well as which snaps have Flatpak equivalents.

# Listing 1: Installing unsnap

```
$ git clone https://github.com/poppey/unsnap
```

Next, `unsnap` creates the helper scripts. If you have a reason not to run one of the helper scripts, you can launch these scripts manually one after the other. Otherwise, call `./unsnap` auto to automatically install the scripts (Figure 4).

On my lab system, I installed about 20 snaps, of which unsnap was able to replace about half. However, I intentionally installed snaps such as the Canonical Juju and LXSD tools, as well as the Mutter command-line email client, to test how the script responded (Figure 5). In general, the chances of finding a Flatpak counterpart for graphical apps

# Table 1: unsnap Subscripts

| Script | Function |
|---|---|
| 08-backup | Runs the snap save command for each Snap package to be migrated. |
| 01-install-flatpak | Installs the Flatpak package manager if not already done. |
| 02-enable-flathub | Adds the Flathub repository to Flatpak if not enabled. |
| 03-install-flatpaks | Installs Flatpaks for each identified Snap package, if it exists. |
| 04-remove-snaps | Removes snaps that have alternative Flatpaks. |
| 99-remove-snapd | Removes snapd itself, which removes any snaps that are still installed. |

![](bbox=[0.37, 0.63, 0.98, 0.87])

**Figure 3: If you call the script without additional commands, it determines the system status and creates the required auxiliary scripts, which you can then launch manually, if required.**