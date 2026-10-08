What you do next depends on whether you're configuring an Ethernet or a wireless NIC. The following two sections are devoted to Ethernet and wireless NICs, respectively.

# Configuring an Ethernet NIC

If you're using an Ethernet NIC, follow the steps in this section to configure its parameters (if you're using a wireless NIC, go to the following section):

+   1. **Follow the steps in the section “Starting the Network Configuration Utility,” earlier in this chapter.**

   When you choose Ethernet from the drop-down list in Step 4 on the preceding list, the Select Ethernet Device window appears.

+   2. **Select the appropriate Ethernet device and click the Forward button.**

   The Network Configuration utility detects all Ethernet devices attached to your computer. Most PCs have only one Ethernet device, so you don't have to make a decision about which one to select.

   The Configure Network Settings window opens as shown later in this section, in Figure 7-2.

+   3. **Configure your TCP/IP address settings.**

   The Red Hat Network Configuration Utility selects DHCP (Dynamic Host Configuration Protocol) as the default method for determining your machine's IP address. (DHCP dynamically assigns an IP address and other parameters to your Ethernet NIC, and you're finished configuring your NIC.) If you're connecting to a network that provides DHCP service, type your computer name in the Hostname (optional) field (for example, Cancun), click the Forward button, and go to Step 9.

   If your network doesn't use DHCP, you need to manually configure your IP address. Proceed to Step 4.

+   4. **Click the Statically Set IP Addresses radio button.**

   You should ask your friendly local system administrator (unless you're the administrator, in which case you may want to avoid talking to yourself) which system your network uses.

   Life is a bit more complicated if you have both a wireless and an Ethernet NIC on your computer. You can run both devices at one time, but the configuration is more difficult. You can solve the problem by clicking the Automatically Obtain IP Address Settings With radio button so that the dot disappears. This simple mouse click prevents the Ethernet NIC from starting automatically.

![](bbox=[0.13, 0.75, 0.23, 0.85])

+   5. **Assign an IP address to your computer by typing it in the Address text box.**