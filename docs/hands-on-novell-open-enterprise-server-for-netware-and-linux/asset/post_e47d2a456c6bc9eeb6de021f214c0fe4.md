
## Using NetWare Administrator

To work with the Directory tree, you need to become familiar with Novell’s management utilities. In previous releases of NetWare, creating and managing the eDirectory tree have required running the NetWare Administrator utility on a computer with Novell Client installed. In NetWare 5.0, Novell introduced the ConsoleOne utility, which was written with the Java language so that it could run on multiple platforms, including the NetWare server’s console. With NetWare 6.0, Novell introduced a new network management tool called iManager. Although iManager version 1 could perform only a limited number of tasks, network administrators could use it to manage their eDirectory trees from a Web browser instead of requiring a computer with Novell Client. Because it doesn’t require the Novell client running on a Windows-based computer, iManager is now an integral part of Novell’s NetWare vision, making network management possible from any client computer on a connected network. By default, only the Admin user has rights to use iManager. For other users to run iManager, they need to be assigned to an iManager role by using Novell’s Role Based Services (RBS). You learn more about using RBS in Chapter 7.

Each utility has its advantages and disadvantages. For example, ConsoleOne is a Java-based utility that can be run from multiple OSs, including the server console. NetWare Administrator has the advantage of providing high performance on older Windows-based computers, and iManager has the advantage of being able to be used from any network computer through a standard Web browser. Because of these utilities’ different capabilities, a CNA should be familiar with all three. Although iManager is the primary utility used in this chapter to work with eDirectory objects, you also learn how to use NetWare Administrator and ConsoleOne for network tasks. In Chapter 4, you learned how to use iManager to access and create objects in the eDirectory tree. In the following sections, you learn how to install ConsoleOne and NetWare Administrator, and then use these utilities to access the eDirectory tree structure you created in Chapter 4.

### Activity 5-1: Creating a NetWare Administrator Shortcut

**Time Required:** 5 minutes

**Objective:** Install and configure NetWare Administrator.

**Requirements:** To perform this activity, you need the following:

- A Windows XP computer with Novell Client installed from Chapter 4
- A dedicated server or a classroom server and eDirectory tree shared with other students. Record the following information for your lab environment:
    - Server name:
    - eDirectory tree name:
    - Your assigned administrative user name:
    - The name and context of your UAS Organization:

**Description:** As the network administrator, Eric Kenton has often used NetWare Administrator to set up and maintain the UAS network system when working from older Windows desktops. To make it easier to start NetWare Administrator, Eric creates a Windows desktop shortcut, and then adds NetWare Administrator to the Start menu. In this activity, you learn how to add a NetWare Administrator shortcut to your desktop and your Start menu.

1. If necessary, start your Windows XP computer, and log in to eDirectory with your administrative user name and password.
2. Open the F:\Public\Win32 folder by following these steps:
    a. Double-click **My Computer**.
    b. Double-click the **F:** drive.
    c. Double-click the **Public** folder and then the **Win32** folder.
3. Right-click the **Nwadm32** program, and then click **Send To Desktop (create shortcut)** to create a shortcut on your desktop.
4. Close the Win32 dialog box. A shortcut to Nwadm32 should now appear on your desktop.
5. To add Nwadm32 to your Start menu, right-click **Start**, and then click **Open** to open the Start Menu window.
6. Right-click the **Nwadm32** shortcut on the desktop, and drag it to the Start Menu window.
7. Release the right mouse button, and then click **Copy Here** on the shortcut menu to place a copy of the shortcut in your Start menu.
8. Close the Start Menu window, and stay logged in for the next activity.

### Activity 5-2: Browsing with NetWare Administrator

**Time Required:** 10 minutes

**Objective:** Use NetWare Administrator to browse the eDirectory tree, view object properties, and create new objects.

**Requirements:** Same as Activity 5-1 and completion of Activities 4-1 and 4-2

**Description:** Because of its good performance and capability of opening multiple browse windows, Eric periodically uses NetWare Administrator to manage his tree structures. In this activity, you learn how to start NetWare Administrator, open multiple browse windows, change the context, and view objects in the eDirectory tree.

1. Start NetWare Administrator by clicking **Start, All Programs, Shortcut to Nwadm32**. The NetWare Administrator utility has a number of toolbar buttons for various tasks, as shown in Figure 5-1. If necessary, read the tip in the Welcome to NetWare Administrator window, and then click **Close**.
2. After NetWare Administrator is started, you see a browse window similar to the one in Figure 5-2.
3. Close the browse window by clicking the **Close** button.
4. Open a browse window to the root of the tree by following these steps:
    a. To open a new browse window, click **Tools, NDS Browser** from the menu to open the Set Context dialog box. Notice that the Context text box displays your computer's current context in UAS_Tree.

![](img/840007e8f98ea6653e5877e945c27dc6_187_0.png)

Figure 5-1 The NetWare Administrator toolbar

![](img/840007e8f98ea6653e5877e945c27dc6_187_1.png)

Figure 5-2 The NetWare Administrator browse window

    b. Click the **browse** button next to the Context text box to open the Select Object dialog box shown in Figure 5-3. The Browse context section on the right is used to change your current context. The Available objects section on the left lists objects in the selected context.

![](img/840007e8f98ea6653e5877e945c27dc6_188_0.png)

**Figure 5-3** The NetWare Administrator Select Object dialog box

    c. To move your current context up one level, double-click the **up arrow** in the Browse context section. All objects in the [Root] container of the tree are then displayed in the Available objects section.
    d. To set the context of the Browse context section to the root of the tree, double-click the [Root] object in the Available objects section.
    e. Click **OK** to save the new context setting. The browse window should now display all the Organization containers.
    f. Record the names and types of all Organization objects displayed in the browse window:
        ______
        ______
        ______
5. View all objects in the UAS container. If you’re using a dedicated server, simply double-click **UAS** in the browse window. If you’re using a shared classroom server, expand the **CLASS** Organization and then double-click the **UAS** OU. Record the names of all Organizational Unit objects in the UAS container:
    ______
    ______
    ______
6. Record the names of all group objects in the UAS Organization:
    ______
    ______
    ______
7. Double-click the **UAS** container to collapse it.
8. Close NetWare Administrator by clicking **Object, Exit** from the menu, and stay logged in for the next activity.

## Using ConsoleOne

ConsoleOne remains the primary Windows-based utility for managing most aspects of the NetWare 6.5 eDirectory tree. In addition to having Novell Client installed, ConsoleOne requires at least 128 MB of RAM and a 300 MHz processor to run effectively. Although the ConsoleOne software can be run directly from the SYS volume of the NetWare 6.5 server, loading ConsoleOne files across the network is slower and uses up network bandwidth. Starting ConsoleOne is much faster if you install it on your local computer. In the following activities, you install ConsoleOne on your Windows desktop, and then practice using it to browse the Universal AeroSpace tree.
