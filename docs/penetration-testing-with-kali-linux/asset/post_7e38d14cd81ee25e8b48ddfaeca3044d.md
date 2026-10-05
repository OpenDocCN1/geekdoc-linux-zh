
## 7.2.3 Performing a Vulnerability Scan

In this section we will perform our first vulnerability scan. To begin, let's click on the New Scan button on the dashboard in the Scans tab.

![](img/336d6ea891e7464f18ad64426619ced4_174_0.png)

Figure 44. Creating a Scan

Nessus provides a list of the different templates. For this section, we will use the Basic Network Scan, which we can launch by clicking on it.

| VULNERABILITIES | | | | | |
| --- | --- | --- | --- | --- |
| Basic Network Scan A full systems scan for active ip range | Advanced Scan Configure a scan using all recommendations | Advanced Dynamic Scan Configure a dynamic plugin scan without remote checks | Malware Scan Scan for malware on Windows and other operating systems | Mobile Device Scan Audit mobile devices on Mobile Exchange and Android |
| Web Application Tests Scan for posted and customers using web applications | Credentialed Audit Authenticates to hosts and audits installed applications | Intel AMFT Security Bypass Remote and local checks for CVE-2017-5636 | Spectre and Meltdown Remote and local checks for CVE-2017-5714 and CVE-2017-5715 | WannaCry Ransomware Remote and local checks for WannaCry |
| Ripple20 Remote Scan A remote scan to detect vulnerabilities in Eternal Track Management of Privilege | Swirligate Remote and local checks to detect SMB vulnerabilities | ProxyLogon: MI Exchange Remote and local checks for Microsoft Exchange vulnerabilities | PrintNightmare Remote and local checks for PrintNightmare vulnerabilities |

Figure 45. Selecting a Basic Network Scan

This will present the scan configuration settings screen containing the BASIC, DISCOVERY, ASSESSMENT, REPORT, and ADVANCED settings.

¹16 (Tenable Docs, 2022), https://docs.tenable.com/nessus/Content/TemplateSettings.htm

# OffSec Penetration Testing with Kali Linux

### New Scan / Basic Network Scan

![](img/336d6ea891e7464f18ad64426619ced4_175_0.png)

Figure 46: Different Settings in Scan Configuration

The default screen is the General settings page with the two required arguments: a name for our scan and a list of targets. Nessus supports multiple target specifications,¹⁷ including a single IP address, an IP range, and a comma-delimited *Fully-Qualified Domain Name* (FQDN), or an IP address list.

For this example, we will scan the following machines: POULTRY, JENKINS, WK01, and SAMBA. We will enter "Basic Vulnerability Scan" into the Name field and the IP addresses of the machines into the Targets field.

### New Scan / Basic Network Scan

![](img/336d6ea891e7464f18ad64426619ced4_175_1.png)

> ¹⁷ (Tenable Docs, 2022), https://docs.tenable.com/nessus/Content/ScanTargets.htm

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# Penetration Testing with Kali Linux

Figure 47: Configuring Scan Name and Target List

Since we chose the Basic Network Scan template, Nessus has already configured most of the settings for us. However, the default configuration might not be exactly what we need. Depending on the scanning type, the environment, time, and the targets, we may need to adapt the settings to fit our needs.

In the default settings of this template, Nessus scans a list of common ports. For this demonstration, we only want to scan ports 80 and 443. To do this, let's click on the Discovery settings and select Custom in the dropdown menu.

![](img/336d6ea891e7464f18ad64426619ced4_176_0.png)

Figure 48: Selecting Custom Discovery Settings

The dropdown menu shown in Figure 48 provides us with a number of predefined options. To scan specific ports, we'll need to select Custom.

After we click on Custom, additional configuration menus appear under the DISCOVERY menu. We can now customize the Basic Network Scan template the same way as the Advanced Scan template in the DISCOVERY menu. Within the Port Scanning section, we will set the Port scan range to “80,443”. Additionally, we'll enable the option Consider unscanned ports as closed so Nessus treats others as closed, since we are only interested in ports 80 and 443.

### New Scan / Basic Network Scan

In this demonstration, we've customized the Basic Network Scan template to only scan two specific ports. But even in the default settings of this template, Nessus does not scan UDP ports. If we need to activate UDP port scanning, we need to manually configure it. We may miss crucial information on UDP services when it's disabled during assessments, but we need to understand that activating UDP port scanning will vastly increase the scan duration. Due to the nature of UDP, it is not often possible to tell the difference between an open and a filtered port.

To save time and scan the targets more quietly, we will turn off *Host Discovery* because we know the hosts are available. We do this by navigating to *Discovery > Host Discovery* where we toggle *Ping the remote host to Off*.

# OffSec Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_178_0.png)

Figure 50: Disable Host Ping in Discovery Settings

With the configuration of the scan definition, we did not configure any credentials, which implies that this scan will run unauthenticated.

We also did not change the default settings of the ASSESSMENT menu in the Basic Network Scan template. This means the brute forcing of user credentials will not be done. Even though brute forcing is disabled, our scan creates a lot of network traffic and we're scanning multiple hosts, which will be highly noticeable.

Now that we have a basic understanding of how we can customize templates to fit our needs, we can launch our first scan by clicking on the arrow next to Save and selecting Launch.

![](img/336d6ea891e7464f18ad64426619ced4_178_1.png)

Figure 51: Launching the Scan

Initially, the scan will have a status of Running in the Nessus dashboard under My Scans.

![](img/336d6ea891e7464f18ad64426619ced4_178_2.png)

Figure 51: Launching the Scan

# OffSec Penetration Testing with Kali Linux

# Penetration Testing with Kali Linux

Figure 52: Running Scan in Nessus

Figure 52 shows the running scan and provides the options to stop or pause it. Once the scan is finished, the status will change to Completed.

![](img/336d6ea891e7464f18ad64426619ced4_179_0.png)

Figure 53: Completed Scan in Nessus

# OffSec

### 7.2.4 Analyzing the Results

In this section we analyze the results of our first scan. Due to the continuous updates of Nessus, the results can differ. We can click on the scan in My Scans to get to the results dashboard.

![](img/336d6ea891e7464f18ad64426619ced4_179_1.png)

Figure 54: Result Dashboard

The initial view displays the Hosts page, which lists all hosts and provides a visual representation of the vulnerability data. This allows us to identify findings in one glance and gives us overview of the security status of each system. On the bottom right, Nessus displays a visual representation of the distribution of all targets' vulnerability information. Above it, we can find general information about the scan.

# OffSec Penetration Testing with Kali Linux

# Penetration Testing with Kali Linux

Figure 55: Vulnerability Result Dashboard of 192.168.50.124

To get the list of findings from a specific host, we can click on a list. This shows the list of vulnerabilities from the selected host. Let's click on the entry for 192.168.50.124.

![](img/336d6ea891e7464f18ad64426619ced4_180_0.png)

The severity column gives us a quick indicator if this is a critical finding or not. Figure shows us there are three findings with the MIXED severity. Nessus tells us this severity when it is grouped. The Count column shows how many findings the group contains. We can click on a grouped finding to display a list of all findings in that group. Let's click on Apache Http (Multiple Issues), which is listed as Web Servers under the Family.

![](img/336d6ea891e7464f18ad64426619ced4_180_1.png)

Figure 56: List of Grouped Findings

Figure 56 shows us information on the findings, which were previously grouped. We can get more information by clicking on a finding. Let's click on Apache 2.4.49 < 2.4.51 Path Traversal Vulnerability.
