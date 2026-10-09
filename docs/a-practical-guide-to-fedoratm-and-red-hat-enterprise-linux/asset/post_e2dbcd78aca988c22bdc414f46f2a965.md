
# Figure 3-4 The Install Image Boot menu

![](img/243613168ac865b539f12460d966088e_117_0.png)

Press the SPACE bar within 60 seconds to stop the countdown. If you do not press the SPACE bar, after 60 seconds Fedora/RHSEL begins a graphical installation.

- **Install Fedora**
  Installs a Fedora/RHSEL system using the Anaconda graphical installer.
- **Test this media & install Fedora**
  Tests the installation medium and installs a Fedora/RHSEL system using the Anaconda graphical installer.
- **Troubleshooting**
  Displays the Troubleshooting menu (Figure 3-5).

# Figure 3-5 The Install Image Troubleshooting menu

![](img/243613168ac865b539f12460d966088e_117_1.png)

The Troubleshooting menu has the following selections.

- Installs a graphical Fedora/RHEL system using the graphical installer. Anaconda does not attempt to determine the type of display attached to the system; it uses a basic video driver that works with most displays. Choose this selection if the installation fails before Anaconda displays the Welcome to Fedora screen (page 63).

- Brings up a minimal Fedora/RHEL system but does not install it. After detecting the system’s disks and partitions, the system enters single-user/rescue mode and allows you to mount an existing Linux filesystem. For more information refer to “Rescue an Installed System” on page 456.

- Runs the memory test described on page 58.

- Boots the system from the hard disk. This selection frequently has the same effect as booting the system without the installation medium in place (depending on how the BIOS [page 31] is set up).

- Displays the Fedora Install Image Boot menu.

# THE ANACONDA INSTALLER

Anaconda, which is written in Python and C, identifies the hardware, loads drivers, probes for the devices it will use during installation, builds the filesystems, starts the X server, and installs the Fedora/RHEL operating system. Anaconda can run in graphical interactive mode (default), limited textual mode (see the text on page 72), or automated mode (see “Editing a Kickstart Script” on page 83).

Exactly which screens Anaconda displays depends on whether you are installing Fedora from a live session, an Install Image, or a Network Image; whether you are installing RHEL; which paths you pick through the installation process; and which parameters you specify on the boot command line. Unless you tell it not to, Anaconda probes the video card and monitor, and starts a native X server.

While it is running, Anaconda opens the virtual consoles (page 121) shown in Table 3-1. You can display a virtual console by pressing CONTROL-ALT-FX, where x is the virtual console number and fx is the function key that corresponds to the virtual console number.

**Table 3-1** Virtual console assignments during installation

| Virtual console | Install Image | Live Image |
| :--- | :--- | :--- |
| 1 | Installation dialog | GUI interactive installation |
| 2 | Shell | Login prompt (log in as **liveuser**) |
| 3 | Installation log | Installation log |
| 4 | Storage log | Login prompt (log in as **liveuser**) |
| 5 | Program log | Program log |
| 6 | Login prompt | Login prompt (log in as *liveuser*) |
| 7 | GUI interactive installation | Nothing |

At any time during the installation, you can switch to virtual console 2 (by pressing CONTROL-ALT-F2) and give commands to see what is going on. Do not give any commands that change any part of the installation process. To switch back to the graphical installation screen, press CONTROL-ALT-F1 (Live Image) or CONTROL-ALT-F7 (Install Image).

## Testing the Installation Medium

The first time you use an installation medium, select *Test this media & install Fedora* from the Boot menu and press RETURN to boot the system. Fedora displays a few lines before displaying a line that starts with *Checking*. This line shows the percent of the disk Anaconda has checked as it verifies the contents of the installation medium. If the installation medium is good, the system boots. If you use the same medium again, you do not have to test it: Select *Install Fedora*.

A DVD might fail the media test if the software that was used to burn the disk did not include padding. If a DVD fails the media test, try booting using the *nocomma* parameter. See page 70 for information on adding parameters to the boot command line. If the DVD passes the media test when you boot the system using the *nodma* parameter, the DVD is good; reboot the system without this parameter before installing Fedora/RHEL. If you install Linux after having booted using this parameter, the kernel will be set up to always use this parameter. As a consequence, the installation and operation of the system can be slow.

## Using Anaconda

