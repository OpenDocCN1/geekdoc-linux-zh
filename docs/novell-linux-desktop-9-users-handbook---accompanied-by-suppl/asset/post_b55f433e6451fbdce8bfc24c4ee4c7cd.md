
# CHAPTER 6: Managing Files

![](img/6e85ebc4ce06a64c82109523b60183ba_165_0.png)

- 1 Open Nautilus
- 2 Select Folders and Files for Archive
- 4 Name Archive
- 3 Create Archive
- 5 Move Archive to Destination
- 6 Back Up Files

## 1 Open Nautilus

On the desktop double-click your Home icon.

## 2 Select Folders and Files for Archive

Select the folders and files that you want to place in the archive.

## 3 Create Archive

In Nautilus, select Edit, Create Archive. A Create Archive dialog box opens.

## Name Archive

Type a name for the archive in the Create Archive dialog box. The file is saved as a tar.gz file. Click Create to end the creation process.

## Move Archive to Destination

Open a USB drive or other location in a second Nautilus window and drag the archive file to its new location while holding down the Alt key. When you release the archive file in the destination window, click Move Here on the shortcut menu. You have archived and backed up your important files.

## Restore Files

Restoring your important files is just a matter of locating the archive that you created as a backup. You can then use File Roller to extract the files so that you can use them.

### BEFORE YOU BEGIN
- Archive Files with File Roller
- Backing Up and Restoring Files
- Back Up Files

## 1 Open Archive Location

Use Nautilus to locate the folder, CD, USB drive, or network drive where you stored your archive file.

To open network locations, double-click the Computer icon and then double-click the Network icon. Browse your network as needed to find the folder location.

## 2 Open Archive File

Double-click the archive file, and the File Roller window opens showing the contents of the archive.

# CHAPTER 6: Managing Files

## 1 Open Archive Location

![](img/6e85ebc4ce06a64c82109523b60183ba_167_0.png)

## 2 Open Archive File

## 3 Specify Destination Location

## 4 Extract Files

## 5 Restore Files

## 3 Specify Destination Location

In the File Roller, select the Extract button. In the Extract dialog box that appears, select the folder (the location) where you want to extract the file. Folders will be re-created for the extracted files by default.

## 4 Extract Files

In the Extract dialog box, click the Extract button. The files are extracted to the location that you chose, and folders will be re-created. Close the File Roller window. Use Nautilus to open the location and view the extracted files and folders.

# CHAPTER 7

# Adding and Managing Software Applications and Tools in NLD

### IN THIS CHAPTER:
- 59 About Updating and Adding Applications to NLD
- 60 About Updating Applications Using Red Carpet
- 61 Run Red Carpet to Update NLD Applications
- 62 About RPMs
- 63 Find Applications Using Red Carpet
- 64 Install Applications Using Red Carpet
- 65 Install and Remove Applications Using YaST
- 66 About Installing Applications from Other Archive Types

# CHAPTER 7: Adding and Managing Software Applications and Tools in NLD

After you become comfortable with the NLD environment, you will probably consider adding additional applications and applets to your system. You will also want to keep your NLD installation files up-to-date. NLD makes it easy for you to install and update software.

In this chapter we explore different ways to update the software on your computer and add new software. We take a look at program archive types and become familiar with YaST and Red Carpet.

## 59 About Updating and Adding Applications to NLD

NLD provides two different GUI tools that make it easy for you to update programs, add software, remove software. YaST, the NLD administrative configuration tool, allows you to add and remove software from your NLD installation (add software using the NLD installation disks or updates) and also makes it easy for you to run a system and apply patches to your system.

Three icons in the YaST window (when Software is selected in the left pane) are of particular interest:

- Install and Remove Software—This tool allows you to view the software installed on your system from a particular installation CD or DVD. You can also use this tool to remove software from your system.
- System Update—This tool allows you to connect to Novell's servers and update your system software.
- Patch CD Update—This tool allows you to install patches to your system from a patch CD or DVD.

### KEY TERM

A patch is a software update to a particular system or software file that resolves issues or tightens security.

To access YaST you must know the root password. This makes sense because even though YaST makes it easy to add and remove or update software, there is always a level of risk involved in maintaining the integrity of your system. Think carefully before adding and removing software.

Another tool that makes it easy to quickly update your NLD software and search for other software packages on the Novell software update servers is Red Carpet. Red Carpet provides a GUI where you can view available updates, view software installed on your system, and search for available unavailable software on the NLD update servers. To use Red Carpet you need to know the root password.

## 59 About Updating and Adding Applications to NLD

YaST provides easy access to software installation and system update tools.

![](img/6e85ebc4ce06a64c82109523b60183ba_170_0.png)

Red Carpet makes it easy to update your system from online software resources.

![](img/6e85ebc4ce06a64c82109523b60183ba_170_1.png)

### NOTE

If you are running a free or "sample" version of NLD, you typically get updates for only a limited period of time. A "full-blown" version of NLD provides a much longer time frame for updating the system software, software applications, and applets. In either case, you must activate the updates for your system for Red Carpet to work properly.

One other thing that we need to discuss before looking at Red Carpet and then YaST is the issue of dependencies. Let's say you want to install program A, but there is a dependency for program B. This typically means that program B must also be installed on the system for program A to actually function after you install it. In some few cases, programs have negative dependencies, meaning you cannot install both the programs on the system if you want either one to run.

# CHAPTER 7: Adding and Managing Software Applications and Tools in NLD

### KEY TERM

Dependency—A necessary software module for a program to run on the Linux system. Linux applications and applets require other software modules to be installed before application or an applet will run.

Dependencies for a software package must be met for it to run after installation.

![](img/6e85ebc4ce06a64c82109523b60183ba_171_0.png)

The question arises: When should you use YaST and when should you use Red Carpet to install and update software? They both share some of the same capabilities.

YaST works best for adding software and patches to your system from CDs and DVDs. YaST actually has a better tool than Red Carpet to check whether the dependencies are met for a package you want to install without having to view a list of dependencies.

Red Carpet is easy to deal with in terms of performing system updates because an indicator appears on the top panel when system updates are available. Red Carpet (at least in my opinion) also makes it easier to quickly view all the software installed on your system, and with just a couple of clicks you can remove or add a package.

## 60 About Updating Applications Using Red Carpet

Red Carpet provides you with the ability to quickly do a system software update, including updates for installed applications and applets. Red Carpet updates are provided by servers set up to support NLD. These are called services. The services supply update channels that you can subscribe to (for example, the NLD channel), meaning that you need to be connected to the Internet to run the Red Carpet update.

You have the option of installing all the available updates or selecting individual updates for specific applications or applets. In terms of updating the NLD
