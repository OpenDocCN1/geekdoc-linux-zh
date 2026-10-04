# Hunting for High Severity Vulnerabilities (HSV) • Chapter 3

signatures, they can report both false positives and false negatives. This means you may ultimately need to verify the results by hand.

# Host Discovery

Host discovery is a process in which the scanner checks the network and finds all of the live hosts that should be included in the scan. Most scanners use a mix of the Internet Control Message Protocol (ICMP), Transmission Control Protocol (TCP), User Datagram Protocol (UDP), and/or MS Networking to determine active hosts.

ICMP Echo is the most popular choice, and almost every scanner supports it. ICMP Timestamp and Netmask are some secondary ICMP types used for host detection in VA tools.TCP or UDP pings for host detection work well for external scanning or heavilywalled environments. They probe for the presence of an active service in a port scan, usually with a smaller list of ports to scan. Discovery via Network Neighborhood is really only appropriate when dealing with Windows-only VA tools, non-Windows hosts would be excluded from the scan.

If the host detection method employed by the scanner does not work well on your network, most scanners will allow you to scan addresses that did not respond to host discovery, although this usually has the effect of slowing down the scan.

# Service Discovery/Enumeration

In performing service discovery, the VA tool will at least perform a port scan to identify services available to the vulnerability checks. Scanners typically will not check all 65,000+ TCP and UDP ports because of the time involved, but you should check the products port list to make sure it covers the critical application on your network.

Some scanners also perform service enumeration (that is, banner grabbing), during this phase. Banner grabbing allows you to see what the server returns if queried for a response.This can be useful in identifying application versions for common and uncommon ports.

# Vulnerability Checking

Vulnerability checking is the heart of any VA scanner. Vulnerability checking is done in a variety of ways, but it usually boils down to an application version check, reproduction of the vulnerability, or looking for signs of the vulnerability, such as telltale files.

![](bbox=[0.707, 0.943, 0.929, 0.966])