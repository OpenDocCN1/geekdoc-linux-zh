![](bbox=[0.15, 0.1, 0.75, 0.35])

# Gathering Software Information

Although hardware information is valuable to obtain prior to installing Linux, the Linux installation program also asks for several software settings, such as the time zone and language support. Most of these software settings need not be documented prior to installation as they can be added during installation at the discretion of the user. Some settings, however, should be researched before starting the installation; these settings include the system network configuration and the package selections.

If you are installing a Linux system to use or provide network services, the installation program prompts for the necessary values to complete the configuration of the NIC in the computer. These values are usually assigned by the network administrator or Internet service provider (ISP) for the company. A summary of these settings is described in the following list:

+   - **Host name**—The name of the computer that is registered in the Domain Name Service (DNS) so that others can connect to it by name.
+   - **IP address**—The unique number assigned to the computer that allows it to participate on an Internet Protocol (IP) network such as the Internet.
+   - **Netmask**—Also known as the network mask or subnet mask, it specifies which portion of the IP address identifies which logical network the computer is on.
+   - **Gateway**—Also known as the default gateway or gateway of last resort, it specifies the address of a computer that accepts information from the local computer and sends it to other computers if the local computer cannot.
+   - **DNS servers**—These servers resolve fully qualified domain names (FQDNs) such as www.linux.org to IP addresses so that users can connect to those addresses across the Internet. You can list more than one DNS server; the local computer then tries the second server in the list if the first one is unavailable, and so on.

You can configure the previous settings manually during the installation program or have the settings automatically configured, provided a **Dynamic Host Configuration Protocol (DHCP) server** exists on the network. If you select the option to use DHCP during installa-