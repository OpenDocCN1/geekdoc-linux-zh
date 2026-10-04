# Attacking and Defending Microsoft Terminal Servers • Chapter 9

Application Server mode for a Windows 2000 Server is used for application sharing; it facilitates concurrent sessions on desktops and environments that share the server's resources. Remote Administration mode for a Windows 2000 Server offers less overhead as well as dramatically increased security.

Windows XP Professional comes with Remote Desktop (a scaled down version of Remote Administration mode) installed. It does not offer an application sharing mode.

Security-focused command line tools available from Microsoft qwinsta (query session), shadow, query termserver ,TSDiscon and reset session, and TSKill.

Terminal Services Configuration Connections (TSCC) allows for configuring of server settings and RDP-Tcp Properties.

# Attacking Terminal Servers

Once an attacker has interactive access to his victim TS can easily upload and execute a privilege escalation exploit to become an administrator.

TSEnum.exe identifies Terminal Servers in a domain if they are running on alternate ports. It will sometimes work even if you have no domain credentials.

If you dual-NIC your servers to connect network segments (not recommended), attackers can use techniques to find them and identify which ones are running Terminal Services.

Fscan.exe, local.exe, and tcsmcd.exe can be used together to enumerate accounts on a server have access to log on to the target Terminal Server.

TSGrinder and TScrack can be used to perform automated password guessing against a Terminal Server via TCP 3389.

If you allow users to connect to your Terminal Server in Application Server mode, an attacker may be able to subvert your security controls, gain access to a cmd.exe shell, then engage in a privilege escalation attack to achieve administrator access.

![](bbox=[0.707, 0.943, 0.929, 0.966])