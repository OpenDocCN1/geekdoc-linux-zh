
In the previous exercise, you created a custom application directory partition in Windows Server 2008. You can also use the next utility to configure, manage, and delete application partitions on a 2008 server. In the next section, we will discuss configuring DNS settings for your client computers so that they can interact with Active Directory, including integrating DNS with additional services such as Dynamic Host Configuration Protocol (DHCP) and WINS.

## Configuring DNS Client Settings and DHCP/WINS Integration

After you have configured your DNS servers with the necessary primary and/or secondary zones, you must configure your client computers (workstations, member servers, and other domain controllers) to use the correct DNS servers for name resolution. You can also integrate DNS name resolution with additional Windows Server 2008 network services, such as the Windows Internet Naming Service (WINS), to augment name resolution configuration for your client computers.

To authenticate to an Active Directory domain, each client must be configured to use a DNS server for name resolution that either:
- Hosts a primary or secondary zone containing the SRV records for your Active Directory domain, or
- Is configured with a stub zone or forwarder to a DNS server that hosts these SRV records.

### TAKE NOTE

If your DNS zones are configured to allow dynamic updates, clients and member servers will, by default, also attempt to dynamically register their A and/or PTR records with their preferred and alternate DNS servers.

When determining name resolution settings for your Active Directory clients, you should configure at least two DNS servers that your clients will use for name resolution, one primary and one secondary, in case the primary DNS server that you specify is not available. You should also consider the physical proximity of these servers and the speed of any WAN links that separate these DNS servers from your clients, so as to select primary and secondary servers that will provide the fastest response times for your clients. Ideally, your clients should point to a DNS server that is located within the same Active Directory site as the client; if you are using Active Directory–integrated DNS, this should be the domain controller that is servicing the site that the clients are using.

When configuring DNS server settings for your Windows clients, you have two options for distributing these settings:
- Manually, using a statically assigned IP address on each client computer
- Automatically, using the Dynamic Host Configuration Protocol (DHCP) service, which is used to automatically configure client computers with IP addresses and configuration information, such as a default gateway, a subnet mask, DNS and WINS server addresses, and so on

### CONFIGURE DNS CLIENT SETTINGS MANUALLY

**GET READY.** These steps will be performed on a Windows Server 2008 member server. This exercise requires you to be logged on to the server as a member of the Administrators group or the Network Configuration Operators group.

1. Click **Start** and select **Server Manager**.
2. In the Computer Information section, click **View Network Connections**. The Network Connections window is displayed.
3. Right-click the **Local Area Connection** icon and click **Properties**. The Local Area Connection Properties window is displayed.
4. Select the **Internet Protocol Version 4 (TCP/IP v4)** protocol and click **Properties**. The Internet Protocol Version 4 (TCP/IP v4) Properties window is displayed.
5. To manually specify one or more DNS servers, select the **Use the following DNS server addresses** radio button.
6. In the **Preferred DNS server** field, key the IP address of the DNS server that should be contacted first for DNS name resolution.
7. In the **Alternate DNS server** field, key the IP address of the DNS server that should be contacted if the preferred DNS server is not available.
8. Click **OK**, and then click **Close**.

**STOP.** Close the Network Connections window and the Server Manager window.

In the previous exercise, you configured the TCP/IP settings of a Windows Server 2008 computer with the IP addresses of a preferred and alternate DNS server.

Although DNS is the default name resolution method for Windows Server 2008, you might still need to configure a means of NetBIOS name resolution to support down-level clients on your network, in addition to applications such as Microsoft Exchange that still require NetBIOS name resolution to function. To enable enterprise-wide NetBIOS name resolution for your clients and servers, you can configure the WINS on one or more servers in your domain. Similar to DNS client resolution, you can configure each client and member server to point to one or more WINS servers for WINS name resolution. Each client and server will query these WINS servers when they need to resolve a NetBIOS name query, as well as registering their own NetBIOS information. Also similar to configuring DNS client resolution, you should configure both a preferred and an alternate WINS server for clients who require NetBIOS name resolution.

> **TAKE NOTE**
> WINS integration is configured on a DNS server on a per-zone basis, not for the entire server.

