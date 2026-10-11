
With the correct driver in place, the user can submit a print job. The iPrint Client receives the job from the Windows spooler and submits it to the iPrint Manager (3). The iPrint Manager waits for the printer to become available and then sends the job to the Printer Agent for the laser printer (4). The job is then printed on the printer.

Let’s look at how you go about installing and configuring iPrint on your NNLS server.

## Installing and Configuring iPrint

**Test Objective Covered:**

- 3. Install and configure iPrint.

As with the NNLS components discussed in the previous chapter, the CLE objectives require you to know how to install and configure iPrint. Just as with these other products, we’re not going to spend a great deal of time discussing how to install the iPrint service because NNLS installation procedures and dependencies were presented in depth in Chapter 5, “NNLS Installation and Administration.” Instead, we will focus on installing the iPrint Client and configuring the iPrint service in this chapter.

### Installing the iPrint Service

If you performed an Express NNLS installation, iPrint was installed on your system. If you performed a Custom install, you had the opportunity to select the iPrint component for installation.

If you didn’t select iPrint during the initial installation of NNLS, you can perform a post-installation by completing the following steps:

1. Mount your NNLS ISO image.
2. Run the `install.sh` script.
3. When prompted, specify a Custom installation.
4. When prompted to select the products to be installed, deselect all products.
5. Select iPrint.
6. Finish the installation according to the instructions presented in Chapter 5.

During the installation process, the iPrint system files are copied to the following directories in your server's file system:

- `/var/opt/novell/iprint` — This directory holds print jobs as they are spooled to the iPrint Manager.
- `/var/opt/novell/log` — This directory contains the iPrint system log file (`ipsmd.log`).

> Be aware that the Novell Apache web server installed with NNLS has the **Access Logging** directive in the configuration file enabled. If your iPrint system is heavily used, it is theoretically possible for the logs created by the web server to fill up your disk, thus bringing your system to a stop. You should periodically delete the old log files or disable Access Logging in the conf file.

- `/var/opt/novell/httpd/htdocs/ippdocs` — This directory contains your system's printer maps.
- `/etc/opt/novell/iprint/` — This directory contains the configuration file for the iPrint daemon (`ipsmd.conf`).

### Installing the iPrint Client

As mentioned earlier, Novell only provides an iPrint Client for Windows workstations at the present time. There are rumblings that an iPrint Client for Linux will become available in future releases. We'll have to wait and see if that actually happens.

For now, let's talk about how the iPrint Client is installed on Windows workstations. As with the iFolder Client we discussed earlier in this book, Novell makes the client software for iPrint available on the iPrint website that is installed by default on your server when you install NNLS.

This makes your job as an administrator very easy. Instead of having to run around to all the PCs in your company with a stack of CDs, the end user can simply access this website and download the required client software.

It also makes the required software easily accessible to remote users. Recall the scenario introduced at the beginning of this chapter. Odds are that the employee working from home at 2:00 in the morning will not have a CD with client software handy. Putting the client software on the iPrint website makes it available to any employee who needs it when he or she needs it.

To install the iPrint Client, you need to do the following:

1. On your Windows workstation, open a web browser and navigate to **http://your_server_IP_address/ipp**. If you don't have the iPrint Client installed, the dialog in Figure 9.2 is displayed.

![](img/c7771e8540507f2b00c088c7a411b57b_422_0.png)
![](img/c7771e8540507f2b00c088c7a411b57b_422_1.png)

2. When prompted to install the iPrint Client, click **OK**.
3. In the **File Download** dialog, click **Open**.
4. If prompted that the web page is trying to close the browser window, click **Yes**. The **Novell iPrint Client Setup** screen appears, as shown in Figure 9.3.

![](img/c7771e8540507f2b00c088c7a411b57b_422_2.png)
![](img/c7771e8540507f2b00c088c7a411b57b_422_3.png)

