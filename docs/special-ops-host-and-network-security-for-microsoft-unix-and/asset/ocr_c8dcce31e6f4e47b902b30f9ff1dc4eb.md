# Chapter 9 • Attacking and Defending Microsoft Terminal Services

# Figure 9.19 Using IE to Access cmd.exe

![](bbox=[0.258, 0.101, 0.683, 0.375])

# Using the Task Manager to Obtain a Shell

Another technique that has effectively to break out of a TS application is by using the default functionality of Windows as a beacon. When stuck in an application or restricted from cmd.exe, try using Ctrl+Alt+End to open Task Manager. If you are successful, click on the **New** task and then execute either cmd.exe or explorer.exe. This technique works as long as the administrator has not used the policy setting Disable Task Manager.

# Using WinZip to Obtain a Shell

Another option for obtaining a shell is to use Alt+Home to open the Start menu and then open WinZip. Create a new zip archive and copy cmd.exe into the .zip file (Figure 9.20). Double-click on the file to run it. This technique will be defeated if WinZip is not on the system. Additionally, group policy settings can be used to disallow the Start menu.

# Figure 9.20 Using WinZip to Get a Shell

![](bbox=[0.273, 0.771, 0.653, 0.897])

www.synergy.com