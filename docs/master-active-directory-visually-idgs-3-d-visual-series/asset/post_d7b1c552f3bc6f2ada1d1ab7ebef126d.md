
# What is the SOA?

The Start of Authority is a resource record that defines which server is authoritative for a zone. The SOA tab allows you to make adjustments to this record as necessary. You can change the primary server that holds the SOA record, and you can even change the responsible person who manages the SOA on that server. The important point about this option is you can make major changes to your server's DNS configuration without having to delete your zones and start all over. This is, of course, a very important feature of Windows 2000.

# What is the Name Servers tab?

Like the SOA tab, the Name Servers tab lists the NS records that are configured for the zone. This list tells you which servers are in the zone and available for the zone. You can use the add, edit, and remove buttons on the Name Server tab to manage the list as desired.

![](img/763d5ae436311371600c0952a3da9094_190_0.png)

![](img/763d5ae436311371600c0952a3da9094_190_1.png)

![](img/763d5ae436311371600c0952a3da9094_190_2.png)

- 1. Click the Start of Authority (SOA) tab.
- 2. Click Increment to adjust the serial number, if necessary.
- 3. Adjust the Refresh, Retry, and Expires After, if necessary.
- 4. Click the Name Servers tab.
- 5. Use the Add, Edit, or Remove buttons to adjust the name servers in the list.

# CONFIGURING ZONE PROPERTIES CONTINUED

The WINS tab enables you to use a WINS forward lookup to resolve NetBIOS names. DNS resolves domain names to IP addresses while WINS resolves NetBIOS names to IP addresses. The WINS lookup feature allows the DNS server to query the WINS server(s) that you specify to lookup a name in the WINS database that the DNS server cannot resolve. This feature is useful in mixed Windows 2000 environments where both DNS and WINS are in use. On the WINS tab, simply click the check box to enable the WINS lookup and then provide the IP address(es) of the WINS server(s).

On the Zone Transfers tab, you can choose to allow zone transfers. A zone transfer updates the secondary DNS servers with the primary zone database file. Remember that the secondary DNS servers in the zone receive a copy of the primary zone database file. Only the primary DNS zone database file can be updated. After the primary zone file is updated, the secondary servers will get the database file from the primary zone server.

![](img/763d5ae436311371600c0952a3da9094_191_0.png)

![](img/763d5ae436311371600c0952a3da9094_191_1.png)

- 1. Click the WINS tab.
- 2. Click these check boxes to use WINS forward lookup and to prevent record replication.
- 4. Type the IP address of the WINS server(s) here.
- 5. Click Add.
- 6. Click the Zone Transfers tab.
- 7. Click this check box to allow zone transfers.
- 8. Click the appropriate radio button to manage the zone transfers.
- 9. Click Notify to notify secondary servers of updates.

# What is a zone transfer?

The updates to the secondary DNS servers occur through a process known as zone transfer. Without the zone transfer process enabled, secondary DNS servers in the zone will not be automatically updated when the DNS database changes. You can choose to allow zone updates to any server in the zone, only the servers listed in the Name Servers tab, or you can configure the server list manually by adding them on the Zone Transfers tab. To add a name server to the list, simply enter the IP address of the name server and click Add. When you choose this option, only the servers you specify in the list receive zone transfers.

![](img/763d5ae436311371600c0952a3da9094_192_0.png)

![](img/763d5ae436311371600c0952a3da9094_192_1.png)

# ENABLING REMOTE ACCESS SERVICE

Remote Access Service (RAS) allows remote network clients to establish a remote connection with a RAS server. After the connection is established, RAS clients function just like locally connected network clients—they can browse the network, access resources, and perform all tasks available through a local connection. A RAS client can perform all these actions, if they are allowed to by RAS configuration, and they can use the Active Directory.

