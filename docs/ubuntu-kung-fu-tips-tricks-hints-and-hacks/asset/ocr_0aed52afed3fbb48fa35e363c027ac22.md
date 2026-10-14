star, or red down-pointing arrow, and the first time it appears a callout will appear informing you that updates are available.

Clicking the icon will show a list of packages that can be updated.

> TIP Ensure any other software installation application is closed first, such as Synaptic. Only one software administration tool can run at any one time. This includes command-line tools.

It’s not absolutely essential to read through the list of updates, but doing so will take only a minute or two, and it’s a good idea to keep track of what’s being updated. Assuming you’re happy with the list of updates, click the INSTALL UPDATES button to automatically download and install the software.

If desired, you can force Update Manager to run by clicking its entry on the System ▸ Administration menu and clicking the CHECK button when the program window appears.

Depending on what system components are updated, you may have to restart your computer to complete installation. You’ll know if this is the case because the update manager icon will change to two circular arrows that, when clicked, will prompt you to reboot the computer.

When a new release of Ubuntu becomes available, Update Manager will inform you via a pop-up window. You can then choose to upgrade (or not, if you do not wish to).

# Updating at the command-line

To update at the command-line, two sets of commands can be issued:

+   - sudo apt-get update
+   - sudo apt-get upgrade

or

+   - sudo apt-get update
+   - sudo apt-get dist-upgrade

sudo apt-get update grabs the latest list of packages, so should always be used before updating.

sudo apt-get upgrade updates all software packages to the latest available versions. If you wish to update the system manually at the command-line, this command should be issued weekly. In contrast, sudo apt-get dist-upgrade updates the entire system, including several vital system files, and thereby updates Ubuntu to the latest release. If run on an 8.04 system, for example, it will update Ubuntu to 8.10. It should be run only when you know a new release to be available.