![](img/243613168ac865b539f12460d966088e_119_0.png)

Anaconda displays the Welcome to Fedora screen after it obtains enough information to start the X Window System. Scroll and click to highlight the language you want to use for installation. This language is not necessarily the same language the installed system will display. Click *Continue*. Anaconda displays the Installation Summary screen.

## The Installation Summary Screen

Anaconda takes a while to load the information the Installation Summary screen displays (Figure 3-6, next page). While it is loading, some items are grayed out. You must wait until Anaconda finishes loading this information and the items are no longer grayed out before you can select these items. *You might need to scroll down to display the Storage item*.

Typically an orange bar that holds an exclamation point in a triangle and the words *Please complete items marked with this icon before continuing to the next step* appears at the bottom of the window. While this bar is displayed the button labeled *Begin Installation* is grayed out to indicate it will not work. The only items you must open and modify are those that display this icon. The items displayed when you are installing Fedora from a live session are a subset of those displayed when you install from an Install Image.

![](img/243613168ac865b539f12460d966088e_120_0.png)

Click on an item to display a screen that allows you to work with that item. Click **Done** to return to the Installation Summary screen. The items that appear in the Installation Summary screen are divided into three groups: Localization, Software (not from a live installation), and Storage.

## You do not need to open most items on the Installation Summary screen

Each item on the Installation Summary screen displays a note about what Anaconda has chosen for that item. You do not need to open an item if it is set properly. For example, if the Date & Time item shows America/Los_Angeles timezone and that is correct, you do not need to open this item. Frequently the only item you need to open is Installation Destination (page 67).

# LOCALIZATION

**Date & Time**  
The Date & Time screen displays a world map that allows you to specify the local time zone. Click a city in the local time zone; Anaconda displays the name of the city in the spin box labeled **City**. Alternately, you can use the spin boxes labeled **Region** and **City** to specify a city.

By default, Anaconda sets up the new system to use NTP (Network Time Protocol) to keep the system clock accurate. If you do not want to use NTP, click the switch labeled Network Time to set it to Off and use the widgets at the bottom of the screen to set the system clock.

**Keyboard**  
The Keyboard Layout screen allows you to specify the type of keyboard that will be attached to the installed system. The box on the left side of this screen displays available keyboard layouts. The entry at the top of the list is the default layout to be used both during installation and for the installed system. Use the buttons at the bottom of this box to add layouts and remove, move, and test the highlighted layout.  
You can specify a keyboard for use during installation only, but you can specify only keyboards that are in the list on the Keyboard Layout screen. Use the small keyboard button to make this change. The button is located at the upper-right of all installation screens.

- Language Support: Not available with a live installation. In the Language Support screen, put ticks in the check boxes adjacent to the languages you want to install.

# SOFTWARE

Not available with a live installation.

- **Installation Source** Typically you install Fedora from the medium you booted from. If that is the case you do not need to open the Installation Source screen. This screen allows you to:
  - Specify as the installation source either the medium you booted from (Auto-detected installation media) or a location (URL) on the network
  - Choose to verify the medium you booted from
  - Install updates as Anaconda installs the system
  - Specify additional repositories (page 533) to use during installation.

The top part of the Installation Source screen is labeled Which installation source would you like to use? and has two radio buttons. By default, Auto-detected installation media is selected and displays the name of the device that holds the installation medium and the label on the medium. Click the button labeled Verify to test that the image on the installation medium is good.

## Test the installation medium

It is possible for data to become corrupted while fetching an installation image; it is also possible for a transient error to occur while writing an image to a recordable medium. When you boot from an installation medium, the button labeled Verify on the Installation Source screen allows you to verify that the image on the installation medium does not contain any errors. Testing the installation medium takes a few minutes but can save you hours of aggravation if the installation fails due to a bad medium.

The second radio button in this section is labeled On the network and allows you to specify a Web, FTP, or NFS URL. When you select Closest mirror from the drop-down list, Anaconda finds the closest Fedora mirror and downloads packages from that site; after you click Done, Anaconda takes a moment to locate the closest mirror. If you reopen the Installation Source screen after selecting Closest mirror, Anaconda reverts to the installation medium and not installing updates.

By default Anaconda does not install updates while it installs Fedora/RHEL. You update the software after you install the system. Remove the tick from the check box labeled Don't install the latest available software updates to cause Anaconda to update software as it installs it.
