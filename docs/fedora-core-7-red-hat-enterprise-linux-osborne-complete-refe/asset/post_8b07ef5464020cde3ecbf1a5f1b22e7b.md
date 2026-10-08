
Starting a GUI from the Command Line

Once logged in to the system from the command line, you still have the option of starting an X Window System GUI, such as GNOME or KDE. In Linux, the command **startx** starts a desktop. The **startx** command starts the GNOME desktop by default. Once you shut down the desktop, you will return to your command line interface, still logged in.

```
$ startx
```

On Fedora, you can use the Desktop Switcher while in your desktop to switch between GNOME or KDE. The Desktop Switcher is accessible from the System | Preferences menu as the Desktop Switching Tool, or with the **switchdesk** command. You will have to install the switchdesk software packages first (use Add/Remove software and search on **switchdesk**).

## Desktop Operations

There are several desktop operations that you may want to take advantage of when first setting up your desktop. These include setting your font sizes larger for high resolution monitors, burning CD/DVD disks, searching your desktop for files, and using removable media like USB drives, along with access to remote host.

## Desktop Font Sizes

With very large monitors and their high resolutions becoming more common, one feature users find helpful is the ability to increase the desktop font sizes. On a large widescreen monitor, resolutions less than the native one tend not to scale well. A monitor always looks best in its native resolution. However, with a large native resolution like 1900 × 1200, text sizes become so small they are hard to read. You can overcome this issue by increasing the font size. The default size is 10; increasing it to 12 makes text in all desktop features like windows and menus much more readable.

To increase the font size, open the Font Preferences dialog by clicking System | Preferences | Look And Feel | Fonts. The Font Preferences dialog is shown in Figure 3-4. You can even change the font itself as well as choose bold or italic. You can further refine your fonts display by clicking the Details button to open a window where you can set features like the dots-per-inch, hinting, and smoothing. To examine a font in more detail, click the Go To Fonts Folder button and click the font.

## Configuring Your Personal Information

The About Me preferences dialog (see Figure 3-5) lets you set up personal information to be used with your desktop applications, as well as change your password. Clicking on the image icon in the top left corner opens a browser where you can select the image to use. The Faces directory is selected by default with images you can use. The selected image is displayed to the left on the browser. For a personal photograph you can select the Picture folder. This is the Picture folder on your home directory. Should you place a photograph or image there, you could then select it for your personal image. The image will be used in the login screen when showing your user entry. Should you want to change your password, you can click on the Change password button at the top right.

![](img/ab68ea377332b50bf70ef1316c8175b6_104_0.png)

There are three panels: Contact, Address, and Personal Info. The Contact panel you enter email (home and work), telephone, and instant messaging addresses. On the Address panel you enter your home and work addresses, and on the Personal Info panel you list your Web addresses and work information.

## Sessions

You can configure your desktop to restore your previously opened windows and applications, as well as specify startup programs. When you log out, you may want the windows you have open and the applications you have running to be automatically started when you log back in. In effect, you are saving your current session, and having it restored when you log back in. For example, if you are in the middle of working on a spreadsheet, you can save your work, but not close the file. Then log out. When you log back in, your spreadsheet will be opened automatically to where you left off.

Saving sessions is not turned on by default. You use the Sessions preferences dialog’s Session Options panel (System | Preferences | Personal | Sessions) to save sessions. You can save your current session manually, opt to have all your sessions saved automatically when you log out, restoring them whenever you log in.

You can also use the Sessions preferences dialog to select programs that you may want started up automatically. Some are already selected like the Software updater and the SELinux troubleshooter. On the Start Up Programs panel you can select programs you want started, as well as un-select the ones you don’t want.

## Beagle: Searching files

Beagle is a desktop search tool ([**beaglewiki.org**](http://beaglewiki.org)). To start Beagle, select Search from the Places menu. Beagle will search all the files on your system, including images, e-mails, media files, and program source code.

![](img/ab68ea377332b50bf70ef1316c8175b6_105_0.png)

![](img/ab68ea377332b50bf70ef1316c8175b6_105_1.png)

On Fedora, to index files so that they can be searched, Beagle uses extended attributes for file systems, an option specified automatically for ext3 file systems by HAL (the user_xattr option). Beagle runs as the daemon beagled, which you can start or stop using system-config-services or the beagled services script. Keep in mind that Beagle does not run on the root user account, only on ordinary user accounts.

By default Beagle performs indexing automatically in the background. Your home directory is indexed by default. Use the Indexing panel in the Search Preferences window to add other directories, as well as specify which directories to exclude (see Figure 3-6).

![](img/ab68ea377332b50bf70ef1316c8175b6_105_2.png)

FIGURE 3-6 Beagle search

The **beagle-info** tool with the **--status** and **--index-info** options provides information about Beagle's current indexing state. Beagle also allows you to do static indexing of directories that do not change often, instead of constantly performing live background indexing.

For specific kinds of application data like MS Word files, Evolution address books, or Adobe PDF files, you can install supporting tools to let Beagle extract indexing information from them. See beagle-project.org/Optional_prerequisites for a detailed listing. The evolution-sharp tool will let Beagle index e-mail addresses, wvl allows Word files to be indexed, and pdfinfo indexes PDF files, both metadata and text. A Firefox extension will index viewed Web sites. To index metadata from video files, you will have to have MPlayer installed.

## Accessing File Systems, Devices, and Remote Hosts

Removable media such as CD and DVD discs, USB storage disks, digital cameras, and floppy disks will be displayed as icons on your desktop. These icons will not appear until you place the disks into their devices. To open a disk, double-click it to display a file manager window and the files on it.

The desktop will also display a Computer folder. Opening this folder will also list your removable devices, along with icons for your file system and network connections (see Figure 3-7). The file system icon can be used to access the entire file system on your computer, starting from the root directory. Regular users will have only read access to many of these directories, whereas the root user will have full read and write access.

Opening Network will list any hosts on your system with shared directories, like Windows systems accessible with Samba (see Chapter 39). GNOME uses DNS-based service discovery to automatically detect these hosts. Opening a host's icons will list the shared directories available on that system. When opening a shared directory, you will be asked for a user and password, like the user and password for a directory owned by a Windows user. The first time you access a shared directory, you will also be asked to save this user and

![](img/ab68ea377332b50bf70ef1316c8175b6_106_0.png)

**FIGURE 3-7** Removable devices, Computer folder, and shared network folders (ECHO icons)
