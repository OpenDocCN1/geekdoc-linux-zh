# MOVE AN OBJECT BETWEEN OUS USING DRAG-AND-DROP

**GET READY.** To complete this exercise, you must be logged on as a member of the Domain Admins group.

+   1. In Active Directory Users and Computers, select the object you wish to move. If you wish to move multiple objects, press and hold the Ctrl key while selecting the objects you wish to move.
+   2. While holding down the left mouse button, drag the object to the desired destination OU and release the mouse. The object will appear in its new location.

**PAUSE.** You can close the Active Directory Users and Computers MMC snap-in now, or leave it open for the next exercise.

In the previous exercise, you moved one or more objects between OUs by using the drag-and-drop feature of the Active Directory Users and Computers MMC snap-in.

# MOVE AN OBJECT BETWEEN OUS USING THE MOVE OPTION

**GET READY.** To complete this exercise, you must be logged on as a member of the Domain Admins group.

+   1. In Active Directory Users and Computers, select the object you wish to move. If you wish to move multiple objects, press and hold the Ctrl key while selecting the objects you wish to move.
+   2. Right-click the selected object(s) and select **Move** from the shortcut menu. In the Move dialog box, select the container object that is the destination for the selected objects and click **OK**. Active Directory will refresh and the objects will appear in their new location.

**PAUSE.** You can close the Active Directory Users and Computers MMC snap-in.

In the previous exercise, you moved one or more objects between OUs by using the Move feature of the Active Directory Users and Computers MMC snap-in.

![](bbox=[0.1, 0.4, 0.28, 0.53])

# SUMMARY SKILL MATRIX

> **IN THIS LESSON YOU LEARNED:**
> 
> * Creating a naming standards document will assist in planning a consistent Active Directory environment that is easier to manage.
> * Securing user accounts includes educating users to the risks of attacks, implementing a strong password policy, and possibly introducing a smart card infrastructure into your environment.
> * As part of creating a secure environment, you should create standard user accounts for administrators and direct them to use Run as administrator or runas when performing administrative tasks.
> * When planning your OU structure, consider the business function, organizational structure, and administrative goals for your network. Delegation of administrative tasks should be a consideration in your plan.
> * Administrative tasks can be delegated for a domain, OU, or container to achieve a decentralized management structure. Permissions can be delegated using the Delegation of Control Wizard. Verification or removal of these permissions must be achieved through the Security tab in the Properties dialog box of the affected container.
> * Moving objects between containers and OUs within a domain can be achieved using the Move menu command, the drag-and-drop feature in Active Directory Users and Computers, or the dmove utility from a command line.