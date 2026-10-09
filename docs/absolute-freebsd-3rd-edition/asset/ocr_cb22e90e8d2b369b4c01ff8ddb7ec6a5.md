your disks. Only then should you proceed to downloading and installing FreeBSD.

Before you even start the install, though, let's look at a couple concepts you'll hit throughout your FreeBSD experience: default files and universal configuration language (UCL).

First, however, you must understand FreeBSD's default configuration filesystem.

# ## Default Files

FreeBSD separates configuration files into default files and customization files. The *default files* contain variable assignments and aren't intended to be edited; instead, they're designed to be overridden by another file of the same name.

Default configurations are kept in a directory called *default*. For example, the boot loader configuration file is */boot/loader.conf*, and the default configuration file is */boot/defaults/loader.conf*. If you want to see a comprehensive list of loader variables, check the default configuration file.

During upgrades, the installer replaces the default configuration files but doesn't touch your local configuration files. This separation ensures that your local changes remain intact while still allowing new values to be added to the system. FreeBSD adds features with every release, and its developers go to great lengths to ensure that changes to these files are backward compatible. This means that you won't have to go through the upgraded configuration and manually merge in your changes; at most, you'll have to check out the new defaults file for nifty configuration opportunities and new system features.

The loader configuration file is a good example of these files. The */boot/defaults/loader.conf* file contains dozens of entries much like this:

verbose_loading="NO" # Set to YES for verbose loader output

The variable *verbose_loading* defaults to NO. To change this setting, do not edit */boot/defaults/loader.conf*—instead, add the line to */boot/loader.conf*