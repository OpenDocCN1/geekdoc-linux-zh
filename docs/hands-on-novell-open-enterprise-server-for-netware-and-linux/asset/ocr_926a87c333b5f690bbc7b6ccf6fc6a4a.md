![](bbox=[0.12, 0.06, 0.58, 0.3])

Figure 11-9 The Primary Document Directory window

document site and directory for Engineering as a separate subdirectory of the main IT\Web content directory. Internet users could then access the Engineering Web site with the URL www.uas.com/engineering. In the following activity, you use Apache Manager to create an additional document site for the Engineering Department’s Web content.

# Activity 11-2: Creating an Additional Document Site for Printing

Time Required: 15 minutes

Objective: Use Apache Manager to create an additional document site to display your printer facility map.

Requirements: An administrative account for the Apache Web server running on your dedicated server or a shared classroom server and the path to your assigned directory. In addition, you need to have completed Activity 8-16, in which you created a printer facility map and added an Ippdocs directory. If you’re using a shared classroom server, the path should be UASHOST\CORP\IT\STUDENTS\##\Corp\IT\Web\Ippdocs; for a dedicated server, use \##UASHOST\CORP\IT\Web\Ippdocs, replacing ## with your assigned student number. This activity should be performed on a Windows XP computer.

Description: In this activity, you use Apache Manager to set up an additional document site that points to the Ippdocs directory containing your printer facility map.

+   1. Follow these steps to start Apache Manager via the Run command:
+      1. Click **Start**, **Run**, enter **https://IPaddress:2200** (replacing *IPaddress* with the IP address of your server), and then press **Enter**. If necessary, click **Yes** to close the security alert message box and open the Login window.
+      2. Enter your administrative user name and password and then click **Login**.
+      3. Click to expand the **Open Source** heading on the left, and then click the **Apache 2.0** link.
+      4. Click **Administer Single Apache Server** under the Apache 2.0 Links heading on the right to display the Server Status window shown previously in Figure 11-6.
+   2. View the status of your Apache Web server and, if necessary, click the **Start Server** button to start the server. Click **OK** to the confirmation message.
+   3. Follow these steps to create an additional document site:
+      1. Click the **Content Management** button on the toolbar.