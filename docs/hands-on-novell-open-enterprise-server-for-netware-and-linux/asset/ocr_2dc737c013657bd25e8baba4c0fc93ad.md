In Chapters 6 and 7, you learn how to assign the rights these Organizational Role objects need for the positions’ required functions. In the following activity, you learn how to use iManager to create Organizational Role objects and then assign users as occupants.

# Activity 5-15: Creating Organizational Role Objects

**Time Required:** 10 minutes

**Objective:** Use iManager to create and manage Organizational Role objects.

**Requirements:** Completion of Activity 5-14

**Description:** To meet the directive of having a manager for each department’s data, Eric created an Organizational Role object for each department manager and then designated a user account for the occupant. In this activity, you create the Organizational Role objects that Eric defined in Figure 5-25 for the IT Department.

+   1. If necessary, log on to your local computer, open your Web browser to start iManager, and log in to iManager with your administrative user name and password.

+   2. If necessary, click to expand the **eDirectory Administration** heading, and then click the **Create Object** link.

+   3. In the Available object classes list box, click **Organizational Role**, and then click **OK** to display the Create Organizational Role window.

+   4. Follow these steps to create an Organizational Role object named **eDirAdm**:

+   a. Type **eDirAdm** in the Organizational Role name text box.

+   b. Click the **Object Selector** button next to the Context text box, and set the context to the **IT OU**.

+   c. Click **OK** to display the “Complete: The Create Organizational Role request succeeded” message.

+   5. Click the **Repeat Task** button. Follow the procedure in Step 4 to create an Organizational Role object named **PrintAdm** in the **IT OU**.

+   6. Click **OK** to return to the iManager main window.

+   7. Follow these steps to add **EKenton** as an occupant of the **eDirAdm** Organizational Role:

+   a. If necessary, click to expand the **eDirectory Administration** heading.

+   b. Click the **Modify Object** link to open the Modify Object window.

+   c. Click the **Object Selector** button next to the Object name text box, and then navigate to the **IT OU**. Click the **eDirAdm** object to place it in the Object name text box.

+   d. Click **OK** to open the Modify Object window for the **eDirAdm** object.

+   e. Click the **Role occupant** link to display the Role occupant list box shown in Figure 5-26.

+   f. Click the **Object Selector** button, and if necessary, navigate to the **IT OU** (see Figure 5-27).

+   g. Click the **EKenton** user account to add it to the Selected Objects list box at the bottom of the Object Selector window.

![](bbox=[0.12, 0.77, 0.18, 0.81])

> You can use the Object Selector window to add multiple users to the Selected Objects list box.

+   h. Click **OK**. **EKenton** should then appear in the Role occupant list box.

+   i. Click **OK** to save your changes and return to the iManager main window.

+   8. Repeat Step 7 to add both **EKenton** and **KThiele** as occupants of the **PrintAdm** Organizational Role object.

+   9. Stay logged in to iManager for the next activity.