The **beagle-info** tool with the **--status** and **--index-info** options provides information about Beagle's current indexing state. Beagle also allows you to do static indexing of directories that do not change often, instead of constantly performing live background indexing.

For specific kinds of application data like MS Word files, Evolution address books, or Adobe PDF files, you can install supporting tools to let Beagle extract indexing information from them. See beagle-project.org/Optional_prerequisites for a detailed listing. The evolution-sharp tool will let Beagle index e-mail addresses, wvl allows Word files to be indexed, and pdfinfo indexes PDF files, both metadata and text. A Firefox extension will index viewed Web sites. To index metadata from video files, you will have to have MPlayer installed.

# ## Accessing File Systems, Devices, and Remote Hosts

Removable media such as CD and DVD discs, USB storage disks, digital cameras, and floppy disks will be displayed as icons on your desktop. These icons will not appear until you place the disks into their devices. To open a disk, double-click it to display a file manager window and the files on it.

The desktop will also display a Computer folder. Opening this folder will also list your removable devices, along with icons for your file system and network connections (see Figure 3-7). The file system icon can be used to access the entire file system on your computer, starting from the root directory. Regular users will have only read access to many of these directories, whereas the root user will have full read and write access.

Opening Network will list any hosts on your system with shared directories, like Windows systems accessible with Samba (see Chapter 39). GNOME uses DNS-based service discovery to automatically detect these hosts. Opening a host's icons will list the shared directories available on that system. When opening a shared directory, you will be asked for a user and password, like the user and password for a directory owned by a Windows user. The first time you access a shared directory, you will also be asked to save this user and

![](bbox=[0.11, 0.63, 0.89, 0.87])

**FIGURE 3-7** Removable devices, Computer folder, and shared network folders (ECHO icons)