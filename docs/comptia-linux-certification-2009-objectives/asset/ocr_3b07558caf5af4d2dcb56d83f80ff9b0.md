# **What You Do**

# **How You Do It**

1. Modify the smb.conf file to share the printer.

+   a. On the terminal window, enter `vi /etc/samba/smb.conf` to open the smb.conf file in the text editor.
b. Navigate to the **Share Definitions** section.
c. Navigate to the beginning of the line containing the *browseable* variable in the **printers** section.
d. Press I to change to insert mode. Press **Enter** to insert a new line before the current line and press the **Tab** key.
e. Press the **Up Arrow** key and press the **Tab** key to move to the previous line.
f. Type **printer name = printer**
g. Press the **Down Arrow** key and press **Backspace** two times.
h. Type **yes** to make it browseable and press the **Down Arrow** key. Press **Backspace** two times.
i. Type **yes** to allow the guest account to access the printer share.
j. Press **Esc** to return to the command mode. Save the file and quit the editor.

2. Add a new smb user and restart the smb service.

+   a. Enter `smbpasswd -a jsmith` to add jsmith to the list of smb users.
b. Press **Enter** two times to set a blank password.
c. Enter `ifconfig` to view the IP address of the Linux system.
d. Note down the IP address of the system.
e. Enter `service smb restart` to restart the samba server.