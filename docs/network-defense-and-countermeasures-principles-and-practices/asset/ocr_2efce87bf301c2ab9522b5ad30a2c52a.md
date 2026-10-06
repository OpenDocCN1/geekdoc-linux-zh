# Implementing VPN Solutions

Regardless of which protocols you use for your VPN, you must implement your choice in some software/hardware configuration. Many operating systems have built-in VPN server and client connections. These are generally fine for small office or home situations. However, they might not be adequate for larger scale operations in multiple users connect via VPN. For those situations, a dedicated VPN solution might be necessary. This section discusses some of those solutions.

# Cisco Solutions

Cisco offers VPN solutions, including a module (https://www.cisco.com/c/en/us/products/collateral/2800-series-integrated-services-routers-isr/prd_qas0900aecd80516d81.html) that can be added to any of their switches and routers to implement VPN services. It also offers client-side hardware that is designed to provide an easy-to-implement yet secure client for the VPN.

The main advantage of this solution is that it incorporates seamlessly with other Cisco products. Administrators using a Cisco firewall or Cisco routers might find this solution to be preferable. However, this solution might not be right for not using other Cisco products and those who don't have knowledge of Cisco systems. However, many attractive specifications for this product include the following:

+   - It can use 3DES encryption (an improved version of DES). But AES is preferred and strongly recommended.

+   - It can handle packets larger than 500 bytes.

+   - It can create up to 60 virtual tunnels per second, a good feature if a lot of users might be logging on or off.

# Service Solutions

In some cases, especially with large VPN situations, you might not want to invest the time, energy, and cost to establish, secure, and monitor VPN connections. You can contract this entire process, the setup and the administration, to VPN vendors. AT&T provides this service for many companies.

Service solutions have the advantage of not requiring any particular VPN skill on the part of the internal IT department. A department that lacks this specific skill areas but wants to implement a VPN might find that using an outside service is the right solution.

# Openswans

The Openswan product (www.openswan.org/) is an open source VPN solution available for Linux operating systems. As an open source product, one of its biggest advantages is that it is free. Openswan uses IPSec, making it a highly secure VPN solution.