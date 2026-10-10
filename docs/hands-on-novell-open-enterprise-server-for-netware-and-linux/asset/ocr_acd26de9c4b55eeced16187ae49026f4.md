server to point to a different home directory. You can also set the FTP server to use the default home directory rather than the user’s home directory. By default, when users log in to the FTP server, their FTP directory path is set to the home directory path stored in their eDirectory accounts. If you want all users to access a common default directory path, enable the check box Always use ‘Default home directory’ instead of the user’s home directory from eDirectory.

![](bbox=[0.14, 0.16, 0.66, 0.38])

**Figure 11-13  The User tab**

FTP Server supports an anonymous user account to give users without accounts on the system access to files intended for public use. When enabling anonymous user access, the network administrator needs to specify the path to the anonymous user home directory and indicate whether an e-mail address is required for the password. The e-mail address doesn’t cause any access restriction but gives network administrators a way to track access to the FTP site and send messages to users.

You can use the Security tab shown in Figure 11-14 to disable accounts after a specified number of invalid login attempts. Notice that intruder detection settings are divided into Host Intruder Detection and User Intruder Detection sections. Host intruder detection is used to prevent other computers from logging in; user intruder detection process is similar to the intruder detection you learned about for local user accounts in Chapter 5. In both cases, you can block logins for a specified number of minutes after the number of invalid login attempts exceeds the specified setting.

![](bbox=[0.14, 0.64, 0.66, 0.87])

**Figure 11-14  The Security tab**