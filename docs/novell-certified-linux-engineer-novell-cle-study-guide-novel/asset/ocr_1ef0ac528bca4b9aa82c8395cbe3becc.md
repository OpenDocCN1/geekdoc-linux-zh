| Attribute | Value |
| --- | --- |
| Telephone | 555-555-1234 |
| Fax Number | 555-555-2345 |
| Email Address | agresko@cle.com |

+   f. Click OK.
+   g. When prompted that the operation is complete, click OK.
+   h. In the **Enter the primary group for this user** field, browse to and select **IFEmployees.IFCLE**.
+   i. Make sure the **Also convert this User object to a Samba User object** box is selected.
+   j. In the **Enter the desired Samba password** field, enter **novell**.
+   k. Click OK.
+   l. When prompted that the LUM user was created, click **OK**.

+   3. Create a home directory for AGresko by completing the following steps:
+       a. Open an alternate shell by pressing **Ctrl+Alt+F2**.
+       b. Authenticate as **AGresko** with a password of **novell**.
+       c. Verify that a home directory was created for AGresko in /home.
+       d. Enter **logout** at the shell prompt.
+       e. Press **Alt+F7**.

+   4. Convert the existing users in your tree to Samba users by completing the following steps:

> WARNING
> This step assumes you deselected the option to make these users Samba users in the Chapter 6 lab exercises.

+   a. In iManager, scroll down to the **Linux User Management** role and select **Convert LUM User to Samba User**.
+   b. In the **Select User** field, browse to and select **CGrayson.IFCLE**.
+   c. Click **OK**.
+   d. When prompted, enter a password of **novell** in the **Enter the desired Samba password** field.
+   e. Click **OK**.