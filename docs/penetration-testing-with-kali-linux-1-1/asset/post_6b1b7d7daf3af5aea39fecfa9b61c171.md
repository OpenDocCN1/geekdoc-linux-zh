
## 23.3.1.1 Exercises

-   1. Set up a PowerShell Empire listener and stager and obtain a working agent.
-   2. Perform enumeration on the domain using various modules.
-   3. Perform a remote desktop login with the account Jeff_Admin to ensure the credentials are cached on the Windows 10 client and then dump the credentials using PowerShell Empire.
-   4. Experiment with the different lateral movement modules.

## 23.4 Wrapping Up

In this module, we covered the basic syntax and functionality of PowerShell Empire, such as listeners, stagers, and agents. We also explored various modules to perform enumeration, obtain credentials, and perform lateral movement. Lastly, we looked at how PowerShell Empire and Metasploit can be used together.

## 24. Assembling the Pieces: Penetration Test Breakdown

Now that we have introduced all the individual pieces of a penetration test, it’s time to put them together. In this module, we will conduct a simulated penetration test inspired by real-world findings.

Although our goal in this exercise is to obtain domain administrator access in the environment, it is important to note that this is not always the end goal of a penetration test. Our goal should be determined by the client’s data infrastructure and business model. For example, if the client’s main business is warehousing data, our goal would be to obtain those data. That is because a breach of this nature would cause the most significant impact to the client. In most cases, domain administrator access would help us accomplish that goal, but that is not always the case.

During this penetration test, we will be going back and forth between enumeration and exploitation. We will spend some time on the enumeration phase to ensure that the methodology we are using for exploitation is good. We will also review some mistakes that are easily made and discuss why obtaining root/admin on a target is not always necessary.

Our fictitious client has provided us an initial target named “sandbox.local” and has mentioned that a compromised domain administrator account would have the greatest impact on their business. The sandbox network is accessible via the lab VPN and has the network layout found in Figure 317.

![](img/ec25e59d75726b7041242a56d3376832_738_0.png)

> This domain is accessible via the PWK VPN but requires us to add an entry to our `/etc/hosts` file. First, we’ll make a backup of the existing file by copying `/etc/hosts` to `hosts.orig` in our home directory. Now we’ll append an entry that will allow us to contact the domain via its DNS name by running `sudo bash -c " echo '10.11.1.250 sandbox.local' >> /etc/hosts"`. With that set, we can continue.

### 24.1 Public Network Enumeration

We will begin by conducting a scan of the external host resolvable through the DNS name sandbox.local. To do this, we will use Nmap with the following command:

```bash
kali@kali:~$ sudo nmap -sC -sS -p0-65535 sandbox.local
```

Listing 855 - Nmap command for initial discovery

The command in Listing 855 will use Nmap’s default set of scripts (`-sC`), use a SYN scan for faster run time (`-sS`), scan all ports (`-p0-65535`), and only target the sandbox.local network.

The Nmap scan results can be found in Listing 856.

```
Nmap scan report for sandbox.local (10.11.1.250) 
Host is up (0.00060s latency). 
Not shown: 65534 filtered ports
PORT STATE SERVICE
22/tcp open ssh 
| ssh-hostkey:
| 2048 86:8f:89:36:79:2f:44:b2:61:18:a4:fb:d5:a1:f3:43 (RSA)
| 256 de:f3:84:f1:cd:f3:c8:9a:30:6d:60:e8:b1:1d:99:27 (ECDSA)
|_ 256 14:6a:ba:77:e0:57:e5:0c:c0:cc:76:31:91:8d:dd:9f (ED25519)
80/tcp open http 
|_http-generator: WordPress 5.3
|_http-title: SandBox &#8211; See the future, Feel the shine
MAC Address: 00:50:56:8A:C8:51 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 111.66 seconds
```

Listing 856 - Nmap scan from initial discovery

Let’s review the results of this scan. First, the Nmap scan revealed only two open ports: 22 and 80. Nmap fingerprinted the services as running a SSH service and HTTP service on the ports respectively. The Nmap default set of plugins also revealed the ssh-hostkeys.

The HTTP service is showing us that the running application might be WordPress 5.3. The risk exposed by the SSH service is typically a lot less than the one exposed by an HTTP service. Therefore, the HTTP service seems to be a better starting point to compromise the sandbox.local environment.

