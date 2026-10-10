# Container Trustee Assignments

As with a group, when a container object is made a trustee of a file or directory, all users in the container and any subcontainer objects share the rights made in the trustee assignment. When working with container trustee assignments, remember that a child container has the same effective rights as its parent. For example, rights granted to the UAS container also belong to the Mgmt, Engineering, Mfg, and IT subcontainers. In the following activity, you use Remote Manager to make your UAS container a trustee of a directory and then verify effective rights for users in your organization.

# Activity 6-6: Making a Container Trustee Assignment

**Time Required:** 5 minutes

**Objective:** Use Remote Manager to assign rights to containers.

**Requirements:** Same as Activity 6-5 and completion of Activity 3-5

**Description:** Eric wanted all users to have rights to access files in the Forms directory located off the root of the CORP volume. To do this efficiently, he made the UAS Organization a trustee of the Forms directory with Read and File Scan rights. In this activity, you use Remote Manager to carry out this task, and then check effective rights for your users.

+   1. If necessary, start Remote Manager by following Steps 1 and 2 in Activity 6-4.
+   2. Log in to Remote Manager with your administrative user name and password.
+   3. Under the Manage Server heading, click the **Volumes** link to display the Volume Management window.
+   4. Click the **CORP** volume to open it. (If you're working on a shared classroom server, click the **STUDENTS** volume first, and then click your **##Corp** directory.)
+   5. Click the **Info** icon next to the Forms directory to display the Directory entry information window.
+   6. Follow these steps to add your UAS container as a trustee with Read and File Scan rights:
+   	 a. Click the **Browse** link next to the User Name text box and navigate to your **UAS** container.
+   	 b. Click the link next to your **UAS** container to place its distinguished name in the User Name text box.
+   	 c. Click the **Add Trustee** button to display the Trustee rights window shown previously in Figure 6-6.
+   	 d. Click to clear all check boxes except Read and File Scan.
+   	 e. Click **OK** to save your changes and return to the Directory entry information window.
+   7. Click the **Exit** button to return to the Remote Manager Login window.
+   8. Check effective rights for Luke McMann in the Forms directory by following these steps:
+   	 a. Log in to Remote Manager with the distinguished name and password for Luke McMann (such as LmCmann.IT.UAS if you're using a dedicated server).
+   	 b. Click your volume name under the Volumes heading on the right. (If you're using a shared classroom server, click your **##Corp** directory.)
+   	 c. Click the **Info** icon next to the Forms directory to display the Directory entry information window for Luke McMann. Record Luke's effective rights:
+   	 ________________________________________________________
+   	d. Click the **Exit** button to return to the Remote Manager Login window.
+   9. Repeat Step 8 to record effective rights for a user in the Engineering OU. Record that user's name and effective rights:
+   	 ________________________________________________________
+   10. Close your Web browser and log off your computer.