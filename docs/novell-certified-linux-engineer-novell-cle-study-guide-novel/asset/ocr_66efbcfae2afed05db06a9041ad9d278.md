+   f. When prompted that the process was successful, select **Repeat Task**.

+   g. Convert the remaining user objects in IFCLE to Samba users using the preceding process.

+   h. Convert the user objects in SLC.CLE to Samba users using the preceding process.

+   5. Create a home directory for all users in your tree by completing the following steps:

+   a. Open a terminal session and check the subdirectories of the /home directory on your server.

+   b. Make a list of users in your tree who don’t have a home directory.

+   c. Open an alternate shell by pressing **Ctrl+Alt+F2**.

+   d. Authenticate the first user in your list who doesn’t have a home directory.

+   e. Verify that a home directory was created in /home.

+   f. Enter **logout** at the shell prompt.

+   g. Repeat this process for each user in your tree who doesn’t have a home directory.

+   h. When you’re done, press **Alt+F7**.

+   6. Configure your Samba server by completing the following steps:

+   a. From a shell prompt, enter vi /etc/opt/novell/samba/smb.conf.

+   b. Scroll down to the **workgroup** line.

+   c. Press **Ins**.

+   d. Change the value of the **workgroup** directive to **CLEWorkgroup**, as shown in Figure 8.41.

+   e. Scroll down to the **server string** line.

+   f. Change the value of the **server string** directive to **CLE1**.

+   g. Scroll down to the **[tmp]** share within the **Share Definitions** section of the smb.conf file.

+   h. Enable the **[tmp]** share by uncommenting the **comment**, **path**, **read only**, and **public** lines. When you’re done, this share should appear as shown in Figure 8.42.

+   i. Press **Esc**.