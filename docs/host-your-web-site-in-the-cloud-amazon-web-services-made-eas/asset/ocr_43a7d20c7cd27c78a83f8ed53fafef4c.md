100 Host Your Web Site in the Cloud

+   1. locate or acquire suitable server hardware
+   2. acquire and attach adequate disk storage
+   3. ensure adequate rack space, power, and cooling
+   4. arrange for internet connectivity
+   5. procure and set up networking gear such as switches, routers, and load balancers
+   6. install the hardware
+   7. boot the server
+   8. install the operating system
+   9. configure necessary applications
+   10. allocate and route IP addresses
+   11. make firewall entries for access and protection
+   12. configure monitoring to verify that the system is functional
+   13. scale all of the above components in response to increasing traffic

Each of these steps is time-consuming and the labor involved expensive when done by hand. A programmable data center replaces each step with equivalent API calls and shrinks the time needed to complete each step from hours, days, or weeks to seconds. This rapid-response, mass production model is a key aspect of cloud computing.

Programmable configuration control also simplifies growth and evolution, since additional resources are readily available.

# # Amazon EC2 Overview

The Amazon EC2 infrastructure exhibits all the concepts of the programmable data center that I listed above. In fact, Amazon EC2 services provide access to multiple data centers (Availability Zones) in multiple geographic regions and are really a collection of programmable data centers. You simply make web service requests “to the cloud” and Amazon EC2 capabilities do the rest. Servers, operating system images, firewall entries, load balancers, IP addresses, and disk storage volumes are all available in a matter of seconds. In this section, we’ll address the difference between persistent and ephemeral resources, cover the key Amazon EC2 concepts, review the pricing model, and discuss the ways the EC2 infrastructure works with other AWS infrastructure services.