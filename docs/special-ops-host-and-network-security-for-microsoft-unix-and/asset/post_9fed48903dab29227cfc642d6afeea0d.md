
# Chapter 9 • Attacking and Defending Microsoft Terminal Services

- www.labmice.net/TerminalServices/default.htm Windows 2000 Terminal Server section of the labmice.net resource.
- www.microsoft.com/security/articles/password.asp Information on password complexity from Microsoft’s Web site.

# Mailing Lists

- ms-focus@securityfocus.com The all-around favorite for Microsoft-centric discussions and vulnerabilities.

# Other Books of Interest

- Craft, Melissa. Configuring Citrix MetaFrame XP for Windows, Including Feature Release 1, (ISBN: 1-931836-53-1). Syngress Publishing, .
- Russell, Ryan. Fast Poof Your Network, Second Edition, (ISBN: 1-928994-70-9). Syngress Publishing, .
- Mathers, Todd W. Windows NT/2000 Thin Client Solutions: Implementing Terminal Services and Citrix MetaFrame. Macmillan Technical Publishing, 2000.
- McClure, Stuart, George Kurtz, Joel Scambray. Hacking Exposed, Third Edition. Osborne/McGraw-Hill, 2001.
- Scambray, Joel, Stuart McClure. Hacking Exposed Windows 2000. Osborne/McGraw-Hill, 2001.
- Weber, Chris, Gary Bahadur. Windows XP Professional Security. Osborne/McGraw-Hill, 2002.

# Solutions Fast Track

# Crash Course in Terminal Services

- By default, Terminal Services use the Remote Desktop Protocol (RDP) via TCP port 3389. Configured properly, each session is authenticated using Windows domain authentication and is bidirectionally encrypted with the 128-bit RC4 crypto algorithm.

# Attacking and Defending Microsoft Terminal Servers • Chapter 9

Application Server mode for a Windows 2000 Server is used for application sharing; it facilitates concurrent sessions on desktops and environments that share the server's resources. Remote Administration mode for a Windows 2000 Server offers less overhead as well as dramatically increased security.

Windows XP Professional comes with Remote Desktop (a scaled down version of Remote Administration mode) installed. It does not offer an application sharing mode.

Security-focused command line tools available from Microsoft qwinsta (query session), shadow, query termserver, TSDiscon and reset session, and TSKill.

Terminal Services Configuration Connections (TSCC) allows for configuring of server settings and RDP-Tcp Properties.

# Attacking Terminal Servers

Once an attacker has interactive access to his victim TS can easily upload and execute a privilege escalation exploit to become an administrator.

TSEnum.exe identifies Terminal Servers in a domain if they are running on alternate ports. It will sometimes work even if you have no domain credentials.

If you dual-NIC your servers to connect network segments (not recommended), attackers can use techniques to find them and identify which ones are running Terminal Services.

Fscan.exe, local.exe, and tcsmcd.exe can be used together to enumerate accounts on a server have access to log on to the target Terminal Server.

TSGrinder and TScrack can be used to perform automated password guessing against a Terminal Server via TCP 3389.

If you allow users to connect to your Terminal Server in Application Server mode, an attacker may be able to subvert your security controls, gain access to a cmd.exe shell, then engage in a privilege escalation attack to achieve administrator access.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_531_0.png)

The common SA Shell password on a system allows an attacker to use the XP_CmdShell extended stored procedure to add a user, and make the user an administrator.

In Windows 2000, the File Copy provides the ability to copy, cut, and paste files to and from a Terminal Server. Windows XP allows the transfer of files within a Remote Desktop Connection via sharing of local drives.

An attacker with control of a Terminal Server can use techniques using the tools PWdump3 and LSADump2 to gain domain access.

# Defending Terminal Services

When not secured properly, the increased functionality of Terminal Services will cause a decrease in overall security for the host operating system. A vulnerability in one will probably lead to a compromise of the other.

Install current patches and secure the operating system. Set strong Windows passwords and use a tool like John the Ripper to test these passwords.

On Windows 2000 Terminal Services, force the setting of High encryption for all sessions.

Set permissions and control Terminal Services settings for local system administrators by implementing Group Policy restrictions at the Domain or OU in Active Directory.

Application Server mode needs to be secured in the same way that you would secure a server that allowed users to log on locally.

# Frequently Asked Questions

The following Frequently Asked Questions, answered by the authors of this book, are designed to measure your understanding of the concepts presented in this chapter and to assist you with real-life implementation of these concepts. To have your questions about this chapter answered by the author, browse to www.syngress.com/solutions and click on the “Ask the Author” form.

- Q: If the server is running in Remote Administration mode, can I connect as a nonadministrative user?
A: Yes, but only if it has been configured to do so (Windows XP must be in the Remote Desktop Users group).

- Q: Ctrl+Alt+Del doesn't work in a Terminal Server session—what can I do?
A: When in a TS session, you will need to use Ctrl+Alt+End to simulate a Ctrl+Alt+Del. Additionally, you can use Alt+(Page Up | Page Down) to switch applications and Alt+Del to right-click the active application’s icon.

- Q: Does Windows XP Remote Desktop offer an application sharing mode like Windows 2000 Terminal Services?
A: No, if you require application sharing mode you should use Windows Server 2003 and add Terminal Services by using Control Panel | Add or Remove Programs | Add/Remove Windows.

# Chapter 10

# Securing IIS
by Mark Burnett

Solutions in this Chapter:

- Learning from the Past
- Preparing the Operating System
- Securing Web Sites
- Securing Web Sites
- Authenticating Users
- Publishing Web Content

Related Chapters:

- Chapter 11: Hacking Custom Applications
- Chapter 12: Attacking and Defending Microsoft SQL Server
- Chapter 13: Attacking and Defending Oracle

- Summary
- Solutions Fast Track
- Frequently Asked Questions

# Introduction

An Intranet Web site is a portal providing a means of publishing and accessing company information. But because it is connected to a wealth of corporate information, it is also a key target for insider hackers. The threats facing an internal Internet Information Services (IIS) server are one and sometimes greater than those coming from outside attacks. This chapter demonstrates how to build an intranet IIS server that can address the unique threats exposed by those hackers coming from behind the veil.

# Knowing the Enemy

An internal IIS server has many unique vulnerabilities and exposures that an outside Web server may not have. The greatest weakness is that the attackers are coming from the same network and therefore have access to many additional attacks. Further, the insiders have access to information that outsiders simply do not have. The insider may already know about the network structure, security measures that are in place, and even pass the IIS server on the water cooler every day. Insiders already have some trusted to the network and do not need to be concerned with penetrating the firewall. Insider hackers may be able to sniff traffic on the internal network and perhaps have the great advantage of gaining physical access to the server itself. As an employee or contractor, the insider may also be able to gather information from sources such as sticky notes or overhear conversations. Insiders may be aware of significant lapses of security, and there is significant potential for social engineering attacks. Most importantly, insiders already have a valid user account on the network and may have access to resources on the intranet IIS server.

Insider attackers are a limited set of individuals who have inside access, but must be trusted to a degree to perform their job duties. Because of that, it is difficult to distinguish between those doing their jobs and those abusing the trust given them.

Securing an intranet server requires special attention to physical security and careful access control. In this chapter, as we describe building the IIS server, we cover the use of encryption, authentication, and logging techniques more appropriate for insider threats.
