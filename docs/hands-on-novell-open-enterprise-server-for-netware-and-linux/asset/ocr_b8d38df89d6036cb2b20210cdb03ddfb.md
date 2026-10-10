| User Template Planning Form | | | |
|:--|:--|:--|:--|
| **Organization:** | **Page of** | | |
| **Developed by:** | **Date:** | | |
| **Template name** | T_IT | | |
| **Context** | .OU=IT.O=UAS | | |
| **Home directory path** | UASHOST_CORP:IT | | |
| **Minimum password length** | 6 | | |
| **Require unique passwords** | No | | |
| **Days between password changes** | 90 | | |
| **Grace logins** | 6 | | |
| **Valid login times** | 5:00 a. m. until 11:59 p. m. Monday through Saturday | | |
| **Concurrent connections** | 1 | | |
| **Groups** | ITMgrs | | |
| **Users** | Kellie Thiele, Luke McMann | | |
| **Rights to Login Script property** | Read | | |
| **Rights to home directory** | All rights except Supervisor and Access Control | | |
| **Template name** | T_Engineering | | |
| **Context** | OU=Engineering.O=UAS | | |
| **Home directory path** | UASHOST_CORP:Engineer/Users | | |
| **Minimum password length** | 6 | | |
| **Require unique passwords** | Yes | | |
| **Days between password changes** | 90 | | |
| **Grace logins** | 6 | | |
| **Valid login times** | 5:00 a. m. until 11:59 p. m. Monday through Saturday | | |
| **Concurrent connections** | 1 | | |
| **Groups** | ITMgrs | | |
| **Users** | Kari Means, Tony Rucci, Lianne Jarka, Paul Aim, Kellie Thiele, Russ Pence | | |
| **Rights to Login Script property** | Read | | |
| **Rights to home directory** | All rights except Supervisor and Access Control | | |

Figure 5-19 The UAS User Template Planning Form

+   e.  Click the **IT** OU to place it in the Context text box, and then click **OK** to create the T_IT template and display the completion message.

+   f.  Click **OK** to return to the iManager main window.

+   4.  Follow these steps to configure the T_IT template as shown in Figure 5-19:

+   a.  Click the **Modify Object** link. Click the **Object Selector** button to select the T_IT template object and then click **OK**.

+   b.  Click the **Environment** link on the General tab to display the Home Directory fields. Click the **Object Selector** button to select the path to the IT directory.