### 24.2 Targeting the Web Application

The first step we take is simply visiting the web application home page.

![](img/ec25e59d75726b7041242a56d3376832_740_0.png)

Figure 318: Visiting the Sandbox.local Webpage

The home page seems to be a fairly standard landing page for a company. The links in the navigation bar all point to anchors on the home page and there is a survey asking for feedback on the bottom left. There appears to be no other field for user-controlled input.

The Nmap scan indicated that the web page is running on WordPress 5.3, but to confirm that, further enumeration is required.

While the WordPress core itself has had its share of vulnerabilities, the WordPress developers are quick to patch them. However, themes and plugins are written by the community and many vulnerabilities are improperly patched or are simply never fixed at all.

This makes WordPress a great target for compromise.

#### 24.2.1 Web Application Enumeration

Before we begin targeting WordPress specifically, let's do a basic directory brute force to discover any potential sensitive files and to confirm that the site is running WordPress. For this, we will use dirb as follows.

```bash
kali@kali:~$ dirb http://sandbox.local
```

Listing 857 - dirb scan of sandbox.local

While **dirb** has many flags and features that we could use, we are choosing to run a simple test. The output of our command can be found in Listing 858.

```
---  Scanning URL: http://sandbox.local/ ---
+ http://sandbox.local/index.php (CODE:301|SIZE:0)
+ http://sandbox.local/server-status (CODE:403|SIZE:278)
=>  DIRECTORY: http://sandbox.local/wp-admin/
=>  DIRECTORY: http://sandbox.local/wp-content/
=>  DIRECTORY: http://sandbox.local/wp-includes/
+ http://sandbox.local/xmlrpc.php (CODE:405|SIZE:42)

--- Entering directory: http://sandbox.local/wp-admin/ ---
+ http://sandbox.local/wp-admin/admin.php (CODE:302|SIZE:0)
=>  DIRECTORY: http://sandbox.local/wp-admin/css/
=>  DIRECTORY: http://sandbox.local/wp-admin/images/
=>  DIRECTORY: http://sandbox.local/wp-admin/includes/
+ http://sandbox.local/wp-admin/index.php (CODE:302|SIZE:0)
=>  DIRECTORY: http://sandbox.local/wp-admin/js/
=>  DIRECTORY: http://sandbox.local/wp-admin/lang/
=>  DIRECTORY: http://sandbox.local/wp-admin/network/
=>  DIRECTORY: http://sandbox.local/wp-admin/user/

--- Entering directory: http://sandbox.local/wp-content/ ---
+ http://sandbox.local/wp-content/index.php (CODE:200|SIZE:0)
=>  DIRECTORY: http://sandbox.local/wp-content/plugins/
=>  DIRECTORY: http://sandbox.local/wp-content/themes/
=>  DIRECTORY: http://sandbox.local/wp-content/upgrade/
=>  DIRECTORY: http://sandbox.local/wp-content/uploads/

--- Entering directory: http://sandbox.local/wp-includes/ ---
(!) WARNING: Directory IS LISTABLE. No need to scan it.
(Use mode '-w' if you want to scan it anyway)

--- Entering directory: http://sandbox.local/wp-admin/css/ ---
(!) WARNING: Directory IS LISTABLE. No need to scan it.
(Use mode '-w' if you want to scan it anyway)
-----
END_TIME: Mon Dec  9 13:00:40 2019
DOWNLOADED: 32284 - FOUND: 12
```

Listing 858 - Output of dirb scan

Our scan revealed common WordPress directories on our target (**wp-admin**, **wp-content**, and **wp-includes**). We also found some directories that are listable; however, these are common WordPress directories and likely won't reveal much.

Let's move on to a more specific scan with WPScan, a WordPress vulnerability scanner that uses a database of known vulnerabilities to discover security issues with WordPress instances.

For a thorough scan, we will need to provide the URL of the target (**-url**) and configure the **enumerate** option to include "All Plugins" (**ap**), "All Themes" (**at**), "Config backups" (**cb**), and 'Db exports' (**dbe**). The final command can be found in Listing 859 below.

```
kali@kali:~$ wpscan --url sandbox.local --enumerate ap,at,cb,dbe
```
