
## Activity 2-6: Managing Volumes and Commands

1. If necessary, follow the steps in Activity 2-5 to start Remote Manager.
2. In the main window, click the **Volumes** link under the Manage Server heading to display the Volume Management window showing the status of all volumes. Record the names and attributes of the first four volumes:
3. Click the **Console Commands** link to display a list of all console commands.
4. Click the **Info** icon next to these commands: CONFIG, CLEAR STATION, and CLS. Record the description of each command and the sample command shown in the Info window:
5. Click the **View Memory Config** link to display the View Memory Config window. Record the total system memory size and current cache memory:
6. Stay logged in and leave Remote Manager open for the next activity.

## Activity 2-7: Viewing the Server Hardware Environment

**Time Required:** 10 minutes

**Objective:** Use Remote Manager to view hardware information.

**Requirements:** Same as Activity 2-5

**Description:** Using Remote Manager, you can view your server's current hardware configuration settings, which is useful when diagnosing problems or planning for new equipment. For example, at Comdex Eric found a 1 GB network card that he wanted to install in the UASHOST server. He used Remote Manager to view the server's hardware configuration so that he could check the slots and interrupts to determine the feasibility of installing the new network card. In this activity, you use the options under the Manage Hardware heading to document your server's available ports and interrupts.

1. If necessary, follow the steps in Activity 2-5 to start Remote Manager.
2. Scroll down the navigation pane to the Manage Hardware heading, and record the options under this heading:
3. Click the **Processors** link to display the Processor Information window. Record the processor information here:
4. Under the Manage Hardware heading, click the **Disk/LAN Adapters** link.
5. Click the **Info** icon next to Network Adapter. Record the interrupt, slot, and ports used by your network adapter:
6. Under the Manage Hardware heading, click the **Other Resources** link to display the Hardware Resources window.
7. Click the **Interrupts** option to display the Hardware Resources/Interrupts window. List the interrupts in use and any available or unused interrupts:
8. Click the **Exit** button, and, if necessary, click **Yes** to close the Remote Manager window.

### Using Java on the Server

One of the features of NetWare 6.5 is that the server is a highly efficient environment for running Java applications. The Java language, developed by Sun Microsystems, can be used to develop Internet applications that run on multiple platforms, including Web browsers such as Netscape. Having the capability to run Java applications opens up many possibilities for running client-server applications on the NetWare server in the future. A client-server application is one in which at least part of the application runs on the server, and the user interface component runs on the client computer. The major reason many organizations install servers is their capability to run server-based software. NT/2000-based applications are typically limited to the Microsoft platform, but one of the strengths of Java applications is their capability to run on multiple platforms. As a result, many Internet and client-server applications are developed in Java to take advantage of OS platform independence. As one of the most powerful and fastest Java machines, NetWare 6.5 is in a good position to be a preferred choice for running Java applications over the Internet as well as on company intranets.

Running Java applications on the server console requires extra hardware resources. Novell recommends at least 256 MB of RAM, a PS/2 or serial mouse, and a PCI video card that conforms to the VESA 1.2 or later specification. If your video card does not meet VESA 1.2 standards, NetWare loads a default driver that supports only 640 × 480 resolution with 16 colors. JAVA.NLM is loaded automatically along with the X Server graphical console when your server starts. If you're not using any Java-based applications, after your server starts, you can exit the GUI interface and unload the Java language by entering the UNLOAD JAVA command at the server console screen.

### Using the NetWare GUI Interface

With NetWare 6.5, Novell has included a Java GUI console interface. The GUI platform is provided by an implementation of X Window, allowing Java programs that conform to the Abstract Windowing Toolkit (AWT) to be displayed with the X Window interface. To load GUI support, type the STARTX command at the server console. Although the NetWare GUI is not intended to be a full-fledged desktop computer, it does provide a graphical way to interact with the NetWare console. For example, Eric used the GUI interface to install the WebAccess product by following these steps:

- 1. After using the STARTX command to display the GUI console, Eric clicked the Novell button to display a menu containing options for Console One, Install, Programs, Utilities, Settings, and Run.
- 2. Then he clicked the Install option to display a list of products already installed.
- 3. To install additional products, he clicked the Add button and entered the path to the installation CD.
- 4. Then he selected the product he wanted to install and clicked Next to display a product summary window. He explained that you can customize any of the selected products by highlighting the product and clicking the Customize button.
- 5. After completing his customizations, he clicked the Finish button to install the selected product, and then restarted the server as prompted. He noted that if any users are logged in, you should be sure to enter the DISABLE LOGIN command and broadcast a message before shutting down the server.

![](img/840007e8f98ea6653e5877e945c27dc6_88_0.png)

The GUI interface can also be used to configure video resolution, background, and keyboard configurations and to run the ConsoleOne utility, which gives administrators a way to work with eDirectory objects and the file system from the server console so that they don't have to return to client computers to create a user or copy a file, for example. You learn more about working with ConsoleOne in future chapters. In past versions of NetWare, it was necessary to perform all file and user maintenance from a Windows computer running the Novell client and the NetWare Administrator utility.

## Modifying Server Startup Files

When the server first starts, it runs commands from the Start-up.ncf and Autoexec.ncf startup files to load drivers, set configuration parameters, and load NLMs. Sometimes a network administrator must modify commands in startup files to perform such functions as modifying the server's IPX network address, preventing the GUI console from loading automatically when the server starts, or adding modules such as NDPS Broker and Manager to the startup process. To view and modify startup files from the server console, you use the Nwconfig utility. In Activity 2–8, you use this utility to view and modify the contents of the Autoexec.ncf file.

## Activity 2-8: Viewing the Server Startup Files

**Time Required:** 10 minutes

**Objectives:** Use the Nwconfig utility to view file server startup files.

**Requirements:** Access to the NetWare 6.5 server console

**Description:** Because the graphical console isn’t used often, Eric would like you to modify the server’s Autoexec.ncf file to prevent automatic loading of the graphical environment in an effort to improve server performance. In this activity, you use the Nwconfig utility to disable loading the graphical environment.

- 1. From the server console, press **Ctrl+Esc** to display the Current Screens menu.
- 2. Type **1** to select the System Console option, and then press **Enter** to display the System Console command prompt.
- 3. Type the **NWCONFIG** command and then press **Enter** to display the NetWare Configuration menu shown in Figure 2-30.

![](img/840007e8f98ea6653e5877e945c27dc6_89_0.png)

Figure 2-30 The NetWare Configuration menu

- 4. Press the **down arrow** to highlight NCF files Options, and then press **Enter** to display the Available NCF Files Options menu shown in Figure 2-31.

![](img/840007e8f98ea6653e5877e945c27dc6_89_1.png)

Figure 2-31 The Available NCF Files Options menu
