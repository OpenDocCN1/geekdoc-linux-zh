
## Activity 14-10: Creating Storage Location Objects

**Time Required:** 15 minutes

**Objective:** Use iManager to create a Storage Location object.

**Requirements:** Internet Explorer from Windows XP or Java-enabled Firefox from SUSE Linux 10

**Description:** Eric wants users to be able to access their home directories from NetStorage. In this activity, you make user home directories available by using iManager to create a Storage Location object for user home directories.

- Log in to your Windows XP system with your local administrator user name and password or your SUSE Linux server with the root user name and password.
- Start your Web browser, start iManager, and log in to iManager with your administrative user name and password.
- Expand the **File Access (NetStorage)** heading and click the **New Storage Location** link to display the *Storage Locations: Create Object* window shown in Figure 14-16.
- In the *Object Name* text box, type **storLoc_hostname** (replacing *hostname* with the name of the SUSE Linux server).
- In the *DisplayName* text box, type **home**. This is the name that’s displayed in the user’s NetStorage window.
- In the *Directory Location* text box, type **ssh:/IPaddress/home** (replacing *IPaddress* with the IP address of your SUSE Linux server).
- Click the **Object Selector** button next to the Context text box, and navigate to and click your **UAS** container.
- Click **Create** to create the object and return to the iManager main window.
- Exit iManager and stay logged in for the next activity.

![](img/840007e8f98ea6653e5877e945c27dc6_593_0.png)

Figure 14-16 Creating a Storage Location object

## Activity 14-11: Accessing NetStorage

**Time Required:** 15 minutes

**Objective:** Use NetStorage to access the SUSE Linux server.

**Requirements:** Completion of Activity 14-8 and a Windows XP or SUSE Linux 10 computer

**Description:** In this activity, you test NetStorage by using your Web browser to log in with your LUMUser name and password.

- If necessary, log in to your **Windows XP** system with your local administrator user name and password or your **SUSE Linux** server with the root user name and password.
- Start your Web browser and enter the URL `https://IPaddress/NetStorage` (replacing *IPaddress* with the IP address of your SUSE Linux server).
- Log in to NetStorage with your LUMUser user name and password.
- List the files and directories you can see: _______________________________
- Exit NetStorage, and leave your system running for the next activity.

## IPRINT SERVICES IN SUSE LINUX

The iPrint system can be used in SUSE Linux as well as NetWare 6.5, as shown in Figure 14-17. A printer can be installed on a Linux, Windows, or Macintosh computer using HTTP or the local operating system's native printer installation. When using HTTP, the Web browser on the computer directs the request to the printer page installed on the iPrint server. The OES server then uses the Driver Store object in Linux or the Broker object in NetWare to send the correct printer driver to the computer.

After a printer is installed, print jobs are sent via the IPP protocol to the Print Manager software, which uses a print spooler to direct the print job to a network-attached printer. The major difference between iPrint in Linux and NetWare is that you must create a **Driver Store** object on the SUSE Linux system for storing print drivers. This object replaces the Broker object used in NetWare. These are the basic steps for setting up iPrint in SUSE Linux:

- Create a Driver Store.
- Add print drivers to the Driver Store from the Windows platforms.
- Create a Print Manager object.
- Create iPrint printer objects.

In the following activities, you set up iPrint on your SUSE Linux system.

![](img/840007e8f98ea6653e5877e945c27dc6_594_0.png)

**Figure 14-17 Using iPrint in SUSE Linux**

## Activity 14-12: Creating a Driver Store

**Time Required:** 10 minutes

**Objective:** Use iManager to set up the iPrint service.

**Requirements:** Internet Explorer from Windows XP or Java-enabled Firefox from SUSE Linux 10

**Description:** The AeroDyn Division needs access to several network printers from both inside and outside the company network. In this activity, you learn how to create a Driver Store for setting up iPrint on the SUSE Linux server.

- If necessary, log on to your Windows XP or SUSE Linux computer with your administrative or root user name and password.
- Start your Web browser, start iManager, and log in to iManager with your administrative user name and password.
- Follow these steps to create a Driver Store object for holding print drivers:
  - Expand the **iPrint** heading and click the **Create Driver Store** link to display the *Create Driver Store* window shown in Figure 14-18.

![](img/840007e8f98ea6653e5877e945c27dc6_595_0.png)

**Figure 14-18** The *Create Driver Store* window

  - If necessary, enter a container name by clicking the **Object Selector** button next to the Container name text box and clicking your **UAS** container.
  - In the Driver Store name text box, type **UASPrint_Drivers**.
  - Enter the IP address of your Linux server in the Target Server text box.
  - Click the **Object Selector** button next to the eDir Server name text box, and click your SUSE Linux server.
  - Click **OK** to create the Driver Store and display the completion message.

> **NOTE** The following steps need to be performed from a Windows XP client.

- If necessary, use the following steps to install the iPrint client on your Windows XP computer. (If you installed the iPrint client in Chapter 8, you can skip to Activity 14-13.)
  - If necessary, log on to your Windows XP computer and click the **Workstation Only** check box.
  - Start Internet Explorer and enter the URL `http://IPAddress/ipp` (replacing *IPAddress* with the IP address of your SUSE Linux server).
  - Click the **Install iPrint Client** link.
  - Click the **Open** option to start the installation wizard.
  - When the Install iPrint Client window is displayed, click **Next** to start the installation process.
  - After the client is installed, click **Finish** to return to the iPrint window. Close your Web browser.
- Leave iManager open for the next activity.

## Activity 14-13: Creating a Print Manager Object

**Time Required:** 10 minutes

**Objective:** Use iManager to set up the iPrint service.

**Requirements:** A Windows XP or SUSE Linux 10 computer; completion of Activity 14-12

**Description:** In this activity, you learn how to create a Print Manager for setting up iPrint on your SUSE Linux system.

- If necessary, expand the **iPrint** heading and then click the **Create Print Manager** link to display the Create Print Manager window (see Figure 14-19).

![](img/840007e8f98ea6653e5877e945c27dc6_596_0.png)

- Type **OES_PMgr** in the Print Manager name text box.
- Click the **Object Selector** button next to the eDir Server name text box, and click your SUSE Linux server.
- Click the **Object Selector** button next to the Driver Store name text box, and click the **UASPrint_Drivers** object you created in Activity 14-12.
- Click the **IP Address** option button, and enter the IP address of your SUSE Linux server in the text box.
- Click **OK** to create the Print Manager object, and leave iManager open for the next activity.

## Activity 14-14: Creating Printer Objects

**Time Required:** 10 minutes

**Objective:** Use iManager to set up the iPrint service.

**Requirements:** Completion of Activity 14-13

**Description:** In this activity, you learn how to create printer objects that can be used to set up iPrint on your SUSE Linux system.

- If necessary, expand the **iPrint** heading and then click the **Create Printer** link to display the Create Printer window shown in Figure 14-20.
- In the Printer name text box, enter **OES_P1**.
- Enter the appropriate information for your printer, and click **Next** to create the printer object.
- Close any open windows, and log off.
