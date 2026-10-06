# 500 Part IV ♦ Implementing Network Services in SUSE Linux

![](bbox=[0.227, 0.137, 0.848, 0.503])

3. When this screen is displayed, the default name TUX-NET appears in the Windows Domain or Workgroup text box.

+   - If you know the exact name of the domain or workgroup, position the cursor in this text box, type the domain or workgroup name, and click the Finish button.
- If you do not know the exact name of the domain or workgroup that you want to join, click the Browse button to display a dialog box that shows the list of Windows domains and workgroups that are detected on the network to which your system is attached.

If you are configuring your system to be a member of a Windows domain, the Samba Client configuration panel provides the option of using the existing Windows authentication information provided by that when you log in your Linux system. This option simplifies local system administration by using a single, central authentication mechanism, but may make it difficult for you to log in when your system is not connected to the network. Using a Windows domain as your primary authentication mechanism is done by adding an SMB Pluggable Authentication Module (PAM) to the authentication process on your system, as defined by the file /etc/pam.conf.