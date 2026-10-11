
![](img/ec25e59d75726b7041242a56d3376832_216_0.png)

*Figure 53: Creating a Scan*

Nessus supports a number of scan types, including:

- **Basic Network Scan:** Generic scan with various checks that are suitable to be used against various target types.
- **Credential Patch Audit:** Authenticated scan that enumerates missing patches.
- **Web Application Tests:** Specialized scan for discovering published vulnerabilities in Web Applications.
- **Spectre and Meltdown:** Targeted scan for the Spectre[^231] and Meltdown[^232] vulnerabilities.

We recommend investigating these scan types, but for this introductory section, we will focus on a standard, basic network scan, which we can launch by clicking on *Basic Network Scan*.

[^231]: (Wikipedia, 2020), https://en.wikipedia.org/wiki/Spectre_(security_vulnerability)
[^232]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Meltdown_(security_vulnerability)

### Scan Templates

![](img/ec25e59d75726b7041242a56d3376832_217_0.png)

*Figure 54: Selecting a Basic Network Scan*

This will present the scan configuration settings screen with two required arguments: a name for our scan and a list of targets. Nessus supports adding targets as an IP address, an IP range, or comma-delimited FQDN or IP list.

For this example, we will scan the Gamma machine in the PWK labs, which has an IP address of 10.11.1.73. We will enter “Gamma - Basic” into the Name field and the IP address into the Targets field:

![](img/ec25e59d75726b7041242a56d3376832_218_0.png)

In this scenario, we have selected the Basic Network Scan template definition which, like all other templates, comes preconfigured with default user settings. However, these defaults might not be exactly what we are looking for and we must take into consideration our environment, our time constraints, and the target that will be scanned. Some things to consider when configuring the Basic Network Scan template include:

1. Are our targets located on an internal network or are they publicly accessible?
2. Should the scanner attempt to brute force user credentials?
3. Should the scanner scan all TCP and UDP ports or only common ports?
4. Which checks should the scanner run and which ones should it avoid?
5. Should the scanner run an Authenticated Scan or an Unauthenticated Scan?

For this scan, we want to run an initial basic port scan against *ALL* ports. By default, the *Basic Network Scan* will only scan the common ports. To change this, we click the *Discovery* link on the left side of the *Settings* tab.

![](img/ec25e59d75726b7041242a56d3376832_219_0.png)

*Figure 56: Accessing the Discovery Settings*

From the *Scan Type* dropdown, we change the value from *Port scan (common ports)* to *Custom*.

![](img/ec25e59d75726b7041242a56d3376832_220_0.png)

| Category | Option | Description/Selection |
| :--- | :--- | :--- |
| **Scan Type** | Port scan (common ports) | |
| | Port scan (all ports) | |
| | **Custom** | |
| | Use fast network discovery | |
| **Port Scanner Settings:** | Scan common ports | |
| | Use nstat if credentials are provided | |
| | Use SYN scanner if necessary | |
| **Ping hosts using:** | TCP | |
| | ARP | |
| | ICMP (2 retries) |

![](img/ec25e59d75726b7041242a56d3376832_220_1.png)

This will add additional configurations under *Discovery*. Next, we will click *Discovery* and *Port Scanning* to configure the port range:

![](img/ec25e59d75726b7041242a56d3376832_221_0.png)

*Figure 58: Selecting new Port Scanning Option*

Within the Port Scanning section, we will set the Port scan range to show "0-65535" in order to scan all ports:

![](img/ec25e59d75726b7041242a56d3376832_221_1.png)

*Figure 59: Configuring Scanner to Scan All Ports*

In this scenario, we have chosen a scan definition that will scan all TCP ports but no UDP ports. While this will increase the speed of the scan, we might miss crucial services running on the target. During an engagement, we must weigh the stability of the target network, the scope of the target, the duration of the engagement, and many other factors when configuring our port scan options.

During the configuration of the scan definition, we did not configure any credentials, which implies that this scan will run unauthenticated. Additionally, we accepted the defaults under **Basic Network Scan**, which means brute forcing of user credentials will not be enabled. If we review other options under **Basic Network Scan**, we can verify that the scan will run generic checks against the target in contrast to other templates like **Spectre and Meltdown**, which include specific vulnerability checks. Keep in mind that a scan configured like this will be highly noticeable on the network traffic level as it scans all ports and searches for all applicable vulnerabilities.

Now that we have completely reviewed all the configuration options and understand (at least at a high level) what the scanner is going to do, we can proceed with running our first scan.

### 8.2.4 Unauthenticated Scanning With Nessus

When we are ready to run this first unauthenticated scan, we click the arrow next to Save and then click Launch:

![](img/ec25e59d75726b7041242a56d3376832_222_0.png)

*Figure 60: Launching the Scan*

Initially, the scan will have a status of *Running* (Figure 61).

![](img/ec25e59d75726b7041242a56d3376832_222_1.png)

*Figure 61: Scan Status in Progress*

Once the scan is finished, the status will change to *Completed* (Figure 62).

![](img/ec25e59d75726b7041242a56d3376832_223_0.png)

*Figure 62: Scan Status in Progress*

The scan time will vary based on many factors including the scan configuration and the speed of the network.

From the "My Scans" screen, we can click on the scan name, "Gamma - Basic", to show the list of hosts discovered during the scan and the breakdown of potential vulnerabilities:

![](img/ec25e59d75726b7041242a56d3376832_223_1.png)

*Figure 63: Viewing Scan Overview*

Whether we scan one host or many, we can click on an IP address or hostname to display the vulnerabilities discovered for that target, as shown in Figure 64:

![](img/ec25e59d75726b7041242a56d3376832_224_0.png)

*Figure 64: Viewing Discovered Vulnerabilities*

We can filter these vulnerabilities by severity, exploitability, CVE, and more. To display the vulnerabilities that will most likely lead to target compromise, we can click on `Filter` and change the dropdown on the resultant panel to “Exploit Available”, accepting the defaults of “is equal to” and “true”. Once configured, we click `Apply`.

![](img/ec25e59d75726b7041242a56d3376832_224_1.png)

*Figure 65: Filtering Vulnerabilities with Exploits*

This will display a list of vulnerabilities in groups that are defined by Nessus:

![](img/ec25e59d75726b7041242a56d3376832_225_0.png)

While this grouping can be useful, we will click the gear icon at the top right of the table and click Disable Groups. This will present a preferred output format, listing all vulnerabilities on a single page, sorted by severity:

![](img/ec25e59d75726b7041242a56d3376832_225_1.png)

This output format is perfect for our purposes as it displays a kind of roadmap to potential compromise of the target, with highest-risk vulnerabilities displayed first:

![](img/ec25e59d75726b7041242a56d3376832_226_0.png)

*Figure 68: Grouping Disabled*

Of course, some of the entries may represent false positives, which is why it is critical to review the scan data and manually test the scan results.

#### 8.2.4.2 Exercises

1. Follow the steps above to create your own unauthenticated scan of Gamma.
2. Run the scan with Wireshark open and identify the steps the scanner performed to complete the scan.
3. Review the results of the scan.

### 8.2.5 Authenticated Scanning With Nessus

We can generate more detailed information and reduce false positives by performing an authenticated scan, which requires valid target credentials. To demonstrate the value of an authenticated scan, we will run one against our Debian lab client. Keep in mind however that as penetration testers we would not perform an authenticated scan in most cases without explicit permission and clear communication from the target network administrators due to potentially higher risks of unintentional interruptions to production systems.

To begin, we’ll click the *New Scan* button to start a scan.
