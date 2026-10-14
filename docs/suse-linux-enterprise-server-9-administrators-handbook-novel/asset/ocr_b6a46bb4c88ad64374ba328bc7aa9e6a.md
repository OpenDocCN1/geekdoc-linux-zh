files for you (such as `/etc/security/pam_unix2.conf` and `/etc/security/pam_pwcheck.conf`). You can make the change either via the User and Group Administration module or the Local Security Configuration module as follows:

+   - From the YaST Control Center, select Security and Users, Edit and Create Users to launch the User and Group Administration module. Click Expert Options, Password Encryption. From the displayed Set Password Encryption dialog box (see Figure 4.4), select the desired method and click OK. Click Finish for the change to take effect.

# **FIGURE 4.4**  
Changing the password-hashing method.

![](bbox=[0.312, 0.343, 0.604, 0.492])

+   - From the YaST Control Center, select Security and Users, Security Settings to launch the Local Security Configuration module. If the Current Security Setting is one of Level 1 through Level 3, click Details. If the selection is Custom Settings, click Next. The first screen is Password Settings (see Figure 4.5). From the Password Encryption Method drop-down list, select the desired method. Make any other changes if desired. Click Next until the Miscellaneous Settings screen is displayed. Click Finish for the new change(s) to take effect. (From a terminal session, you can launch the Local Security Configuration module directly using `yast security` or `yast2 security`.)

# **WARNING**

There appears to be a cosmetic bug with the User and Group Administration module when setting passwords. Regardless of your current password-hashing algorithm, when you try to use a password longer than eight characters, YaST always warns you that the password is too long and asks if it should be truncated. When you click Yes, it is truncated when using DES. However, with MD5 and Blowfish, the password is not truncated even though you are led to believe it will be after you click Yes; if you click No, you're returned to the screen to enter the password again.