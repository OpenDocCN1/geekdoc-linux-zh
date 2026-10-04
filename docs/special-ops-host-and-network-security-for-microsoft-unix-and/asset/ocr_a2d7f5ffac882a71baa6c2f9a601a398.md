# Chapter 9 · Attacking and Defending Microsoft Terminal Services

After the client acknowledges the updated ActiveX control download dialog, the Remote Desktop Web Connection will automatically connect on that port.
One word of caution: if you are using TSAC, I do not recommend running the IIS Web server on the same system as the Terminal Server. For security reasons, it is good practice to segregate applications on separate servers.

> NOTE
By default, the TSAC component for Windows 2000 does not offer you the ability to change what port it connects to—it is hard-coded to 3389. However, with a simple hack, you can configure it to connect to an alternate TCP port. If you copy the TSWeb directory from a Windows XP server to your Windows 2000 server, it will allow the functionality to change the TCP connection port just like on XP.

# MMC Snap-in

Microsoft has included a snap-in to the Microsoft Management Console (MMC) to allow managing multiple Terminal Servers from one place. The components of the MMC Snap-in are the following:

+   - A Mtsmmc.dll
- A console file called Tsmmmc.msc

One problem with this MMC snap-in is that it has no mechanism for one to specify an alternate connection port. Only Terminal Servers left at the default port of 3389 can be reached directly via this tool.
Regardless of that shortcoming, this tool could be quite useful if you have many servers that you normally connect to throughout the day—simply clicking each connection puts you right at the console. Figure 9.8 shows two servers that have been added to the MMC.

# Using the Rdesktop Linux Client

Rdesktop is an open source client for Windows Terminal Services. It is capable of natively speaking RDP to achieve this task. Rdesktop currently runs on most Unix-based platforms with the X Window System.

![](bbox=[0.067, 0.942, 0.297, 0.967])