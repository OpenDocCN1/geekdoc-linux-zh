**Description:** The AeroDyn Division needs access to several network printers from both inside and outside the company network. In this activity, you learn how to create a Driver Store for setting up iPrint on the SUSE Linux server.

+   1. If necessary, log on to your Windows XP or SUSE Linux computer with your administrative or root user name and password.

+   2. Start your Web browser, start iManager, and log in to iManager with your administrative user name and password.

+   3. Follow these steps to create a Driver Store object for holding print drivers:
+      a. Expand the **iPrint** heading and click the **Create Driver Store** link to display the *Create Driver Store* window shown in Figure 14-18.

![](bbox=[0.11, 0.255, 0.58, 0.49])

**Figure 14-18**  The *Create Driver Store* window

+      b. If necessary, enter a container name by clicking the **Object Selector** button next to the Container name text box and clicking your **UAS** container.
+      c. In the Driver Store name text box, type **UASPrint_Drivers**.
+      d. Enter the IP address of your Linux server in the Target Server text box.
+      e. Click the **Object Selector** button next to the eDir Server name text box, and click your SUSE Linux server.
+      f. Click **OK** to create the Driver Store and display the completion message.

> **NOTE**  The following steps need to be performed from a Windows XP client.

+   4. If necessary, use the following steps to install the iPrint client on your Windows XP computer. (If you installed the iPrint client in Chapter 8, you can skip to Activity 14-13.)
+      a. If necessary, log on to your Windows XP computer and click the **Workstation Only** check box.
+      b. Start Internet Explorer and enter the URL `http://IPAddress/ipp` (replacing *IPAddress* with the IP address of your SUSE Linux server).
+      c. Click the **Install iPrint Client** link.
+      d. Click the **Open** option to start the installation wizard.
+      e. When the Install iPrint Client window is displayed, click **Next** to start the installation process.
+      f. After the client is installed, click **Finish** to return to the iPrint window. Close your Web browser.

+   5. Leave iManager open for the next activity.