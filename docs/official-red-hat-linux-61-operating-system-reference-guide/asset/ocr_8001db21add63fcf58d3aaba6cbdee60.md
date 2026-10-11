Press the **Accept** button again when finished. The system will let you know if it thinks the password is easy to crack; if you get a warning message, don’t use the password.

# ### 3.1.6 Modifying a User Account

+   - Go to **Config => Users accounts => Normal => User accounts**, use the filter if necessary, and then select the account that you wish to modify.
+   - See Section 3.1.5, *Adding a User Account* if you need guidance for how to fill in the user accounts fields.

To implement the changes select **Accept**. If you decide against making any changes select **Cancel**. This guarantees that no changes are made.

# ### 3.1.7 Changing a User’s Password

+   - Open **Config => Users accounts => Normal => User accounts**. This will open the **Users accounts** tab (see Figure 3–3, *Users Accounts Screen*).
+   - You may see a filter screen, depending upon the settings you’ve provided on **Control => Features**. If you want the full list, select **Accept** without changing any of the parameters. For detailed information on the various filters, select the `Help` button on the **Filter control** screen.
+   - Select the account whose password you wish to change. This will open the **User information** tab.
+   - Select **Passwd** from the options at the bottom of the screen.

`linuxconf` will prompt you to enter the new password. There is also a field called `Confirmation` where you will need to type the password again. This is to prevent you from mistyping the password. See Section 3.1.5, *Adding a User Account* for guidance on choosing a password. If you decide against changing the password, select **Cancel**. Once you have entered the new password select **Accept**.

# ### 3.1.8 Changing the Root Password

Because of the security implications of root access, `linuxconf` requires you to verify that you currently have access to the root account.

+   - Open **Config => Users accounts => Normal => Change root password**.