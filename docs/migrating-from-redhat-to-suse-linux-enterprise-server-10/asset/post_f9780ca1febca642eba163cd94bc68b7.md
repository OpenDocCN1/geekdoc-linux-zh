
## Configure Security Settings

YaST provides a Local Security module that lets you configure the following local security settings for your SUSE Linux Enterprise Server:

- Password settings
- Boot configuration
- Login settings
- User creation settings
- File permissions

You can select from (or modify) three preset levels of security, or create your own customized security settings to meet the requirements of your enterprise security policies and procedures.

You can access the Security Settings module from the YaST Control Center by selecting **Security and Users > Local Security**, or by entering as root `yast2 security` in a terminal window.

The following appears:

### Figure 2-18

![](img/63e88022bf135307e3eac051ad238b5b_111_0.png)

From this dialog, you can select one of the following preset configurations:

- **Home Workstation.** Select for a home computer not connected to any type of a network. This option represents the lowest level of local security.
- **Networked Workstation.** Select for a computer connected to any type of a network or the Internet. This option provides an intermediate level of local security.
- **Network Server.** Select for a computer that provides any type of service (network or otherwise). This option enables a high level of local security.
- You can also select **Details** or **Custom Settings** to modify an existing security level or create your own configuration.

By selecting one of the three predefined security levels and selecting **Next**, the chosen security level is applied. By selecting **Details**, you can change the settings for the security level you have selected.

If you choose the **Custom Settings** and then select **Next**, you can directly change the details of the security configuration.

The dialogs for the detail settings look the same for every security level, but the preselected options are different. In the following dialogs, you see the settings for Level 3 (Network Server).

In the first dialog you can change the default password requirements that are accepted by the systems:

![](img/63e88022bf135307e3eac051ad238b5b_112_0.png)

From this dialog, you can select or enter the following password settings (mainly stored in `/etc/login.defs`, some values also in `/etc/default/passwd` and `/etc/security/pam_pwcheck.conf`):

- **Check New Passwords.** It is important to choose a password that cannot be found in a dictionary and is not a name or other simple, common word. By selecting this option, you enforce password checking in regard to these rules.
- **Test for Complicated Passwords.** Passwords should be constructed using a mixture of uppercase and lower case characters as well as numbers. Special characters like `:`, `=` etc. may be used too, but could be hard to enter on a different keyboard layout. This makes it very difficult to guess the password. Select this option to enable additional checks.
- **Password Encryption Method.** From the drop-down list, select one of the following encryption methods:
  - **DES.** This is the lowest common denominator. It works in all network environments, but it restricts you to passwords no longer than eight characters. If you need compatibility with other systems, select this method.
  - **MD5.** This encryption method allows longer passwords and is supported by all current Linux distributions, but not by other systems or older software.
  - **Blowfish.** This encryption method uses the blowfish algorithm to encrypt passwords. It is not yet supported by many systems. A lot of CPU power is needed to calculate the hash, which makes it difficult to crack passwords with the help of a dictionary. It is used as default encryption method on SLES 10.
- **Minimum Acceptable Password Length.** Enter the minimum number of characters for an acceptable password. If a user enters fewer characters, the password is rejected. Entering 0 disables this check.
- **Password Age.** Minimum refers to the number of days that have to elapse before a password can be changed again. Maximum is the number of days after which a password expires and must be changed.
- **Days Before Password Expires Warning.** A warning is issued to the user this number of days before password expiration.

Although root receives a warning when setting a password, she can still enter a bad password despite the above settings.

When you finish configuring password settings, continue by selecting **Next**. The following appears:

### Figure 2-20

![](img/63e88022bf135307e3eac051ad238b5b_114_0.png)

From this dialog, you can select the following boot settings (which update the file `/etc/inittab`):

- **Interpretation of Ctrl + Alt + Del**. When someone at the console presses the **Ctrl+Alt+Del** keystroke combination, the system usually reboots.
  - **Ignore.** Sometimes you want to have the system ignore this keystroke combination, especially when the system serves as both workstation and server. Nothing happens when the **Ctrl+Alt+Del** keystroke combination is pressed.
  - **Reboot.** The system reboots when the **Ctrl+Alt+Del** keystroke combination is pressed.
  - **Halt.** The system is shut down when the **Ctrl+Alt+Del** keystroke combination is pressed.
- **Shutdown Behavior of KDM.** You use this option to set who is allowed to shut down the computer from KDM.
  - **Only Root.** To halt the system, the root password has to be entered.
  - **All Users.** Everyone, even remotely connected users, can halt the system using KDM.
  - **Nobody.** Nobody can halt the system with KDM.
  - **Local Users.** Only locally connected users can halt the system with KDM.
  - **Automatic.** The system is halted automatically after log out.

For a server system you should use **Only Root** or **Nobody** to prevent normal or even remote users from halting the system.

When you finish configuring boot settings, continue by selecting **Next**. The following appears:

### Figure 2-21

![](img/63e88022bf135307e3eac051ad238b5b_116_0.png)

From this dialog, you can enter and select the following login settings (mainly stored in `/etc/login.defs`):

- **Delay After Incorrect Login Attempt**. Following a failed login attempt, there is typically a waiting period of a few seconds before another login is possible. This makes it more difficult for password crackers to log in. This option lets you adjust the time delay before another login attempt. Default is 3 seconds, which is a reasonable value.
- **Record Successful Login Attempts**. Recording successful login attempts can be useful, especially in warning you of unauthorized access to the system (such as a user logging in from a different location than normal). Select this option to record successful login attempts in the file `/var/log/wtmp`. You can use the command `last` to view who logged in at what time.
- **Allow Remote Graphical Login**. You can select this option to allow other users access to your graphical login screen via the network. Because this type of access represents a potential security risk, it is inactive by default.

When you finish configuring login settings, continue by selecting **Next**. The following appears:

![](img/63e88022bf135307e3eac051ad238b5b_117_0.png)

From this dialog, you can enter the following ID settings (stored in `/etc/login.defs`):

- **User ID Limitations**. Enter a minimum and maximum value to configure a range of possible user ID numbers. New users get a UID from within this range.
- **Group ID Limitations**. Enter a minimum and maximum value to configure a range of possible group ID numbers.

When you finish configuring user and group ID limitations, continue by selecting **Next**. The last page of the security configuration appears:

### Figure 2-23

![](img/63e88022bf135307e3eac051ad238b5b_118_0.png)
