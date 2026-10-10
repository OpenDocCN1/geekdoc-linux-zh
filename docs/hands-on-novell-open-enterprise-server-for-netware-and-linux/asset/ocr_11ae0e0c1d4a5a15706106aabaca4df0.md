+   6. Click the **Repeat Task** button and follow the procedure in Step 5 to create a user account for **Luke McMann**.

+   7. Click the **Repeat Task** button and follow the procedure in Step 5 to create a user account for **Bernie Mueller**.

+   8. Click **OK** to return to the iManager main window, and stay logged in for the next activity.

# ## Creating Organizational Role Objects

In addition to reducing the need to assign rights to multiple users, groups are a convenient way to give users the rights they need for certain job responsibilities. However, normally you don’t want to create groups that represent positions in the company. For example, David Heise wanted the IT Department to set up a manager for each department’s data and user accounts. Currently, Kari Means is assigned to act as the manager for the Engineering Department’s data and user accounts, Russ Pence is responsible for the Manufacturing Department’s data and users, and the administrative assistant, Lynn Dai, acts as the manager for the Business Division.

In addition, to increase security by limiting use of the network administrator’s user name, Eric created separate accounts to perform administrative tasks, such as eDirectory management and printer management. Because the user accounts assigned to these positions will change and could include multiple users, Eric didn’t want to assign rights to individual users. Instead of having to create groups for these types of positions, Novell has another object type called an **Organizational Role object**, which enables you to assign rights to an object rather than a specific user. You can then make any user an occupant of the Organizational Role object to gain its associated rights. If the job duties are given to another employee, you simply need to make the new employee an occupant of the Organizational Role object. For example, to give his user account rights to perform eDirectory management functions, Eric made the EKenton user an occupant of the eDirAdm Organizational Role object. Figure 5-25 lists the Organizational Role objects Eric defined for the UAS network.

**Organizational Role Planning Form**

Created By: | Date:

| Role Name | Context | Purpose | Primary Occupant(s) |
| :--- | :--- | :--- | :--- |
| SysOp | .IT.UAS | Backup system operator | Clark Kent |
| eDirAdm | .IT.UAS | Administrative role for maintaining eDirectory | EKenton |
| PrintAdm | .IT.UAS | Administrative role for maintaining Internet printing | EKenton, KThiele |
| EngMgr | Engineering.UAS | Engineering Department data manager | Kari Means |
| ISSEng | Engineering.UAS | Primary engineer assigned to the International Space Station | Tony Rucci |
| RoverEng | .Mfg.Engineering.UAS | Primary engineer assigned to the Mars Rover project | Lianne Jarka |
| MfgMgr | .Mfg.Engineering.UAS | Manufacturing Department data manager | Russ Pence, Bernie Mueller |
| AdmAss | .Mgmt.UAS | UAS administrative assistants | Lynn Dai, Kari Means |
| AeroMgr | .Mfg.Engineering.UAS | Manager of AeroDyn Division network objects | Bernie Mueller |

Figure 5-25 The UAS Organizational Role Planning Form