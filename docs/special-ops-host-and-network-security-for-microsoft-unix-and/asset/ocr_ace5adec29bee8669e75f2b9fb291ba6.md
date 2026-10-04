# Crash Course in Terminal Services

By default, Terminal Services use the Remote Desktop Protocol (RDP) via Transmission Control Protocol (TCP) port 3389. Configured properly, each session is authenticated using Windows domain authentication and is bidirectionally encrypted with the 128-bit RC4 crypto algorithm. The kernel supports multiple users with graphical sessions that can simultaneously run any number of applications on a single server.

# Terminal Services on Windows 2000

When you choose to install Terminal Services on a Windows 2000 Server you will be asked if you want to install in one of the following modes:

+   * Remote Administration mode
* Application Service mode

If you have used applications such as WinVNC or PCAnywhere, you might assume that Remote Administration mode will actually give you access to console applications applications do. This is not the case for Windows 2000; you will be connected to your own session on the server, separate from the console. You will need the console on Windows 2000, you will need to stand up and walk to the server and log on at the console. This doesn't detract from the overall value because believe me, Remote Administration mode will save the day if other applications such as Internet Information Services (IIS) or SQL code need to be restarted.

Application Service mode was created to facilitate concurrent sessions that share the server's resources. These sessions have individual desktops and environments. Unless you plan to use the Terminal Server for application sharing, you should install Remote Administration mode because it offers less overhead as as dramatically increased security. When you select Application mode, you will be prompted to select between permissions compatible with Windows 2000 users or NT 4 users (see Figure 9.1). If you have a very good and documented reason to allow the users access to the Registry and system files, you should choose the Permissions compatible with Windows 2000 Users. Finally, when upgrading from 4.0 Terminal Server, the new Terminal Server will be put into Application Server mode automatically and the items listed previously will come into effect. Do yourself a favor and rebuild your server. My Dad always said, “Do things the right way the first time and it will save you a lot of time later.”

![](bbox=[0.708, 0.942, 0.931, 0.966])