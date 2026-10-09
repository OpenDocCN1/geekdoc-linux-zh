
### Disable the NIC

- Enter `cd /etc/sysconfig/network-scripts` and delete the corresponding `ifcfg-eth{Number}` file in the directory.
- Or, enter `ifdown eth{Number}`.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_498_0.png)

## Delete a NIC

To delete any NIC devices, delete the corresponding `ifcfg-eth{Number}` file located in the `/etc/sysconfig/network-scripts/` directory.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_498_1.png)

## Procedure Reference: Configure a Wireless Network Interface Using the iwconfig Command

To configure a wireless network interface using the `iwconfig` command:

1. Log in as root in the CLI.
2. Specify the different parameters for the wireless interface.
   - Enter `iwconfig (device number) essid (ess id | network name)` to set the network name for the wireless device.
   - Enter `iwconfig (device number) nwid (network id | domain id)` to set the network id for the wireless device.
   - Enter `iwconfig (device number) nickname (nickname)` to specify the nickname for the wireless device.
   - Enter `iwconfig (device number) mode {Ad-Hoc|Managed|Master|Repeater|Secondary|Monitor|Auto}` to set the mode of the wireless device.
   - Enter `iwconfig (device number) freq|channel (frequency value | channel number)` to set the frequency or channel for the wireless device.
   - Enter `iwconfig (device number) ap (access point id)|any|off` to set the access point for the wireless device.
   - Enter `iwconfig (device number) rate (bit rate)|auto)` to set the bit-rate for the wireless device.
   - Enter `iwconfig (device number) key (key value)` to set the encryption key for the wireless device.
3. View the details of the configured wireless devices.
   - Enter `iwconfig` to view the details of all the configured wireless devices.
   - Enter `iwconfig (device number)` to view the details of a specific wireless device.
4. Restart the network service to apply the changes.

## Procedure Reference: Configure the LDAP Client

To configure the LDAP client:

1. Log in as root in the CLI.
2. Enter `authconfig-tui` to use the Authentication Configuration utility to configure the LDAP client.
3. In the Authentication section, select **Use LDAP Authentication**.
4. Press F12 to go to the next screen.
5. If necessary, in the **LDAP Settings** screen, check the **Use TLS** option to transfer the encrypted password.
6. In the **Server** text box, type the LDAP server information.
7. In the **Base DN** text box, type the base distinguished name.
8. Press F12 to finish and close the wizard.

## ACTIVITY 12-1

### Connecting to a Network Manually

**Before You Begin:**

1. The system, srvB, is rebooted and the GUI login screen is displayed.
2. Log in to the GUI as root.
3. Switch to the first terminal of the CLI.

**Scenario:**

You are working as a system administrator in a startup company. Your responsibilities include setting up and configuring network connectivity in your organization. An employee has joined your organization. You need to assign the employee a system and make it part of the existing network. The network configuration details of the system are as follows:

- IP address of the system: 192.168.0.248
- Netmask: 255.255.255.0

**What You Do** | **How You Do It**
--- | ---
1. Identify the IP address of the system. | a. Log in as **root** in the CLI.<br>b. Enter `ifconfig` to view the inet addr: 192.168.0.X<br>![](img/477ccb2f05b6ba1b2d563ea74f18c197_500_0.png)<br>![](img/477ccb2f05b6ba1b2d563ea74f18c197_500_1.png)<br>c. Observe that the results contain details about Ethernet and loopback devices. In addition, observe that the HWaddr is displayed along with the details about the received (RX) and transmitted (TX) packets.<br>d. Enter `clear` to clear the terminal screen.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_500_2.png)

The DHCP server (the system designated as the instructor server) will provide different IP addresses to all students on a first-come, first-served basis. The IP address specified in the scenario (192.168.0.248) is only for one student and is used specifically to suit online course needs. In a classroom setup, the host octet value will vary for all students and therefore, will be represented by an X sign (192.168.0.X), which is the host octet value ranging from 10 to 253. Each student will be requested to use the IP addresses provided to their respective systems by the DHCP server.