5. Click **Next**. The client files are copied as shown in Figure 9.4.
6. When the file copy is complete, the **Install Complete** screen is displayed, as shown in Figure 9.5. Click **Finish**.
7. Shut down and restart the workstation.

Let's now talk about how to configure your iPrint implementation.

**FIGURE 9.4**
iPrint Client file copy.

![](img/c7771e8540507f2b00c088c7a411b57b_423_0.png)

**FIGURE 9.5**
iPrint Client installation complete.

![](img/c7771e8540507f2b00c088c7a411b57b_423_1.png)

## Configuring iPrint

In order to configure your iPrint system, you need to complete a series of tasks. These include the following:

- Configuring the Driver Store
- Configuring the iPrint Manager
- Configuring Printer Agents
- Creating location-based print maps

Let's look at the first task: configuring your system's Driver Store.

### Configuring the iPrint Driver Store

As we discussed earlier, the iPrint Driver Store contains the drivers for the printers serviced by your iPrint Manager. However, the Driver Store is not created during the installation of iPrint. You must create it manually with iManager. To do this, follow these steps:

1. Open a web browser and navigate to `https://your_server_IP_address/nps/iManager.html`.
2. Authenticate as your **admin** user.
3. In the left frame, scroll down to the **iPrint** role, shown in Figure 9.6.

![](img/c7771e8540507f2b00c088c7a411b57b_424_0.png)

**FIGURE 9.6**
iPrint role in iManager.

4. Select **Create Driver Store**. The screen in Figure 9.7 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_424_1.png)

**FIGURE 9.7**
Creating a Driver Store.

5. In the **Driver Store** name field, enter a name for your Driver Store object in the eDirectory tree.
6. In the **Container** name field, enter the container where you want your Driver Store object to reside.
7. In the **Target Server** field, enter the IP address of your iPrint server.
8. In the **eDir Server** field, browse to and select the server object for your NNLS server in the eDirectory tree.
9. Click OK.
10. When prompted that the Driver Store object has been created, click OK.

After completing this process, you will see a new *Driver Store* object in your eDirectory tree. In Figure 9.8, a *Driver Store* object named CLEDriverStore has been created in the IFCLE container.

**Figure 9.8**
Driver Store object in the eDirectory tree.

![](img/c7771e8540507f2b00c088c7a411b57b_425_0.png)

With the Driver Store object created, the next task you need to complete is to add printer drivers to the Driver Store. By default, NNLS doesn’t provide any printer drivers, as shown in Figure 9.9.

**Figure 9.9**
No drivers in the Driver Store.

![](img/c7771e8540507f2b00c088c7a411b57b_425_1.png)

Before you can deploy iPrint, you must upload the appropriate drivers for your printers into the Driver Store object. Using iManager, you can upload drivers in two ways:

- You can upload drivers from a driver floppy disk, from a CD-ROM, or from files downloaded from the Internet.
- You can upload drivers directly from the Windows operating system’s set of drivers.

To upload drivers, you must access iManager using Internet Explorer. You can’t use Mozilla or Netscape Navigator. You must also access iManager from a workstation that already has the iPrint Client installed. Once these conditions are met, you can upload a driver by doing the following:

1. From a Windows workstation, open Internet Explorer and navigate to `https://your_server_IP_address/nps/iManager.html`.
2. Expand the **iPrint** role in iManager.
3. Select **Manage Driver Store**. The screen in Figure 9.10 is displayed.

![](img/c7771e8540507f2b00c088c7a411b57b_426_0.png)

**FIGURE 9.10**
Selecting the Driver Store to manage.

4. In the **iPrint Driver Store name** field, browse to and select your Driver Store object; then click **OK**. The screen in Figure 9.11 is displayed.

![](img/c7771e8540507f2b00c088c7a411b57b_426_1.png)

**FIGURE 9.11**
Managing the Driver Store.

5. Select the **Drivers** tab.
6. Select the operating system you want to upload a printer driver for. In Figure 9.12, the screen for Windows XP driver upload is displayed.
