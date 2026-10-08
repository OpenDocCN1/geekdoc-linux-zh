
# Wireless network warning

![](img/8c094d1b36276212c03d10d898508a6e_112_0.png)

Wi-Fi, the standard for wireless technology, uses an encryption system named wireless equivalent privacy (WEP) to provide security. WEP encrypts communication between wireless devices to prevent someone with the right equipment from listening to and using your wireless network. But WEP is flawed and can be broken using tools available on the Internet (that's a big surprise). If a hacker breaks in to your Wi-Fi network, he can read your communications. But your problems don't end there. Hackers can use your wireless network to connect to both your private network and the Internet; you give the bad guys a free lunch and a launch pad to the Internet.

On the other hand, wireless networking is so useful that many people make accommodations for the risk. The logic? If you assume that your wireless network has already been hacked, you don't have to worry when it might be hacked in the future.

You should use OpenSSH, Secure Sockets Layer (SSL), and virtual private networks (VPN) — all bundled with Red Hat Linux — to conduct all your internal and external communication. Keep in mind that using SSH, SSL, and VPN protects your information, but doesn't prevent someone from connecting to your network. The next generation of Wi-Fi, 802.11g, is supposed to fix the WEP weakness. Until the WEP problems are solved, be aware of the risks.

## Configuring your Ethernet or wireless NIC

To get your Red Hat Linux computer working on a LAN, you must first configure its network interface card, or NIC. The NIC is the device that electronically connects your computer to your LAN. To work with the other computers on your network, your Ethernet or wireless adapter must be given a network address and a few other pieces of information.

![](img/8c094d1b36276212c03d10d898508a6e_112_1.png)

We have divided the configuration instructions between Ethernet and wireless (or Wi-Fi) NICs. The instructions start by explaining how to start the Red Hat Network Configuration Utility. We then devote a subsection apiece to describing the particulars of configuring Ethernet and wireless devices. After we cover the device specifics, we discuss general configuration issues. The overall configuration process is outlined in these steps:

- 1. Start the Network Configuration Utility.
- 2. Configure your Ethernet or wireless device.
- 3. Configure your computer's host name.
- 4. Configure your computer's domain name service.
- 5. Restart your network.

## Starting the Network Configuration Utility

Follow these steps to start the Network Configuration Utility:

- 1. Click the **GNOME Main Menu button** and choose **System Settings→ Network**.

    *TIP*
    Alternatively, you can click the GNOME Menu button and choose **System Tools→Network Device Control**. When the Network Device Control window opens, select the Ethernet or wireless device and click the **Configure** button. The Network Configuration Utility starts.

- 2. Enter the **root password** if you're prompted to do so.

    Figure 7-1 shows the initial configuration window. A NIC may or may not be displayed in the window. The NIC is displayed only if you configured your networking during the Red Hat installation.

    ![](img/8c094d1b36276212c03d10d898508a6e_113_0.png)

- 3. Click the **New** button if no NIC is displayed on the **Devices** tab or if you want to configure an additional one.

    Otherwise, skip to Step 3 in the following section when you're working with an Ethernet device; skip to Step 1 in the section “Configuring a wireless NIC,” later in this chapter, if you're working with a Wi-Fi NIC.
    The Select Device Type window appears.

- 4. Select the appropriate type from the list of devices and then click the **Forward** button.

    For example, select **Ethernet** if you're using that type of interface. If you're using a Wi-Fi (also referred to as wireless or IEEE 802.11b) device, select **Wireless Connection**.

What you do next depends on whether you're configuring an Ethernet or a wireless NIC. The following two sections are devoted to Ethernet and wireless NICs, respectively.

## Configuring an Ethernet NIC

If you're using an Ethernet NIC, follow the steps in this section to configure its parameters (if you're using a wireless NIC, go to the following section):

- 1. **Follow the steps in the section “Starting the Network Configuration Utility,” earlier in this chapter.**

    When you choose Ethernet from the drop-down list in Step 4 on the preceding list, the Select Ethernet Device window appears.

