
## Activity 4-1: Creating an eDirectory Structure in iManager

**Time Required:** 10 minutes

**Objectives:** Use iManager to create eDirectory components.

**Requirements:**

- Windows XP or SUSE Linux 10 system using Internet Explorer or Java-enabled Firefox
- Access to a NetWare 6.5 server
- The administrator’s distinguished user name and password. If you’re using a dedicated server, your distinguished name should be Admin.UAS. If you’re using a classroom server with the standard setup, your distinguished name should be ##Admin.CLASS (## represents your assigned student number). Record the distinguished name of your administrator account here:
  -------------------------------------------
- The path to your UAS container. If you’re using a classroom server with the standard setup, the path should be ##UAS.CLASS (## represents your assigned student number). Record the path to your UAS container here:
  -------------------------------------------

**NOTE:** With some Linux Web browsers, steps in iManager might take a little longer to perform.

**Description:** Eric wants you to create a simplified version of the UAS eDirectory structure to be used in testing the NetWare 6.5 server. In this activity, you use iManager to set up the eDirectory structure shown previously in Figure 4-13.

1. If necessary, start your system and log on to your local computer. If you’re using your Windows XP Professional computer with Novell Client, click the **Workstation Only** check box to prevent logging in to the eDirectory tree.
2. Start your Web browser, and enter the URL [https://IPAddress/nps/iManager.html](https://IPAddress/nps/iManager.html) to display the iManager Login window.
3. Enter your administrative user name, password, and tree information, and then click the **Login** button to display the Novell iManager window shown previously in Figure 4-15.
4. In the Roles and Tasks pane on the left, click to expand the **eDirectory Administration** heading. Record the six eDirectory Administration options here (two per line):
   
   -------------------------------------------
   
   -------------------------------------------
   
5. Create the Engineering OU within your assigned container by following these steps:
   - a. Click the **Create Object** link to display the Create Object window shown in Figure 4-16.
   - b. In the Available object classes list box, scroll down and click **Organizational Unit** and then click **OK** to display the Create Organizational Unit window shown in Figure 4-17.

**NOTE:** If you’re using Linux, you might need to use the drop-down list under the Roles and Tasks heading and select All Categories before doing Step 4. See Appendix B for more information on using iManager with Linux.

![](img/840007e8f98ea6653e5877e945c27dc6_161_0.png)

Figure 4-16 The Create Object window

![](img/840007e8f98ea6653e5877e945c27dc6_161_1.png)

Figure 4-17 The Create Organizational Unit window

   - c. Enter **Engineering** in the Organizational Unit name text box.
   - d. Click the **Object Selector** button next to the Context text box to enter the path to your assigned container, using one of these two options:
     - ■ If you're using a classroom server, navigate to the path you recorded for your UAS container in the Requirements section.
     - ■ If you're using your own server, navigate to the UAS Organization container.
   - e. Click **OK** to display the completion message, and then click **OK** to return to the Novell iManager main window.

6. Follow the procedure in Step 5 to create the IT OU.
7. Follow these steps to create the Mfg OU within the Engineering container:
   - a. Click the **Create Object** link to display the Create Object window.
   - b. In the Available object classes list box, click **Organizational Unit** and then click **OK** to display the Create Organizational Unit window.
   - c. Enter **Mfg** in the Organizational Unit name text box.
   - d. Click the **Object Selector** button next to the Context text box to select the path to the Engineering container you created in Step 5.
   - e. Click **OK** to display the completion message, and then click **OK** to return to the Novell iManager main window.

8. Leave iManager open for the next activity.

## Activity 4-2: Creating Leaf Objects in iManager

**Time Required:** 10 minutes

**Objectives:** Use iManager to create eDirectory components.

**Requirements:**

- Windows XP or SUSE Linux 10 system with access to a NetWare 6.5 server
- NetWare 6.5 user name and password with rights to create objects in iManager
- Successful completion of Activity 4-1
- The context of your UASHOST server. If you're using a shared classroom server, the recommended context is ##UAS.CLASS. If you're using a dedicated server, the context should be _UAS. Record the context for your UASHOST server here: ________________________

**Description:** Eric wants you to be able to access the UASHOST server easily from the IT OU. In this activity, you use iManager to create an alias object for your UASHOST server in the IT OU you created in Activity 4-1.

1. To create an alias object for the UASHOST server in the IT OU, follow these steps:
   - a. If necessary, click to expand the **eDirectory Administration** heading.
   - b. Click the **Create Object** link.
   - c. Verify that the Alias object class is selected in the Available object classes list box, and then click **OK** to display the Create Alias window shown in Figure 4-18.

![](img/840007e8f98ea6653e5877e945c27dc6_162_0.png)

   - d. Enter **UasHost** in the Alias name text box.
   - e. Click the **Object Selector** button next to the Create alias for object text box, and then navigate to the container for your UASHOST server (based on the information in the Requirements section).
   - f. Click your UASHOST server object to place it in the Create alias for object text box.
   - g. Click the **Object Selector** button next to the Context text box, and then navigate to the IT OU you created in Activity 4-1 to place its distinguished name in the Context text box.
   - h. Click **OK** to create the alias object and display the completion message.

2. Click **OK** to return to the iManager main window, and leave iManager open for the next activity.

## Activity 4-3: Creating User Objects in iManager

**Time Required:** 10 minutes

**Objectives:** Use iManager to create eDirectory components.

**Requirements:**

- Windows XP or SUSE Linux 10 system with access to a NetWare 6.5 server
- NetWare 6.5 user name and password with rights to create objects in iManager
- Successful completion of Activity 4-1

**Description:** Eric wants you to create a user object that he can use to log in to the NetWare 6.5 eDirectory tree. In this activity, you use iManager to create a user account for yourself and Eric in the Engineering and IT OUs you created in Activity 4-1.

1. Scroll down and click to expand the **Users** heading in the Roles and Tasks pane. Record the user options here:
   
   --------------------------------------------------

2. To create a user name for Eric Kenton in the IT OU, follow these steps:
   - a. Click the **Create User** link to display the Create User window shown in Figure 4-19. Record all required fields (indicated by a red star) here:
     -------------------------------------------------
   - b. Enter the following information:
     - Username: **EKenton**
     - First name: **Eric**
     - Last name: **Kenton**
     - Context: If you’re using your own server, enter **IT.UAS**; if you’re using a classroom server, enter **IT.##UAS.CLASS** (## represents your assigned student number)
   - c. Scroll down and enter **password** in the Password and Retype password text boxes.
   - d. Click to select the **Set simple password** check box.
   - e. Scroll down and click **OK** to create the new user account for Eric.
   - f. Click **OK** to return to the Novell iManager main window.

![](img/840007e8f98ea6653e5877e945c27dc6_163_0.png)

3. Repeat the process in Step 2 to create a user name for yourself in the Engineering container. Record your user name here:

4. If you’re not going on to the next activity at this time, click the **Exit** button to return to the iManager log in screen. You can then close your Web browser and log out of your local client computer. If you’re continuing to the next activity, however, leave iManager open and stay logged in.

## Implementing eDirectory Replicas and Partitions

The first NetWare 6.5 server installed in the eDirectory tree stores the global eDirectory database in its SYS volume. The copy of the eDirectory database placed on a new server is called a **replica**. There are five types of replicas: Master, Read/Write, Filtered, Read-Only, and Subordinate. The eDirectory service automatically creates Read-Only and Subordinate replicas, so these two types aren’t a concern for small to medium networks. A Master replica is the original main copy of the eDirectory data. As a network administrator, you might want to create additional Read/Write (R/W) replicas for two major reasons: They improve performance by reducing the time required to authenticate or access a network object, and they ensure additional reliability and fault tolerance. For example, future expansion plans for Universal AeroSpace include adding a dedicated NetWare 6.5 server for Engineering and Manufacturing use. When the new server is added, eDirectory automatically places a copy of the entire eDirectory database on the new server, as shown in Figure 4-20.

![](img/840007e8f98ea6653e5877e945c27dc6_164_0.png)