If you require both DNS and WINS for name resolution, you can configure your DNS server to automatically query one or more WINS servers when responding to a DNS query; this can allow your clients to resolve the name of a host that has been registered in WINS but not in DNS, even if your clients have only been configured with the IP addresses of a DNS server and not a WINS server. To integrate DNS and WINS name resolution on a Windows Server 2008 DNS server, use the steps in the following exercise.

### CONFIGURE DNS/WINS INTEGRATION

**GET READY.** To perform these steps, you must be logged onto the Windows Server 2008 computer as a member of the **Administrators** group or the **DNS Admins** group. These steps can be performed on a domain controller and a member server that has been configured with the DNS Server role.

1. Click **Start**, click **Administrative Tools**, and then click **DNS**. Expand the DNS MMC console to full screen, if necessary.
2. Click the plus-sign (+) next to the <server name> node, expand the **Forward Lookup Zones** node, and then expand the zone that you wish to configure.
3. Right-click the zone that you wish to configure and select **Properties**.
4. Click the **WINS** tab.
5. Place a checkmark next to **Use WINS forward lookup**. Key the IP address of each WINS server and click **Add**.
6. If you have any non-Windows DNS servers, place a checkmark next to **Do not replicate this record**.
7. Click **OK** to save your changes.

**STOP.** Close the DNS Management console before continuing.

In the previous exercise, you configured a DNS forward lookup zone to use WINS integration. This will allow DNS to forward requests to one or more WINS servers to resolve a name resolution query for a client.

## Configuring Additional Services

**THE BOTTOM LINE.** In addition to the Active Directory Domain Services role, Windows Server 2008 offers several additional services that can integrate with Active Directory Domain Services to increase the security and functionality of your Active Directory network.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_304_0.png)

In our final section, we will discuss two such additional services: the **Active Directory Rights Management Service (AD RMS)** and **Active Directory Federation Services (AD FS)**. Although neither of these services is necessary for the Active Directory Domain Services role to function, each has its place on a well-secured Windows Server 2008 network. Both the AD RMS role and the AD FS role can be installed using the Server Manager MMC snap-in on a Windows Server 2008 computer.

Active Directory Rights Management Service (AD RMS) is a Windows Server 2008 service that you can use to protect sensitive data on a Windows network. In particular, it enables owners of data stored within RMS-capable applications (such as word processing or spreadsheet applications) to control who can open, modify, or print a document, and even who can print or forward confidential email messages.

The following components are required to deploy AD RMS on your network:

![](img/a8ee53dbf1310726255b6fbb9f296fb2_304_1.png)

- A Windows Server 2008 computer running the AD RMS role, which also involves installing IIS on the selected server. This server can be a member server or a domain controller.
- A database server, such as one running SQL Server 2005. The database software can be installed on the same hardware as the server that is running the AD RMS role or it can be installed on a separate server.
- A computer running the AD RMS client software, such as a Windows Vista workstation that is working with an RMS-protected Microsoft Word document.
- The Active Directory domain must be at the Windows Server 2003 domain functional level or better.
- The AD RMS client is installed by default on Windows Vista and Windows Server 2008; down-level clients can be downloaded from the Microsoft Web site for Windows 2000 Service Pack 4 and later.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_304_2.png)

Finally, the Active Directory Federation Services (AD FS) role allows administrators to configure **Single Sign-On (SSO)** for Web-based applications across multiple organizations without requiring users to remember multiple usernames and passwords. This enables you to configure Internet-facing business-to-business (B2B) applications between organizations. For example, a user from adamum.com can use adamum.com credentials to access a Web-based application that is hosted by treyresearch.com. Rather than relying on Active Directory trust relationships, which can be difficult to set up and maintain over public networks such as the Internet, AD FS-enabled applications are *claims based*, which allows a much more scalable authentication model for Internet-facing applications.

An AD FS configuration consists of two types of organizations:
- **Resource organizations**. These organizations own the resources or data that are accessible from the AD FS-enabled application, similar to a trusting domain in a traditional Windows trust relationship.
- **Account organizations**. These organizations contain the user accounts that are accessing the resources controlled by resource organizations, similar to a trusted domain in a traditional Windows trust relationship.

When installing the AD FS role on a Windows Server 2008 computer, the following components are available:
- **AD FS Federation Service**. This service allows you to route authentication requests from user accounts in one organization to Web-based application resources in another.
