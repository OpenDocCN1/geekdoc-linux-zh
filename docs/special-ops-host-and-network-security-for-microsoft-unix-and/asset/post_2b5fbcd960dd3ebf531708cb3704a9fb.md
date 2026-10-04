
# System Hardening

- **Verify NTFS usage** You should ensure that all of your disks are matted with the NTFS file-system.

- **Secure your local security policy** This is a beast of a task but manageable. It is pertinent that you remember to log both success and failure events and restrict all anonymous connections.

- **Set file system and directory permissions** Use the golden rule of “Least Privilege,” that is, provide the least amount of privileges required for the job to succeed. This rule should be implemented throughout the system.

- **Protect file shares** Disable the default system shares $C$, ADMIN$, and IPC.

- **Enable ICF** Right-click on your active network connection and click **Properties** and then click **Advanced**. It is as easy as checking the box and clicking **OK**.

- **Configure Software Restriction Policies** Use hash-based rules to secure your system against file-specific threats such as the Melissa and Red Code viruses and use extension-based rules to protect against extensions as .exe and .vbs threats.

- **Remove unnecessary services, protocols, users, and groups** Keep what you need, as Antonie de Saint-Exupéry says “Perfection is reached, not when there is no longer anything to add, but when there is no longer anything to take away.”

- **Create IP security policies** Encrypt sensitive traffic between servers in which you have constant communication. IPSec rules should be created for internal DNS servers, development servers, print and file servers, and domain controllers.

- **Install anti-virus protections** Symantec, Trend Micro, and McAfee are the market leaders in anti-virus protection.

# Security Maintenance and Monitoring

- **Automate system updates** Configure your system to update on a daily basis. Lunchtime works best for most people.

- **Automate anti-virus updates** Anti-virus security updates are vendor-specific, but ensure that yours is configured to update virus definitions on a daily basis. If it is not feasible to update daily, weekly will suffice, but updates should not be spread apart by more than one week.

- **Review security logs** At the very minimum, ensure that your security logs are configured to reach a size that will save entries for at least one month in the case of a security incident.

- **Review system users and shares** It is always a good idea to review your active system shares by typing **C:/Net Use** from the command line and to review users through the MMC panel.

# Summary

XP Professional releases significant modifications over its predecessor Microsoft platform. New XP features include offline Web page viewing, dual DLL, built-in wireless support, and an enhanced version of the Remote Desktop Protocol (RDP). Multiple other security-related defense tools have also been implemented. The few XP-specific attacks that have been released focus more on Internet Explorer 6.0 and the new scripting functionality rather than the OS. Attacks such as the Universal Plug and Play denial of service attack received a good amount of press since the attack crossed most of the Microsoft developed platforms; however, Bill Gates' statement that Windows XP is the most secure OS to date stands.

Securing Windows XP is somewhat cumbersome initially, but the tools that have been implemented for the end user to maintain an acceptable level of security are easy to use and effective. The automated update wizard allows for auto-critical security-updates to be automatically downloaded and installed on a daily basis with the Software Restriction Policy engine is a good addition that proactively secures XP against application-layer threats. The combination of additional tools, built-functionality, and papers documenting best-of-breed security guidelines and practices are constantly improving. Most important, XP is the first example of Microsoft's dedication to security at the operating system level.

# Links to Sites

- **www.microsoft.com/windowsxp** You probably guessed it. This is the home of the Windows XP operating system.

- **http://windowsupdate.microsoft.com** Whether you like it or not, Microsoft has really hit the nail on the head with this site on ActiveX control. It is by one of the most conventionally useful sites for Microsoft technology administrators looking to lock-down systems.

- **www.microsoft.com/windowsxp/security/default.asp** The Microsoft Windows XP home for security advisories, vulnerabilities, threats, patches, white papers, and "techie tips." Another good resource for administrators.

- **www.microsoft.com/security** Microsoft's central location for security-related information.

# Attacking and Defending Windows XP Professional

- **www.tipsdr.net** A useful little site with general "tips and tricks" for enhancing and maximizing Windows XP. All of the tips are not security-focused; however, you can apply many of them in attack and defense MOs if you are a creative thinker.

- **www.ntsecurity.net** The home of the Windows & .NET Magazine provides excellent information pertaining to Microsoft technologies and Windows XP. It has databases with Win32 code, security-related information, and numerous articles.

- **www.xptutilities.com** A small site worth mentioning because of the array of products pertaining specifically to leveraging Windows XP features and configurations.

- **http://online.securityfocus.com** This is by far the best database on the Net combined with the home of the best security listing in existence. It is also a great place to look for Windows XP vulnerabilities based on patch level. Additionally, it is a great place to search for OS vulnerabilities and configuration dependencies. Unfortunately, due to commercialization, it is becoming less of a place to find the exploits for the attacks.

- **http://packetstormsecurity.org** The PacketStorm database represents what the Internet used to be when the DB consistently moved around and RootShell was still in existence. It is by far the most useful source for tools, exploits, and white papers describing just about vulnerabilities on all systems, including Windows XP.

# Forums and Mailing Lists

- **Buqtraq (http://online.securityfocus.com)** Excellent list covering security discussions, vulnerabilities, and patches across all platforms. Loosely moderated and tends to err on the side of full disclosure. It is an excellent list if you don't mind seeing a lot not related to anything you're likely to be running. Requires more patience than most but not happens without passing through this list.

- **NTBugtraq (nbtbugraq.com)** Focuses on issues related to Microsoft operating systems including Windows NT, 2000, and XP. Tightly moderated and tends towards limited disclosure. A good list for those interested in Microsoft-related vulnerabilities and not all the other cluster than can come from using general security lists.

- **VulnWatch (www.vulnwatch.org)** Full disclosure list that focuses on vulnerabilities rather than discussions or patch releases. This is a good choice if you are only interested in keeping up with recent issues but do not need the noise of open discussions or vendor patch announcements.

- **focus-ms (http://online.securityfocus.com)** A discussion list for those tasked with securing Microsoft operating systems and application servers. This focus less on vulnerabilities and acts more as an open how-to list for users to discuss best practices and share experiences.
