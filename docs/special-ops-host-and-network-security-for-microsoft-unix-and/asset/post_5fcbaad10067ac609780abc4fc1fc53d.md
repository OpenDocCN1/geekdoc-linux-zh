
# Chapter 9 · Attacking and Defending Microsoft Terminal Services

After the client acknowledges the updated ActiveX control download dialog, the Remote Desktop Web Connection will automatically connect on that port.
One word of caution: if you are using TSAC, I do not recommend running the IIS Web server on the same system as the Terminal Server. For security reasons, it is good practice to segregate applications on separate servers.

> NOTE
> By default, the TSAC component for Windows 2000 does not offer you the ability to change what port it connects to—it is hard-coded to 3389. However, with a simple hack, you can configure it to connect to an alternate TCP port. If you copy the TSWeb directory from a Windows XP server to your Windows 2000 server, it will allow the functionality to change the TCP connection port just like on XP.

## MMC Snap-in

Microsoft has included a snap-in to the Microsoft Management Console (MMC) to allow managing multiple Terminal Servers from one place. The components of the MMC Snap-in are the following:

- A Mtsmmc.dll
- A console file called Tsmmmc.msc

One problem with this MMC snap-in is that it has no mechanism for one to specify an alternate connection port. Only Terminal Servers left at the default port of 3389 can be reached directly via this tool.
Regardless of that shortcoming, this tool could be quite useful if you have many servers that you normally connect to throughout the day—simply clicking each connection puts you right at the console. Figure 9.8 shows two servers that have been added to the MMC.

## Using the Rdesktop Linux Client

Rdesktop is an open source client for Windows Terminal Services. It is capable of natively speaking RDP to achieve this task. Rdesktop currently runs on most Unix-based platforms with the X Window System.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_486_0.png)

Rdesktop was written by Matt Chapman and is free under the GNU General Public License (GPL). The rdesktop source code can be downloaded from www.rdesktop.org. Compile the source by running make on your platform to get the executable. Precompiled Linux binaries can also be downloaded from www.sourceforge.com.

Figure 9.9 shows Rdesktop starting the connection.

## Figure 9.9 Connecting Using the Rdesktop Client

![](img/729efc56f204a2ebffb8295c3a2dfdfb_487_1.png)

Once the server is specified, the application connects via TCP 3389 just like the Remote Desktop Connection client (see Figure 9.10).

www.synergy.com

## Figure 9.10 The Rdesktop Connection in Action

![](img/729efc56f204a2ebffb8295c3a2dfdfb_488_0.png)

## Macintosh Clients

There is even a Remote Desktop Connection client for Macs. You can download the client and detailed information from www.microsoft.com/mac/DOWNLOAD/MISC/RDC.asp.

## Using Terminal Server Tools

Many tools are available to manage and secure the Terminal Servers in your network depending on your requirements. Some work only within a TS session, some are command-line applications, and some are GUI applications. The following categories are discussed in this section:

- Windows 2000 Terminal Server Commands
- Using TScmd.exe
- Terminal Server Manager
- Terminal Server Configuration
- Terminal Server Group Policies

## Using Windows 2000 Terminal Server Commands

There are many command line tools available from Microsoft that are useful in a Terminal Server session. The following lists are some of the security-focused command-line tools from Microsoft. Each tool has a variety of uses; you should try all of them to find out which work best for you. Many of these tools exist on Windows XP and Windows Server 2003:

- Qinsta.exe (query session) This is useful to figure out how their sessions are connected and in case you need to "look over your shoulders" for any reason using Shadow. This can also be used to monitor other Terminal Servers using the /server:server_ip directive. Query Session is shown in Figure 9.11.

## Figure 9.11 Example of the Query Session Command

![](img/729efc56f204a2ebffb8295c3a2dfdfb_489_0.png)

- Shadow This allows you to monitor and control other user sessions from your TS session. The ability to perform this action is determined by the setting with the highest precedence. The same applies regarding Require Users Permission setting that determines if they will or not be asked for permission to allow the shadowing. An interesting fact is that the Console cannot be shadowed on Windows 2000, but it can be shadowed and controlled on Windows XP and Windows Server 2003.

- Query termserver This command can only be used in a TS session. It is useful for attackers and administrators to find other Terminal Servers in the current domain.

- TSDiscon This command allows you to disconnect a user session without logging them out. This can be useful if you need to clear a session or prevent a user from occupying a slot.

- TSKill This command is used to force log a user off the system. It is useful when a user session is hung or needs to be terminated immediately.

- Queryinsta This command can be used to display information about all sessions on a Terminal Server. It is useful for identifying which users are currently logged in.

- Userinsta This command allows you to query information about a specific session by its ID. It can be useful for troubleshooting issues with a particular user.

- Shadowinsta This command allows you to shadow a specific session. This is useful for monitoring what a user is doing in real-time.

- Disinsta This command allows you to disconnect a specific session. It is useful for removing a user from the system.

- Killinsta This command allows you to kill a specific session. It is useful for terminating a session that is no longer responsive.

## Figure 9.8 MMC Snap-In Viewing Multiple Servers

![](img/729efc56f204a2ebffb8295c3a2dfdfb_487_0.png)
