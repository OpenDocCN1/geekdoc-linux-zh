# 130 Linux Web Server Toolkit

if you don't install LILO on a floppy disk and you have a problem where your system won't boot correctly to Linux, you can use the installation disk created at the beginning of the installation procedure. Boot with that disk, but instead of pressing Enter at the first prompt, enter the following command, substituting the correct partition for your Linux filesystem (in this example, it is the third partition of the first IDE hard disk):

With all that said, it's usually best to choose the LILO option that is chosen for you by default in the menu. The installation program analyzes your system and makes the best choice in most cases.

Press Enter to use the default name for your standard Linux system. If you used any parameters when you started the installation, they should be entered here. They are stored in the LILO configuration file, so you don't have to enter them each time you start your system.

Now you'll see a list of other partitions on your system. You can select any of these to add a boot option to LILO, so you can choose to boot into DOS, for example, each time you start your computer.

The same steps (pick a partition and enter a name) are followed for each boot option you need to enter. When you've entered them all, choose the menu item to indicate that you've finished.

Review the LILO configuration file (well, just press Enter, because you can't change it here). LILO is installed.

# CHOOSING SERVICES

From the next screen, shown in Figure 5-9, you can choose which network services are started each time you start your Linux system. The boxes that you check in this list (use the-use the arrow keys and the spacebar) will be added to your initialization files with the correct information to have them start automatically.

![](bbox=[0.18, 0.755, 0.915, 0.963])