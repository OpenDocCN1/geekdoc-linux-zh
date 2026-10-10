
19. Click the **IP** check box and enter the IP address and mask for the NetWare 6.5 server that you wrote down earlier on your NetWare Server Installation Planning form. If selected, configure **IPX** as defined on your NetWare Server Installation Planning form.

20. Click **Next** to display the Domain Name Service window. If there's no DNS server on the local network, leave all fields blank and click **Next**. When you receive a warning message stating that some services have limited functionality without the DNS service, click **OK** to continue.

21. Next, select your time zone and click **Next** to initialize the eDirectory service and display the eDirectory Installation window.

22. Click the **Create a new eDirectory tree** option button, and then click **Next** to display the eDirectory Installation window shown in Figure 2-13.

![](img/840007e8f98ea6653e5877e945c27dc6_68_0.png)

23. Enter the name of your eDirectory tree (the one you wrote down on your NetWare Server Installation Planning form) in the Tree Name text box and your Organization name in the Context for Server Object text box. Enter a password for your Admin user in the Password and Retype Password text boxes, and then click **Next** to install eDirectory and display the eDirectory Summary window. Record the information from this window on your NetWare Server Installation Planning form, and then click **Next** to display the Licenses window.

24. The Licenses window can be used to install licenses for the NetWare 6.5 server and users during server installation. License files have an .nf extension and can also be installed after server installation by using iManager as described in Chapter 5. Click the browse button to locate the license certificate on your floppy disk, and then add it to the License(s) to be installed list box (see Figure 2-14).

> **NOTE** A sample MLA license certificate for evaluation purposes is included on the NetWare 6.5 Products CD in the license\eval folder.

25. Click **Next** to display the MLA License Certificate Context window. You use the Select the NDS context text box to specify the context where licenses are installed. The licenses are then valid for all users in the selected context and below. Verify that the context is set to your UAS Organization, and then click **Next** to install the licenses and display the LDAP Configuration window.

26. Record the default clear text and SSL/TLS port numbers on your NetWare Server Installation Planning form, and then click **Next** to accept the default port settings and display the Novell Modular Authentication Service (NMAS) window shown previously in Figure 2-6.

![](img/840007e8f98ea6653e5877e945c27dc6_69_0.png)

**Figure 2-14** The Licenses window

27. To provide for all login methods, click the **Select All** button and then click **Next**. The installation program continues by configuring each selected service.

28. When prompted, restart your server. Congratulations! Your NetWare 6.5 server is now ready for use.

29. To shut down your NetWare server correctly, press **Ctrl+Esc** on the server console to display the console selection menu, and then select the **System console** option to display the console prompt. The following section describes using the NetWare server console and commands.

30. Type the command **DOWN** and press **Enter**. When the DOS prompt is displayed, you can safely power off your server. (You learn more about the DOWN and EXIT commands in the following section.)

## WORKING WITH THE SERVER CONSOLE

As described in the “Preparing for NetWare 6.5 Installation” section, a NetWare server contains at least two disk partitions: one for DOS and one for NetWare. A NetWare server starts first from the DOS partition (C: drive). As shown previously in Figure 2-1, the NetWare server consists of the Server.exe kernel software and modules that are loaded to provide services. The Server.exe kernel supplies the core NetWare services, such as file sharing, and provides a software bus for NetWare Loadable Modules and Java applications. Most network services, such as Novell Distributed Print Services (NDPS) and Novell eDirectory, and device drivers are provided by software modules called **NetWare Loadable Modules (NLMs)**, which are loaded during or after the server startup process.

To start the NetWare server, you begin by running the Server.exe program from the DOS partition. During installation, the Server.exe program, its support files, and its disk driver modules are stored on the DOS boot partition in the C:\Nwserver directory. If you selected to start the server automatically during the installation process, the commands needed to start the server are placed in the Autoexec.bat file. When the computer starts, DOS automatically performs the commands placed in the Autoexec.bat file. For example, the following commands were placed in the Autoexec.bat file of the UASHOST server:

```
C:\>cd nwserver
C:\nwserver>server
```

