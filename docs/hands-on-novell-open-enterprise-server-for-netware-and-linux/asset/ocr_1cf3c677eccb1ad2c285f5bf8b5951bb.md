+   b. Click the **browse** button next to the For Trustee text box, navigate to the **IT OU**, and click the **LMcMann** user.

+   c. Scroll down and click the **Path** property. Record Luke’s effective rights here:
+   
+   \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

+   6. Repeat Step 5 to check effective rights for a user in the Engineering OU. Record the user name and effective rights to the Path property here:
+   User name:
+   \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\n
+   Effective rights:
+   \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

+   7. Close ConsoleOne, and stay logged in for the next activity.

# Inherited Rights

To reduce the number of trustee assignments you need to make, NetWare allows trustee rights granted in a container to flow down to any subcontainers or leaf objects. As you learned for file system security, the process of rights flowing down the tree structure is called **inherited rights**. For example, in Chapter 5 you created the eDirAdm Organizational Role object. The occupant of this role needs rights to create, change, and modify objects in the eDirectory tree, so the eDirAdm Organizational Role object must have all rights except Supervisor to the UAS Organization and all its OUs. To do this, you can simply make the eDirAdm object a trustee of the UAS Organization. Through inheritance, the eDirAdm object receives all assigned rights to OUs in the UAS Organization, as shown in Figure 7-12.

![](bbox=[0.08, 0.46, 0.92, 0.72])

**Figure 7-12** Rights granted through trustee assignments to a parent container are inherited by subcontainers and leaf objects

Without inheritance, you would have to make several trustee assignments granting eDirAdm rights to each OU in the UAS structure. In Activity 7–4, you use iManager to make a trustee assignment and then check inherited rights.