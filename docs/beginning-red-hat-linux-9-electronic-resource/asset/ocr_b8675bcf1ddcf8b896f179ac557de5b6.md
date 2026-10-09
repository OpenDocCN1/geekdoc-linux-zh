# DNS

Rather than remember the IP address of the Wrox web site, it is easier for us to remember **www.wrox.com**. **Domain Name System** (DNS) servers provide the mapping between human-readable addresses (such as www.wrox.com) and the IP addresses of the machines acting as the web servers for the corresponding web service. Applications such as web browsers and e-mail clients require the IP address to connect to a web site or a mail server respectively. In order to get this from the human-readable input that we provide them with, they query a DNS server for the corresponding IP address information. Obviously, this also means that the browser and other clients on the machine need to know the IP address of the DNS server. For machines that use DHCP, the information about the DNS server is automatically available when the machine is configured.

# Other Connection Types

The Internet Connection Wizard also allows us to configure some of the less common types of connection devices, such as ISDN and Token Ring adapters:

![](bbox=[0.17, 0.39, 0.86, 0.74])

External ISDN terminal adapters (the ones that are connected to the serial port on a machine) can be configured **just like ordinary analog modems**. This discussion deals with ISDN adapters that are **internal ISDN cards**. In this case, we need to know the name of the adapter, its IRQ, the IO address and the D-Channel protocol used, so as to configure it properly. This information should be available as part of the vendor's documentation for your adapter (if you've not got it you could try calling them, or using **Google** if you've a second machine). Similarly, for configuring a Token Ring adapter, we need to know the name of the adapter we intend to use before we can configure it.