As the Server.exe program is loading, it reads commands from the Startup.ncf file, also located in the C:\Nwserver directory. This file contains the names of the disk drivers and other configuration commands, as shown in Figure 2-15.

![](img/840007e8f98ea6653e5877e945c27dc6_70_0.png)

**Figure 2-15** A sample Startup.ncf file

After Server.exe has loaded its disk drivers, it mounts the SYS volume and continues to read commands from the Autoexec.ncf file stored in the System directory of the SYS volume. As shown in Figure 2-16, the Autoexec.ncf file contains commands that identify the server's name, internal address, and any NLMs, such as the network card drivers, that must be loaded for server operation.

![](img/840007e8f98ea6653e5877e945c27dc6_70_1.png)

**Figure 2-16** Reading commands from the Autoexec.ncf file

After startup, the server console displays the Novell Open Enterprise Server screen. You can change the background of the GUI screen by clicking Novell, pointing to Settings, and then clicking Backgrounds. In addition to the GUI console, the NetWare 6.5 servers has a text-based console screen and console screens for several modules. You can flip between console screens with the Alt+Esc key combination, or you can select a console screen by pressing Ctrl+Esc to display all consoles and then enter the number of the screen you want to display (see Figure 2-17).

![](img/840007e8f98ea6653e5877e945c27dc6_70_2.png)

**Figure 2-17** Selecting a NetWare console

For example, to change to the System Console screen, press Ctrl+Esc to display the list shown in Figure 2-17. Type 1 and press Enter to display the console prompt showing the server name followed by a colon. You can use the System Console screen to enter console commands and load modules as described in the following sections.

### Console Commands

To become a CNA and effectively operate a server console, you need to know how to use the basic **console commands** built into the NetWare operating system. Table 2-2 summarizes the purpose of the server console commands, and the following sections describe some of these commands in more depth and provide examples of using them to perform server operations. In Activity 2-3, you practice using console commands.

Table 2-2 Essential console commands

| Command Syntax | Description |
| :--- | :--- |
| BIND protocol TO<br>driveboard_name<br>(drive_<br>parameters) | Attaches a protocol to a LAN card. Replace protocol with the protocol name (IPX or IP, for example). Replace driveboard_name with the name of the NIC or an optional name assigned to the network card. You can optionally replace drive_parameters with the hardware settings that identify the NIC (such as I/O port and interrupt). |
| LOAD path/module_name<br>(parameters) | Loads an NLM in the file server’s RAM. Optionally replace path with the DOS or NetWare path leading to the directory containing the module to be loaded. Replace module_name with the name of the NLM you want to load. Optional parameters can be entered depending on the module being loaded. |
| CONFIG | Displays configuration information about each NIC, including hardware settings, network address, protocol, and frame type. |
| DISPLAY servers | Displays all servers in the file server’s IPX router table, including the number of routers (hops) to get to each server. This command is not available unless IPX is selected during server installation. |
| MEMORY | Displays the total amount of memory available to the file server. |
| SET time | Allows you to change the file server’s current system date and time. |
| CLS/OFF | Clears the file server console screen. |
| DISABLE /ENABLE LOGIN | Prevent or enable new user logins. |
| BROADCAST | Send the specified message to all currently logged-in users. |
| DOWN | Closes all files and volumes, disconnects all users, and takes the file server offline. |
| MOUNT volume_name<br>(ALL) DISMOUNT volume_<br>name | Places a volume online or offline. Replace volume_name with the name of the volume you want mounted, or use ALL to mount all NetWare volumes. |
| MODULES | Lists all currently loaded modules starting with the last module loaded. |
| SEARCH (ADD/DEL) | Displays and updates the paths where the server will look for modules. Use this command to add and delete paths for loading modules. |
| SECURE CONSOLE | Provides additional security to help protect the server from unauthorized access. |
| SEND "message" (TO)<br>user_name/connection_<br>number | Sends a message to a specified user. Replace message with a message line you want sent and replace user_name/connection_number with the name of the currently logged-in user or the connection number assigned to the user. The connection_number can be obtained from the Connection option of the MONITOR NLM. |
