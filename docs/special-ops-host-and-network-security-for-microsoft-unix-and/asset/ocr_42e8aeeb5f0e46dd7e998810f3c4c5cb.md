Attacking and Defending Microsoft Terminal Services • Chapter 9

# Privilege Escalation Attacks

Many exploits can be used to escalate a unprivileged account to administrator or LocalSystem. In this section, I discuss two of these exploits (GetAd.exe and DebPloit[ERunAsX.exe]) to demonstrate the danger of allowing users to connect to a Terminal Service that does not have the current Microsoft-issued patches installed.

If you require Terminal Services' application sharing, the best way to secure yourself against these types of exploits is with vigilant patch management. All Terminal Services in your environment should be kept up to date with the current Microsoft patches using http://windowsupdate.microsoft.com or a similar solution.

# Running GetAd.exe

The Bugraq ID for this vulnerability is 5927. It was discovered and published by Serus in Oct 09, 2002. This vulnerability affects Windows 2000 (including SP3). An unprivileged local attacker can leverage the Winlog NetDDE to obtain escalated privileges. This is performed by using a WM_COPYDATA message to send arbitrary code to NetDDE, which will be executed with Local System privileges when a WM_TIMER message is sent. More information is available from www.microsoft.com/technet/security/topics/htshat.asp.

# Running DebPloit Exploit in TS to Get Administrator

This privilege escalation attack was discovered on March 9, 2002 by Radim “EliCZ” Picha and is available from www.anticracking.sk/EliCZ/bugs.htm. The exploit works by impersonating the security context of snmss.exe (SYSTEM) by using a duplicated handle, even from a TS session.

Windows 2000 Servers with SP3 are not vulnerable to this exploit. Additionally, servers that have implemented the specific Microsoft patch are not vulnerable. The patch, which can be downloaded from www.microsoft.com/technet/security/bullet/MS02-024.asp, eliminates the vulnerability by implementing proper validation for requests to the debugging service.

In the following example shown in Figure 9.21, I check the UserAccount and show that it is not in the Administrators group, then I run it and tell it to execute the command net localgroup administrators UserAccount /add.

The window freezes, but if I open another cmd.exe on the TS (as shown in Figure 9.22) you can see that it was successful. You will need to off the server then log again to rebuild your token as an Administrator.

![](bbox=[0.707, 0.946, 0.927, 0.966])