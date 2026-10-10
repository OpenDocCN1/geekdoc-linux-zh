+   6. To select printers, follow these steps to identify the IP address of your Print Manager:
+   a. Click the **Locate printers** button next to the Printer List text box to open the **Change printer list – Web Page Dialog** window.
+   b. Enter the IP address of the UASHOST classroom server in the **Print Manager Address** text box, and then click **OK**.
+   c. If asked to log in, enter your administrative user name and password.
+   
+   7. The next step in building a printer map is to select a graphics file for the floor plan. When the Map utility loads, it scans the `Login\Ipdocs\Images\Maps` directory automatically for any graphics files. Scroll down and click the **Background** list arrow to display all graphics files in the `Maps` directory, and then click the **Office.gif** file to display a sample office layout in the main window.
+   
+   8. Follow these steps to place the **IT_Optr_1** printer on the floor plan:
+   a. Click the **Printer List** list arrow to display all printers managed by the Print Manager you selected in Step 6.
+   b. Click the **IT_Optr_1** printer.
+   c. Drag the printer icon to the Engineering Department in the UAS layout, next to Kari Means.
+   d. In the Printer URL text box, enter `http://IPaddress/ips/IT_Optr_1.` (Replace `IPaddress` with the IP address of your NetWare server).
+   
+   9. Follow these steps to save the facility printer map:
+   a. Click the **Save** link at the top to open the Save dialog box.
+   b. Navigate to the `IT\Web\Ipdocs` directory, enter **UASPrinters** in the File name text box, and click the **Save** button.
+   
+   10. Close your Web browser.

![](bbox=[0.09, 0.47, 0.75, 0.54])

11. Close all open windows, and log out.

# # ESTABLISHING A PRINTING ENVIRONMENT

Now that you have had a chance to become familiar with setting up NDPS/iPrint components, it’s time to apply this new knowledge to setting up network printers for your version of the UAS network. Eric’s first task in establishing the printing environment was to define the printing needs to be supported on the network, which involved these steps:

+   1. Determine the number and types of printers, and define printing requirements for each user’s applications.
+   2. Determine printer locations and attachment methods.
+   3. Define names for all printers and identify any required print queues.
+   4. Plan the eDirectory context for each printer object.

In the following sections, you apply these steps to defining a network printing environment for your UAS organization using the NDPS Definition Form that Eric developed.

# ## Step 1: Defining Printing Requirements

The first step is to identify the number and types of network printers the organization needs. To do this, you need to analyze the requirements of all users’ applications and their printing needs. Table 8-1 summarizes the printing needs for Engineering, Mgmt, and Mfg users in the UAS network.