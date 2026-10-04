# Securing Exchange and Outlook Web Access · Chapter 7

Follow the recommendations for hardening the Windows 2000 platform, Active Directory, and Internet Information Server found in Chapter 5 (Windows 2000 Operating System), Chapter 6 (Windows Active Directory), and Chapter 10 (Microsoft Information Server).

Next, consider locking down potentially unnecessary services and ports. This means removing any services that are not absolutely necessary for the operation of Exchange 2000. Remove unnecessary protocols and network drivers (such as the Network Monitor driver) if installed. On the TCP/IP properties of each network adapter, disable NetBIOS over TCP/IP (as shown in Figure 7.10). There is no reason for file and print services clients to be connecting to the Exchange server using NetBIOS.

# 7.10 Disable NetBIOS over TCP/IP for All Exchange Server Network Adapters

![](bbox=[0.357, 0.383, 0.642, 0.65])

Next, get the Exchange Server up to the very latest patches and security fixes. Although there are usually not many security fixes for Exchange 2000, when one is released it is patching a known vulnerability.You can bet that many potential intruders know about the vulnerability before Microsoft does.

# Dedicate Servers to Specific Functions

Whenever possible, dedicate servers to a specific task. This is not always possible in smaller organizations, but in a larger organization, I recommend breaking up servers into specific types of servers. This allows you to enable the maximum possible security configuration for that particular role without worrying about