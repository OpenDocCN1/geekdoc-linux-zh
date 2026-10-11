
## TIPS

### What settings can I edit on the Encryption tab?

You have the selection of no encryption, basic, or strong. You can use any combination of these, only one, or all of them. With one selection, users are restricted to that method. For example, if you select only strong encryption, then all connections require strong authentication. If all your RAS clients are capable of strong encryption, then this is the most secure choice. However, you may need to allow a combination of strong and basic (or even no encryption) to service all clients.

### What settings can I edit on the Advanced tab?

On the Advanced tab, you can specify additional attributes for policy. By clicking the Add button, you have an extensive list of attributes that you can use to meet the RAS needs of your organization. For example, if you are using a RADIUS server, you can add attributes for that server. If you are using AppleTalk or other networking methods, such as ATM, you can add attributes for those as well.

![](img/763d5ae436311371600c0952a3da9094_218_0.png)

- 12. Click the Encryption tab.
- 13. Click the appropriate check boxes to enforce certain levels of encryption.
    - You can select all for the most leniency.
- 14. Click the Advanced tab.
- 15. Use the Add, Remove, or Edit buttons to manage additional connection attributes that you want to enforce for the policy.
- 16. Click OK to save the changes.

## CONFIGURING RAS PORTS

Ports allow communication to flow in and out of a computer. Different devices can be connected to these ports that enable network communication. In the RAS snap-in, a Ports icon appears under the server name. The actual ports that can be configured appear in the details pane. You may see a number of port types, such as various WAN Miniports for PPTP (VPN) connections and L2TP (Layer 2 Tunneling Protocol)—also for VPN connections. For each device, you can check the status (connected or not) and you can reset it.

Concerning port configuration, you can select Ports in the console and access the Properties sheet in the Action menu. From this view, you can select any device attached to your server that RAS uses and click the Configure button. Then you can make selections about how the device should be used, such as for inbound and outbound RAS and demand-dial connections.

![](img/763d5ae436311371600c0952a3da9094_219_0.png)
![](img/763d5ae436311371600c0952a3da9094_219_1.png)

- 1. Select Ports in the console.
- 2. Choose Action: Properties.

### What is the demand-dial routing option for?

You can configure your devices to inbound (RAS) connections or for inbound and outbound (RAS and Routing) connections. The demand-dial feature is used by Routing to establish remote connections with other RAS servers in a WAN. Because the feature is demand-dial, a connection is established only when a “demand” exists to send data. This feature is particularly helpful to conserve bandwidth or connection time on slow or leased WAN links. Because there is not a persistent connection, the demand-dial component allows a connection to be established when there is a need for routing communication to occur.

### What is the phone number box for?

Each device, depending on your configuration, may have its own phone number that users dial to access your RAS server. Depending on the device, this dialog box appears for you to enter the phone number.

![](img/763d5ae436311371600c0952a3da9094_220_0.png)

- 1. Select a device in the list.
- 2. Click Configure.

![](img/763d5ae436311371600c0952a3da9094_220_1.png)

- 3. Click the appropriate check boxes for your configuration.
- 4. Type a phone number if necessary.
- 5. Click OK.

## CONFIGURING IP ROUTING

Depending on your system configuration, you may have an IP Routing icon in the console and perhaps an IPX Routing icon. Both of these function in a similar fashion and are used for IP and IPX routing purposes. This section focuses on IP because it is the most common, and if you are using IPX, it is configured in a similar way.

For the most part, IP routing takes care of itself. You do have some configuration options through the properties sheets, and, mostly, you can use the icon and the actual routing icons in the details pane to gain TCP/IP information, which is especially helpful for troubleshooting purposes.

On the properties sheets, you have four major tabs. First, the General tab allows you to enable IP router manager, which is automatically selected. You can also enable router discover advertisements. This feature allows your router to learn about routing table updates through discover advertisement packets. Windows 2000 sends these packets using multicast ICMP messages. Although helpful, they may produce a lot of excessive traffic on your network.

![](img/763d5ae436311371600c0952a3da9094_221_0.png)

- 1. Expand IP Routing in the console and select General.
- 2. Select a desired IP connection in the details pane.
- 3. Click the Action menu.
    - From this menu, you can gain TCP/IP information by simply selecting the category to display the desired information.

![](img/763d5ae436311371600c0952a3da9094_222_0.png)

### What are the TCP/IP information options for the IP connections?

Find the following TCP/IP information by selecting the connection in the details pane and clicking the Action menu.

- Show TCP/IP Information: Shows basic TCP/IP configuration information.
- Show Address Translations: Shows the number of network address translations that have occurred.
- Show IP Addresses: Shows the IP address and subnet masks of the connections.
- Show IP Routing Table: Shows the IP routing table including IP address, subnet mask, and default gateway.
- Show TCP Connections: Shows all network connections that occurred through TCP.
- Show UDP Listener Ports: Shows all UDP ports that are available.

![](img/763d5ae436311371600c0952a3da9094_222_1.png)
![](img/763d5ae436311371600c0952a3da9094_222_2.png)

- 4. Choose *Action* → *Properties*.
- 5. Select the appropriate check boxes to enable IP router management and router discovery advertisements.

## CONFIGURING IP ROUTING CONTINUED

On the Configuration tab, you can choose for the device to obtain an IP address from the DHCP server or you can specify a static IP address. Under many circumstances, you may prefer to use a static IP address for RAS IP Routing devices.

The Multicast Boundaries tab enables you to define a multicast scope for multicasting communication. *Multicasting* is the process of sending messages or communication to a group, much like you would send a group e-mail message. You must have multicasting scopes configured in the properties of the IP Routing General icon in the RAS console for this action to be available.

Finally, the Multicast Heartbeat tab enables you to enable multicast heartbeat detection. This feature listens for periodic multicast traffic to determine that multicasting is functioning properly on your network. The heartbeat detection determines this by an acceptable quiet time. If quiet time goes higher than the configured amount (default of ten minutes), an alert is sent to the administrator.

![](img/763d5ae436311371600c0952a3da9094_223_0.png)

- 1. Click the Configuration tab.
- 2. Click the appropriate radio button for the device to obtain an IP address for DHCP or specify one manually.
- 3. Click the Advanced button.

![](img/763d5ae436311371600c0952a3da9094_223_1.png)

- 4. Use the Add, Edit, or Remove buttons to manage the IP address(es) and default gateway(s) for the device.
- 5. Click OK.

## TIPS

### Should I allow my RAS devices to receive an IP address from DHCP?

Under normal circumstances, the best advice is to use a static IP address for all server hardware because dynamic IP addresses can cause communication problems, especially in the case of a router. You can choose DHCP, but you may experience some communication problems.

### Why is it called a multicast heartbeat?

The heartbeat detection listens to multicast traffic on your network to determine if the traffic flow is normal. Much the same way that a doctor listens to a human heart for a pattern or rhythm, the multicast heartbeat listens to the traffic and sends an alert after an acceptable amount of quiet time has passed. A quiet time that is too long may indicate that multicast communication problems exist.

![](img/763d5ae436311371600c0952a3da9094_224_0.png)
![](img/763d5ae436311371600c0952a3da9094_224_1.png)

- 1. Click the Multicast Boundaries tab.
- 2. Click the drop-down box to select a Multicast scope.
- 3. Click the Add button to define a multicast boundary.
- 4. Click this check box to activate the TTL boundary, and enter TTL values as desired.
- 5. Click the Multicast Heartbeat tab.
- 6. Click this check box to enable multicast heartbeat detection.
- 7. Adjust the quiet time if desired.
- 8. Click OK to save the changes.
