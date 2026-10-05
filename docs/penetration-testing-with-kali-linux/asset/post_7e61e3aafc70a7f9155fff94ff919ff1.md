
# OffSec

The client's intent is to get an overview of the security status of all systems that are accessible by an external attacker. In most cases, we get a list of IP addresses the client wants to scan but occasionally, they want us to map all accessible systems and services by ourselves. While a company should know which of their systems are publicly accessible, it's not always the case. As a result, we will often find externally exposed systems and services that the company is not aware of.

On the other hand, there is the internal vulnerability scan where we have direct access to either a part of or the complete network of a client. When a client asks us with this kind of vulnerability scan, we either get VPN access or we perform the scan on-site. The intention is to get an overview of the security status of the internal network. It is important to analyze which vectors an attacker can use after breaching the perimeter.

The next scan types we will examine are authenticated and unauthenticated vulnerability scans. When we perform a vulnerability scan on a system without providing credentials, it is called an unauthenticated vulnerability scan. Unauthenticated scans are made to find vulnerabilities in remotely accessible services on a target. Therefore; they map the system with open ports and provide us with an attack surface by matching the information to vulnerability databases mentioned before.

However, we have no information about local security flaws, such as matching patches, outdated software, or configuration vulnerabilities on the system itself. For example, in an unauthenticated vulnerability scan on a Windows target, we cannot determine if the system is patched against the HiveNightmare vulnerability, which allows a privileged user to read sensitive systems. This is where authenticated scans come into play.

Most scanners can be configured to run authenticated scans, when the scanner logs in to the target with a set of valid credentials. In most instances, authenticated scans use a privileged account to have the best visibility into the target system. The goal of authenticated vulnerability scans is to check for vulnerable packages, matching patches, or configuration vulnerabilities.

We will perform both authenticated and unauthenticated scans in the next Learning Unit, but first, let's discuss how to obtain accurate and conclusive results.

## 7.1.3 Things to consider in a Vulnerability Scan

In this section, we will cover a few things we need to consider when planning and performing a vulnerability scan. In large engagements, we need to configure the vulnerability scanner carefully to get meaningful and relevant results.

The first consideration we'll discuss is the scanning strategy. Depending on the scanning type and number of targets, the duration of an automated scan can vary very much. Because external scans over the internet can be time consuming due to the number of hops and intermediate systems on the network route, it's important that we plan accordingly if we have a large list of IP addresses.

We also need to discuss target visibility. While it is easy to input an IP address and start the vulnerability scan, we have to properly consider our targets. It's important to determine if our targets are accessible without the need of VPNs or permissions in a firewall. In most cases, a client providing a list of IP addresses for an external scan can't cause concern. But if we are single-handling the attack surface of a client's publicly accessible infrastructure, we need to understand that firewalls and other access restrictions, could make systems and services inaccessible, which might be in place.

For example, an international client has several systems in multiple countries. They restrict access from all IP addresses outside of the country where each system is located. From our location, we are only able to access the systems in our country while all others are inaccessible to us.

Let's consider target visibility in an internal engagement. We need to think about our positioning in the network to get meaningful results, especially when we want to scan systems from other subunits. Keep in mind that firewalls, intrusion prevention systems (IPS), and intermediate network devices (such as routers), can filter or alter our traffic. One example of this is when a vulnerability scanner sends ICMP packets in the Host Discovery step and the intermediate device drops them. Hence, the scanner marks the target as offline.

In addition, our scan can be affected by rate limiting, which is used to limit the amount of traffic on a network. When our scan exceeds thresholds through packet count, connection or the source of our vulnerability scan can be drastically restricted in the context of networking capabilities. When the host discovery and service detection probes are rate limited the vulnerability scanner may miss hosts or services. Most vulnerability scanners can address this by specifying delays, timeouts, and limiting parallel connections.

Finally, let's review the network and system impact of vulnerability scans. A vulnerability scanner produces a lot of traffic in many configurations, especially if we want to scan multiple targets in a parallel way. This can easily make a network unusable. To address this, we could reduce the number of parallel scans or the scanning speed. An even bigger problem is the potential impact of our scan on the stability of a system. We need to consider that every vulnerability scan can bring instability to any system or service we scan.

## 7.2 Vulnerability Scanning with Nessus

This Learning Unit covers the Learning Objectives:

- Install Nessus
- Understand the different Nessus components
- Configure and perform a vulnerability scan
- Understand and work with the results of a vulnerability scan with Nessus
- Provide credentials to perform an authenticated vulnerability scan
- Gain a basic understanding of Nessus plugins

Penetration Testing with Kali Linux

In this Learning Unit, we will focus on Nessus, which is one of the most popular vulnerability scanners, containing over 67000 CVEs and 168000 plugins.

Nessus is available as Nessus Essentials and Nessus Professional. We will use the free version, Nessus Essentials, which comes with some restrictions and constraints. For example, we can only scan 16 IP addresses, and some templates and functions are not available. However, Nessus Essentials will give us insight into how to use the full commercial version and the general concepts discussed in this section will also apply to most commercial scanners.

### 7.2.1 Installing Nessus

For this Learning Unit, we will need to install Nessus on the Kali Linux VM, which is used to connect to the lab environment. An internet connection and email address will be necessary to download and activate Nessus. The minimum hardware requirements Tenable recommends are 4 CPU cores and 8GB of RAM. However, we need to meet these requirements for our exercises.

Nessus is not available in the Kali repositories and must be installed manually. We can download the current version of Nessus as a 64 bit deb file from the Tenable website, we also get the SHA256 and MD5 checksums for the installer.

Let's select Linux - deb: amd64 and download the installer.

![](img/336d6ea891e7464f18ad64426619ced4_167_0.png) Nessus for Kali

After downloading the installer, we will check the SHA256 checksum to validate it. To do this, we click the Checksum and copy the SHA256 checksum to the clipboard via the copy icon.