Although RAS is not technically a part of Active Directory’s operation, I include it in this book because of its mature and growing usage. As more users become mobile, users will access RAS more often. RAS in Windows 2000, formally called Routing and Remote Access Service (RRAS) in Windows NT, is an integrated part of the operating system and is installed by default when you install Windows 2000 Server. In order to configure your server to be a RAS server, you have to enable RAS and configure it so it provides the functionality needed.

![](img/763d5ae436311371600c0952a3da9094_193_0.png)

- 1. Click Start->Programs->Administrative Tools->Routing and Remote Access.
- 2. The RAS snap-in appears with your server icon and a note about enabling RAS.

![](img/763d5ae436311371600c0952a3da9094_194_0.png)

# Why is RAS installed by default?

Windows 2000 expects you to use RAS. With the distributed nature of networks today and the mobility of users, most network environments need to use RAS to give remote network clients access to the network. Windows 2000 installs the service by default, but you can remove it from the system by using Add/Remove Programs in Control Panel if desired.

# Do I have to enable RAS?

RAS exists in your operating system, but it is not configured or enabled. If you want to use your Windows 2000 server as a RAS server, then you need to configure and enable RAS.

# If I enable RAS, can I later remove it from my server?

RAS is installed by default on your operating system. If you configure RAS for use, then later decide not to use the server as a RAS server, you can disable the service. See the next section to find out how to disable RAS.

![](img/763d5ae436311371600c0952a3da9094_194_1.png)

![](img/763d5ae436311371600c0952a3da9094_194_2.png)

- 2. Select your server, and then click Action>Configure and Enable Routing and Remote Access.
- 3. The Routing and Remote Access Configuration Wizard begins.
- 3. Click Next to continue.

# ENABLING REMOTE ACCESS SERVICE CONTINUED

To enable and configure RAS, you use the Action menu for your server. A wizard appears that guides you through the configuration process. As you configure RAS, you need to make some important decisions.

First, you can choose to allow your server to function as a router, for either the local network or for both local and remote networks (LAN and WAN). A router passes TCP/IP traffic to different subnets so that communication among subnets can occur. By selecting the check box, your server can function as a router and help manage network traffic.

Next, you have to click a check box to enable remote access. This allows remote clients to gain access to the local network through your server. These two features together enable you to configure your server for both routing and RAS, or as one or the other.

Next, you have to select which external adapters (such as NICs, modems, ISDN, and so on) are configured for routing and remote access. The options allow you to enable all external devices, enable all devices for routing only, enable all devices for remote access only, or choose to configure your devices individually.

![](img/763d5ae436311371600c0952a3da9094_195_0.png)

![](img/763d5ae436311371600c0952a3da9094_195_1.png)

- 4. Click this check box to enable your server as a router.
- 5. Click the appropriate radio button to enable local routing only or local and remote routing.
- 6. Click this check box to enable Remote Access.
- 7. Click Next to continue.
- 8. Click the appropriate radio button to configure your external adapter(s) as required.
- 9. Click Next to continue.

# What authentication and encryption methods should I use?

First, you can choose all methods. This allows clients to submit their passwords to the RAS server for authentication using any authentication method available, including clear text. Obviously, this choice is not very secure. You can also choose to use only methods that secure the users' passwords, which basically means that passwords must be encrypted. This feature is more secure, but may cause problems for some network clients. You can fine-tune these features after you configure the RAS server, and policies that you implement on your network also drive the configuration as well.

# Which protocol and access features should I use?

Next, you select the protocol that RAS users must use to connect to the RAS server. This is normally TCP/IP. You also select whether to allow RAS clients to access only the RAS server or the entire network. The entire network feature is less secure, but it gives the RAS users the most access to Active Directory and network resources.

![](img/763d5ae436311371600c0952a3da9094_196_0.png)

**10** Click the appropriate radio button to allow either all methods of authentication or only secure methods.

**11** Click Next to continue.

![](img/763d5ae436311371600c0952a3da9094_196_1.png)

**12** Select the protocol clients use for dial-up connections.

**13** Click the appropriate radio button for either Access this server only or Access entire network.

**14** Click Next to continue.