2. Configure the IP address manually.

a. Enter `cd /etc/sysconfig/network-scripts` to change to the network-scripts directory.

b. Enter `vi ifcfg-eth0` to open the device file.

c. Observe that the default configuration of the NIC is displayed.

d. Change `BOOTPROTO=dhcp` to `BOOTPROTO=static` and press Enter.

e. Enter `IPADDR=192.168.0.X` to set the IP address for the NIC device.

f. Enter `NETMASK=255.255.255.0` to specify the netmask address.

g. Press `Esc` to switch to the command mode.

h. Save and close the file.

i. Enter `service network restart` to restart the network service.

j. Enter `clear` to clear the terminal screen.

3. Test the network connectivity.

a. Enter `ping -c 5 192.168.0.2` to check network connectivity.

b. Observe that the response from `192.168.0.2` is displayed five times with the `ttl` and `time`, which indicates that the network is functional. In addition, observe that the statistics section displays details about the number of packets transmitted and received, percentage of packet loss, and total time taken.

c. Enter `clear` to clear the terminal screen.

# TOPIC B

## Configure Routes

You configured the IP settings for network interfaces. Routing allows you to manage data transmission traffic on networks. It enables data to be transmitted from a source to its destination through different routes. In this topic, you will configure routes.

Computers on a network interact with each other simultaneously at numerous instances. If one computer on a network communicates with many computers at the same time, and if the data transmission routes or communication paths are not configured, it may lead to a system crash due to flooding of information. Therefore, the routes for information transmission have to be configured to avoid collision in network traffic.

### Routers

**Definition:**

A router is a networking device that connects multiple networks. Routers enable data to be exchanged among networks by examining and determining the best network path for data to travel. A router can be a dedicated device or can be implemented as a software application running on a network enabling device.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_502_0.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_502_1.png)

*Figure 12-12: A router connecting two networks.*

### Routing

**Definition:**

Routing is the process of selecting the best route for moving data packets from a source to its destination on a network. To assist the process of routing, a router applies appropriate algorithms to generate and maintain an information base about network paths. It considers various metrics, such as the path bandwidth, path reliability, and communication costs, while evaluating the available network paths to determine the optimal route for forwarding a packet. Once the optimal route for a packet is assigned, packet switching is done to transfer the packet from the source host to the destination host.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_502_2.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_503_0.png)

*Figure 12-13: Example of routing on a network.*

### Packets

A *packet* is a formatted unit of data being sent across a network. In addition to the user data, it comprises control information, such as the source and destination addresses, which is required to deliver the user data. A packet is also known as a *datagram*.

### Packet-Switching Technology

Packet-switching technology is used for transmitting data among computers on a network. In a packet-switched network, a message is broken into packets, which are transmitted individually or switched to their required destination. During the process, each packet may follow a different path, but at the destination, the packets are reassembled to form the original message sent from the main destination. This technology ensures greater routing and transporting efficiency on a network. The Internet is a packet-switched network.

### Benefits of Packet-Switched Networking

The benefits of a packet-switched network lie in the underlying technology of dividing a message to be sent over the Internet into packets. When data is transported in packets rather than in one big stream of data, the packets do not all have to move through the same path. Because the data is broken up into small packets, the packets can be sent across the Internet over various paths, eventually (in a fraction of a second) reaching their destination, where the packets can be reassembled into the original data. This means that one or more of the smaller networks, which make up the Internet, can go out of service without preventing the packets from ultimately reaching their destination, because the packets can simply take a different path to get there. If a few packets never reach their destination, they can be resent over a different path.

If files were not broken up into smaller packets, the entire file will have to be resent if any part of it did not reach the destination intact. Having multiple paths and breaking up files into small packets increase the reliability of the network.
