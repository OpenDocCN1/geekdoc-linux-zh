![](bbox=[0.14, 0.07, 0.9, 0.28])

+   9. Create the Cad subdirectory within the Apps directory structure by following these steps:
+   a. Click the **Info** icon in the first row of the NetWare File Listing table to display the Directory entry information window for the Apps directory (refer to Figure 3-30).
+   b. List the options available for the Apps directory:
+   _________________________________________
+   c. Enter the name **Cad** in the New name text box, and click the **Create Subdirectory** button to add this subdirectory to the Apps structure.

+   10. Repeat Step 9 to create the Office, Utility, and Desktop subdirectories under the Apps directory.
+   11. Click the .. link to return to the root of your volume, and stay logged in for the next activity.

# Activity 3-6: Implementing Directory Quotas

**Time Required:** 10 minutes

**Objective:** Use Remote Manager to set directory quotas.

**Requirements:** Successful completion of Activity 3-5

**Description:** Eric wants you to implement a directory quota on the volume to prevent directories from exceeding their planned sizes. In this activity, you use Remote Manager to set directory quotas on the directories you created in Activity 3-5.

+   1. If necessary, follow Steps 1 to 3 in Activity 3-5 to start Remote Manager and open the Volume Management window.
+   2. Set a directory quota of 4 GB for the IT directory by following these steps:
+   a. If necessary, click your assigned volume to display the NetWare File Listing window.
+   b. Click the **Info** icon next to the IT directory to display the Directory entry information window.
+   c. Next to the File space limit text box, click **None** to display the Directory Space Quota window.
+   d. Enter **4000000** in the Set Space Restriction in KB text box, and then click the **Set Space Restriction** button to set the file space limit.
+   e. Click the **Back to directory listing** link to return to the root of your assigned volume.
+   3. Use the procedure in Step 2 to set a directory quota of 500 MB (500000 KB) for the Forms directory. Record the value you enter for the space restriction:
+   _________________________________________
+   4. Click the **Exit** button to log out of Remote Manager, and close your Web browser.