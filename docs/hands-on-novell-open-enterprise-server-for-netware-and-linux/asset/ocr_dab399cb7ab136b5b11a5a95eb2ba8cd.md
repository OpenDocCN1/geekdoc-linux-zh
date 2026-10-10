+   5. To enable group members to access all Linux servers, click the **Object Selector** button next to the Select the **Linux Config** object text box, and click the **UNIX Config** object. To Linux enable group members for selected SUSE Linux servers, click the Select one or more Linux Workstation objects option button, click the **Object Selector** button, and select only the Linux Workstation objects you want group members to access.
+   6. Click **OK** to enable the group and display the success message. Click **OK** again to return to the iManager main window.

In the following activity, you create a Linux-enabled group on your SUSE Linux server, create users, and then make one user a member of the Linux-enabled group.

# ### Activity 14-2: Creating Linux-Enabled Groups and Users

**Time Required:** 10 minutes

**Objectives:** Use iManager to create Linux-enabled users and groups.

**Requirements:** Access to the SUSE Linux server with an administrative account and a Windows XP or SUSE Linux 10 computer; you can also perform this activity from the OES Linux Enterprise Server 9 console. If using Linux, use the Java-enabled Firefox or Mozilla Web browser.

**Description:** To test the SUSE Linux server, Eric wants you to create an eDirectory structure for the AeroDyn Division that contains a Users OU with two test users. In this activity, you use iManager to create a Users OU in the AeroDyn Division, and then create a Linux-enabled group and users so that Eric can test the server.

+   1. If necessary, start your Linux server and log in with the root user name and password. If you’re working in Windows XP, log on to your Windows XP computer with your local user name and password.
+   2. Start your Web browser and start iManager by entering the URL *https://IPaddress/nps/iManager.html* (replacing *IPaddress* with the IP address of your SUSE Linux server).
+   3. Log in to iManager with your administrative user name and password.
+   4. Follow these steps to create a Users OU:
+       a. Click to expand the eDirectory Administration heading, and then click the **Create Object** link.
+       b. Scroll down and click the **Organizational Unit** object class, and then click **OK** to display the Create Organizational Unit window.
+       c. Type **Users** in the Organizational Unit name text box.
+       d. Click the **Object Selector** button next to the Context text box, and click your **UAS** container.
+       e. Click **OK** to create the Users OU and display the completion message.
+       f. Click **OK** to return the iManager main window.
+   5. Follow these steps to create a group and make it Linux enabled:
+       a. Click the **Create Object** link to display the Create Object window.
+       b. Click the **Group** object class, and then click **OK** to display the Create Group window.
+       c. Type **LinuxUsers** in the Group name text box, click the **Object Selector** button next to the Context text box, and click the **Users OU**.