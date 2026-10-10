![](bbox=[0.12, 0.06, 0.58, 0.33])

Figure 7-14   Viewing assigned rights for the Login Script property

+   g. Click to select the **Write** and **Inherit** check boxes.
+   h. Scroll down and click **Done** to save the new assignment.
+   i. Click the **Apply** button to save your changes.

+   7. Follow these steps to check effective rights for KThiele in the IT OU:
+   a. In the Roles and Tasks pane, click the **View Effective Rights** link under the Rights heading to display the View Effective Rights window.
+   b. Click the **Object Selector** button next to the Trustee name text box, and then click the **KThiele** user to insert her distinguished name in the Trustee name text box.
+   c. Click **OK** to display the View Effective Rights window.
+   d. Click the **Object Selector** button next to the Object name text box, and navigate to and click the **IT OU** to display KThiele’s effective rights. Record the effective rights to the Login Script property for KThiele:
+   
+   ____
+   e. Click the **All Attributes Rights** option and click the **Login Script** property. Record attribute rights for KThiele:
+   
+   ____
+   f. Click **Done** to return to the iManager main window.

+   8. Leave iManager open for the next activity.

# Using the Inherited Rights Filter

As in the file system, inherited rights can be blocked by using an Inherited Rights Filter (IRF). A difference between eDirectory security and file system security is that with eDirectory security, you can block a container or leaf object from inheriting Supervisor rights. You use this feature later in the “Planning eDirectory Security” section. In the following activity, you use iManager to work with IRFs.