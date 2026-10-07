
# 170 About Synchronizing a Handheld Device with Evolution

device and Evolution. You must specify the port type (Serial, USB, for example) and the actual port that will be used for the Palm to Evolution communication. The default is /dev/pilot, but other ports such as ttyUSB0 or ttyUSB1 can be used.

# NOTE

You need read and write access to connect to a port such as a USB or serial port. So, connecting a handheld device to an NLD system when you are not running as root, poses some of the same problems that burning CDs or DVDs do (meaning root privileges are required to access devices). You can use commands such as own and chmod at the command line, when logged in as root using the su (superuser) command, to gain access to ports. For example, you can run the command chmod 777 /dev/tty0 to access the first USB port on a system. Successfully connecting to a Palm device may require help from your system administrator or require some additional research on your part to get the Palm device and your system talking when you are not logged in to the system as root.

Specify the port and port type for the communication between the Palm device and Evolution.

![](img/6e85ebc4ce06a64c82109523b60183ba_400_0.png)

After the port and port type are specified, the wizard walks you through the steps of synchronization with the Palm device for the first time. You can specify whether you have synced the device with other groupware software in the past or are synchronizing the device with a groupware product (such as Evolution) for the first time. In either case, a username and unique ID are negotiated between the handheld device and your system.

# CHAPTER 15: Staying Organized with Novell Evolution

After your system and the handheld device have been synchronized for the first time, you can configure the conduits that allow you to synchronize email, appointments, or tasks between Evolution and the Palm device. You can access the Pilot Settings (including the conduit settings) by selecting Tools, Pilot Settings from the menu after you have run the initial synchronization.

The Pilot Settings dialog box provides three tabs: Pilots, Devices, and Conduits. The Pilots tab lists the device that was identified during the initial synchronization. The Devices tab shows the cradle and communication port (such as a USB port) that was configured by the Gnome-Pilot Wizard.

The Pilot Settings dialog box shows the settings that were configured when you ran the Gnome-Pilot Wizard.

![](img/6e85ebc4ce06a64c82109523b60183ba_401_0.png)

The Conduits tab is used to configure how Evolution and the handheld device share information. You will have different conduits listed on the Conduit tab such as EAddress, which is for synchronizing the address book, and Ecalendar, which is used for synchronizing your appointments. You select a conduit and then enable it by selecting the Enable button. To configure the conduit, you select the conduit (such as EAddress) and then select Settings. Selecting Settings opens a Conduit Settings dialog box for the selected conduit.

You then must determine how you want Evolution and the handheld device to handle the information shared during subsequent synchronizations. In the Conduit Settings dialog box you select the Action drop-down list. You can then select from the following:

386

- Synchronize—New data is shared between Evolution and the device (no matter where the new information resides), and information deleted in Evolution or the Palm device is removed from Evolution and the hand-held device.

- Copy from Pilot—New information is copied from the Palm device to Evolution.

- Copy to Pilot—New information is copied from Evolution to the Palm device.

- Merge from Pilot—New data is copied to Evolution, and any data deleted on the handheld device is also deleted from Evolution.

- Merge to Pilot—New data is copied to the handheld device from Evolution, and any information that has been deleted from Evolution is also deleted from the handheld device.

Conduits are configured to determine how information is dealt with during the synchronizing of Evolution and the handheld device.

![](img/6e85ebc4ce06a64c82109523b60183ba_402_0.png)

Configure all the conduits that you want to synchronize. You can then synchronize Evolution and your Palm device as needed. After you have configured your conduits, you can synchronize Evolution and your handheld device as needed by pressing the sync button on your handheld device's cradle.

# Delete Evolution Items

The end result of deleting items in Evolution really depends on the item you are deleting. Deleted messages are placed in the Trash folder. This allows you to recover the message if it has been deleted inadvertently. When you delete contacts, appointments, and tasks, you aren't really given a second chance in terms of recovering the deleted item. They are removed from Evolution completely.

# CHAPTER 15: Staying Organized with Novell Evolution

![](img/6e85ebc4ce06a64c82109523b60183ba_403_0.png)

# Delete Message

With the Inbox selected, right-click on any message and select Delete from the shortcut menu. The message is deleted from the Inbox.

TIP

You can select multiple messages and then delete them by pressing the Delete key.

388

# View Messages in Trash Folder

Select the Trash folder. Deleted messages are held in the Trash folder until you empty or exit.

To configure Evolution to automatically empty the folder, go to the Mail Preferences. Select the Empty Folders on Exit check box on the General tab.

When you delete items such as appointments or tasks, you don't have the luxury of recovering them. To undelete a message in the Trash folder, right-click on the message and select Undelete.

# Delete Appointment

With the Calendars selected, right-click on an appointment on the daily calendar. Select Delete from the shortcut menu.

# Confirm Appointment Deletion

An Evolution dialog box opens that lets you know the item will be permanently deleted; select Delete to remove the item.

# Using Novell iFolder

- 172 About Novell iFolder
- 173 Start the iFolder Client
- 174 Access iFolder from the Desktop
- 175 Access Your iFolder from a Web Browser
- 176 About Synchronizing Files
- 177 Manually Synchronize Files
- 178 View Files in the iFolder Bin
- 179 Set iFolder Preferences

# CHAPTER 16: Using Novell iFolder

Having the ability to access important files from any computer, even a computer that is not running NLD, provides a number of possibilities for working on the road and collaborating with other users. Novell iFolder is a network service that allows you to access a dedicated iFolder from any workstation running NLD or from any computer's web browser. This chapter provides a basic overview of the client side of iFolder.

# 172 About Novell iFolder

Novell iFolder is a network and Net service that allows you to access a personal folder on a server (the iFolder server can be a NetWare, SUSE, or Microsoft Windows server configured with the iFolder service). The items in the local folder are synchronized with your iFolder on the server. This provides seamless access to the files that you need as if they exist locally, and it also backs up these files in iFolder on the server.

You can access your folder on the iFolder server from any computer that provides access to an iFolder client. NLD provides an iFolder client that is installed during the NLD installation.

In cases where you have access to a computer but not to an iFolder client, you can access your iFolder from any computer that has a web browser. As files are moved over the network and/or the Internet, they are encrypted, protecting your data.

# 173 Start the iFolder Client

The iFolder client is the easiest way to access your online iFolder. The client software is installed by default during the NLD installation.

+ 1 Start iFolder Client
From the NLD desktop, select Programs, Accessories, Novell iFolder. The Login dialog box opens.

+ 2 Enter Logon Information
Enter your user ID, password, and the name of the iFolder server. After you have completed entering the information, select Login. The first time you log in, the Novell iFolder Location dialog opens.
