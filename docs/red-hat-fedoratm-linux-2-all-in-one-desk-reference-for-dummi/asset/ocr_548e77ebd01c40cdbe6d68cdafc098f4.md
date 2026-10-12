# ## Configuring Samba

To set up the Windows file-sharing and print-sharing services, use the graphical Samba Server Configuration tool following these steps:

+   1. **Select Main Menus::System Settings::Server Settings::Samba.**
+   If you are not logged in as **root**, enter the **root** password when prompted for it. Then the Samba Server Configuration window appears.
+   2. **Click the Add button.**
+   The Create Samba Share dialog box appears.
+   3. **Enter the name of the directory to share or click Browse and select a directory. The directory must already exist.** Also select the **permission** — either **read-only** or **both read and write** (see Figure 6-4).

Figure 6-4 shows a typical example that shares the /home/public directory. If the directory does not exist, you can create the directory by logging in as root and typing mkdir /home/public in a terminal window.

![](bbox=[0.14, 0.49, 0.7, 0.74])

+   4. **Click the Access tab in the Create Samba Share dialog box. Then type in the users who need access to the shared directory or click the Allow Access to Everyone radio button. Then click OK.**
+   The Samba Server Configuration tool creates the Samba share by adding entries in the configuration file /etc/samba/smb.conf.