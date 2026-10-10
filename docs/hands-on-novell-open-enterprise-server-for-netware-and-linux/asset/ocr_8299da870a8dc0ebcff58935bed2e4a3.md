# Activity 7-10: Documenting the Default Trustees of a New User

**Time Required:** 5 minutes

**Objective:** Identify the default trustees of a new user.

**Requirements:** Same as Activity 7-8

**Description:** When a new user object is created in eDirectory, certain attribute rights are granted automatically to give the user access to basic network resources. Knowing the default rights assignment for a new user can help you plan and set up an eDirectory security system that meets the needs of the organization and users. In this activity, you use NetWare Administrator to document the default trustees of a new user.

+   1. If necessary, start your computer, log in to eDirectory with your administrative user name and password, and start NetWare Administrator.
+   2. If necessary, open a browse window for your UAS container:
+      a. Click **View, Set Context** from the menu.
+      b. Click the **Browse** button next to the Context text box.
+      c. Double-click the **UAS** container in the Available objects section, and click **OK**. (If you're using a shared classroom server, expand the **CLASS** Organization, and then double-click your **UAS** container.)
+   3. Follow these steps to create a user name for yourself in the UAS container:
+      a. With the UAS container selected, click the **Create User** button on the toolbar.
+      b. Enter your information in the Login name and Last name text boxes, and then click **Create**.
+   4. Right-click your new user name, and then click **Trustees of this Object**.
+   5. Record the trustees of your user name and your assigned entry and attribute rights on the following lines. Click the **Selected properties** option button to include any selected attribute rights.
+   
+   ___________________________________________
+   
+   6. Click **Cancel** to return to the NetWare Administrator browse window.
+   7. Exit NetWare Administrator, and log out.

# DELEGATING ADMINISTRATIVE RIGHTS

As explained in Chapter 5, the occupant of the SysOp Organizational Role object is a backup administrative user whose account can be used if the main NetWare Admin user account is disabled or its password becomes compromised. One way to give the SysOp occupant the capability to act as a network administrator is to make the object a trustee of the [Root] object with Supervisor rights. In the following activity, you make the SysOp object a backup administrator for your system.

> Be careful when assigning the Write attribute right to the All Attributes Rights option. If users have the Write attribute right to the ACL property, for example, they can modify their trustee assignments, even to the point of making themselves a Supervisor of an object. In addition, having the Write attribute right to the Server object’s ACL property gives the trustee Supervisor rights to all volumes on that server—the one exception when assigning eDirectory rights affects file system security. Making users a Supervisor of the Server object grants them all rights to the file system, which can’t be blocked or overridden in any subdirectories or files.