- 2. **Select the appropriate Ethernet device and click the Forward button.**

    The Network Configuration utility detects all Ethernet devices attached to your computer. Most PCs have only one Ethernet device, so you don't have to make a decision about which one to select.

    The Configure Network Settings window opens as shown later in this section, in Figure 7-2.

- 3. **Configure your TCP/IP address settings.**

    The Red Hat Network Configuration Utility selects DHCP (Dynamic Host Configuration Protocol) as the default method for determining your machine's IP address. (DHCP dynamically assigns an IP address and other parameters to your Ethernet NIC, and you're finished configuring your NIC.) If you're connecting to a network that provides DHCP service, type your computer name in the Hostname (optional) field (for example, Cancun), click the Forward button, and go to Step 9.

    If your network doesn't use DHCP, you need to manually configure your IP address. Proceed to Step 4.

- 4. **Click the Statically Set IP Addresses radio button.**

    You should ask your friendly local system administrator (unless you're the administrator, in which case you may want to avoid talking to yourself) which system your network uses.

    Life is a bit more complicated if you have both a wireless and an Ethernet NIC on your computer. You can run both devices at one time, but the configuration is more difficult. You can solve the problem by clicking the Automatically Obtain IP Address Settings With radio button so that the dot disappears. This simple mouse click prevents the Ethernet NIC from starting automatically.

    ![](img/8c094d1b36276212c03d10d898508a6e_114_0.png)

- 5. **Assign an IP address to your computer by typing it in the Address text box.**

    ![](img/8c094d1b36276212c03d10d898508a6e_115_0.png)

    IP addresses are analogous to street addresses: They provide a number that uniquely distinguishes your machine from all others. Private IP addresses don’t require any registration with the powers that be — the InterNIC organization that distributes IP addresses. Public IP addresses aren’t routed on the Internet and can be used on LANs for your own use.

    If you’re on a network with registered IP addresses, be sure to get an IP address from your system administrator. Otherwise, go ahead and use a private IP address. (Use any Class C address between 192.168.1.1 and 192.168.254.254; for example, 192.168.1.20 or 192.168.32.5.) Private IP addresses in this range are designated for use by private networks. By design, private IP addresses don’t get *routed* (sent from one machine to another) through the Internet, and anyone can use them. Private IP addresses would wreak havoc on the Internet if they were routed.

- 6. **Type 255.255.255.0 or the netmask for your IP address in the Subnet Mask text box.**

    ![](img/8c094d1b36276212c03d10d898508a6e_115_1.png)

    The Internet Protocol (IP) defines only three network address classes: A, B, and C. Only Class C addresses are assigned by InterNIC. Use the 255.255.255.0 netmask for Class C networks, 255.255.0.0 for Class B, and 255.0.0.0 for Class A.

    ![](img/8c094d1b36276212c03d10d898508a6e_115_2.png)

    Class C netmasks are used almost universally now, and we use only Class C addresses here. If you’re not using a Class C address, you’re probably experienced in the ways of TCP/IP and know which netmask to use. Godspeed. Otherwise, don’t fool with Mother Nature: Use a Class C address.

- 7. **In the Default Gateway Address text box, type the IP address of the Internet gateway for your LAN.**

    The Internet gateway is the device (router or computer) that connects your network to your ISP and the Internet. Obtain the address from your system administrator if you’re at work and have one. If you’re a home user, a typical convention is to assign the highest address — 254 — of a Class C subnetwork as the gateway. For example, type 192.168.1.254.

    Your TCP/IP Settings should look similar to the dialog box shown in Figure 7-2.

- 8. **Click the Forward button.**

    The Create Ethernet Device dialog box opens, indicating that you have finished the configuration process. The dialog box shows a summary of the information you entered in the preceding steps.

- 9. **Review the summary and click the Apply button.**

    You return to the Network Configuration window that now displays the newly configured Ethernet NIC.
