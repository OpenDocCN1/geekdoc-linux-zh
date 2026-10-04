# Attacking and Defending Microsoft Terminal Services • Chapter 9

# Windows XP TSAC

Windows XP has an installable component called Remote Desktop Web Connection, which is a fancy name for the TSAC in an XP environment. The Remote Desktop Web Connection can be installed from the Add/Remove Windows Components Wizard in Add Or Programs by adding IIS and the World Wide Web Service. The option for Remote Desktop Web Connection is hidden under details for the World Wide Web Service, as is shown in Figure 9.7.

If you require TSAC on a Windows XP system, I recommend that you start your research with this article from Microsoft: www.microsoft.com/windowsxp/pro/downloads/rdwebconn.asp.

# Figure 9.7 Installing TSAC on Windows XP

![](bbox=[0.248, 0.355, 0.752, 0.636])

# TSAC and Alternate Terminal Server Ports

TSAC in Windows XP offers the unique ability to modify the destination port for the ActiveX control. This is a wonderful new feature that allows the administrator to use the functionality of TSAC, without removing the ability to implement an extra layer of security by modifying the TCP port of the Terminal Server.

Let's say you have a Terminal Server that is configured to listen on TCP port 19740, and you want TSAC clients to be able to connect to this server via the ActiveX control. You just need to make an addition to the connect.asp file located in the /TSWeb directory. Before the connect method in the CONNECT.ASP code, simply insert your line:

```
MsTc.AdvancedSettings.RDPPort = 19740
```