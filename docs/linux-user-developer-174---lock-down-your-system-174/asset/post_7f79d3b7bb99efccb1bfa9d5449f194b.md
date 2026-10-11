
## Lock down your system
### STAY BEHIND UFW
Protect your ports with a few quick commands

Ufw (Uncomplicated Firewall) and its graphical companion Gufw serve as front-ends for the iptables firewall that is standard in most distributions of Linux.

Run the following command:

```
apt-get install ufw gufw
```

...in Kali to explore further.

Gufw is self-explanatory and comes with a switch to enable the firewall, and wizards to block or allow certain ports. There are even preset configurations to allow certain applications and games such as Call of Duty. The command-line version is almost as easy to use. Run:

```
ufw enable
```

Then to check firewall status, run:

```
ufw status verbose
```

By default, all outgoing connections are enabled and all incoming are disabled. You can enable connections with a single command citing the port and protocol. For example, if running a Minecraft server, allow incoming TCP traffic with:

```
ufw allow 25565/tcp
```

Services such as SSH follow the following syntax:

```
ufw allow ssh
```

To disable ports or services, replace ‘allow’ with ‘deny’.

![](img/1f330653f83dcf0397f7d224ce8bbc16_21_0.png)

Ufw comes pre-installed on Ubuntu and certain other Debian-based distros, but is not ideal for RPM-based ones.

For a true cross-platform solution, consider running a dedicated firewall distro such as IPFire (featured later).

> Sparta will ask you to specify a range of IP addresses to scan. Once the scan is complete, Sparta will identify any machines, as well as any open ports or running services

![](img/1f330653f83dcf0397f7d224ce8bbc16_21_1.png)

## ANALYSE APPS WITH BURP SUITE
Lock down your web applications

Burp Suite is an integrated platform for analysing and attacking web applications. The free version, which comes pre-installed in Kali, is likely to meet most admins' needs.

Burp Suite contains an intercepting proxy, which you run on startup on port 8080. This allows you to scan any browser traffic through it for analysis. Make a request in your web app for the proxy to intercept it. Head over to the Target tab if you wish to view a site map.

From inside the Target tab, find your web application and then right-click one of your nodes. Select the ‘spider from here’ option to make sure there are no links to sensitive resources like databases that hackers might be able to exploit.

Back in the Proxy tab, click the Action button, then Send to Intruder to pass intercepted traffic to Burp Suite Intruder. This allows you to automate an attack against one of your web applications, such as trying to brute-force a user's password.

Click the Intruder tab and then Positions to configure the request template as well as the attack type. The Payloads tab allows you to choose specific payload sets. Click the Start Attack button when ready.

For a complete rundown of all Burp Suite's features, visit the Developer's support site at portswigger.net/burp/help.

## TEST YOUR NETWORK WITH SPARTA
A handy Python GUI for nmap and Nikto – this is Sparta

Sparta, which comes pre-installed in Kali, serves as a front-end for the awesome nmap and Nikto tools among others, making network enumeration much easier.

Upon launch, Sparta will ask you to specify a range of IP addresses to scan. Once the scan is complete, Sparta will identify any machines, as well as any open ports or running services. Where possible, it will also list the OS in the information tab.

If ports 80 or 443 are open, Sparta will also have Nikto run a scan. Nikto essentially checks server software to make sure it's up to date, as well as ensuring that there are no potentially harmful files or programs. Use the Nikto tab to view the results and the Notes tab to record your progress.

Sparta also incorporates the ‘hydra’ tool, which can be used to brute-force remote authentication services such as SSH. Besides specifying the IP, port and service of the remote host, you’ll need to link to a password list. Kali includes the ‘rockyou’ list containing thousands of the most commonly used passwords. If you want to test Sparta safely, consider using the Metasploitable virtual machine (featured later), which intentionally includes vulnerabilities.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_0.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_1.png)

### 01 Add hosts
Launch Sparta in Kali by going to Applications > Vulnerability Analysis > Sparta. When the window launches, select ‘Click here to add host(s)’ to scope. A pop-up will appear asking you to specify an IP range. You can add a single IP address or you already know the host you wish to scan or specify an entire subnet, for example 192.168.1.0/24. Click Add to Scope to begin the scan. If you're checking several hosts, right-click each as you go and select Mark as Checked to omit them from future scans.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_2.png)

### 02 Gather host information
Hosts are listed in the left-hand pane. Click on each to see open ports in the Services tab. The layout is very clear. Numbered ports are listed under Port and the type of service in question such as SSH or FTP is listed under Name. Use the information tab to see the total number of open ports. Sparta also uses OS Fingerprinting to determine the host's operating system, but this is not always accurate. Use the Notes tab at this stage to record any observations you've made so far.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_3.png)

### 03 Check Nikto scan
This step is optional but recommended. Nikto will automatically scan ports 80 or 443 if it finds them open. Click on the Nikto tab to see the results of the scan. The results can be quite convoluted so it pays to break them down by section. The ‘SSL info’ section in the screenshot, for instance, shows that the default HTTPS certificate used in devices running Broadcom firmware is installed. This certificate is installed on over 480,000 devices so needs to be updated. Other alerts such as ‘No CGI Directories found’ are more self-explanatory. Some may be prefixed with OSVDB- followed by a number. These are Open Source Vulnerability Database designations. Search osvdb.org for further information on individual vulnerabilities.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_4.png)

### 04 Select service to brute-force
If you wish to test the strength of passwords on a remote host, click on the Services tab and then right-click on the name of the service you wish to attack, such as SSH. Click ‘Send to Brute’ to specify the IP, port and service you wish to crack. Next, click on the Brute tab and check these are correct.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_5.png)

### 05 Prepare your brute-force attack
Once you have clicked on the Brute tab, examine the default options. These are checked so hydra will look for obvious vulnerabilities such as a blank password or a password that's identical to a username. Below this, you can specify a username and/or password manually or choose from a list. Click the Browse button to view the /usr/share/wordlists folder. Extract rockyou.txt.gz to try some of the most common passwords. Alternatively, use the password list from John the Ripper located in /usr/share/john/password.lst or search this list online.

![](img/1f330653f83dcf0397f7d224ce8bbc16_22_6.png)

### 06 Launch the brute-force attack
Click Run to begin brute-forcing the password of your chosen host. Pay careful attention to the warning message in the pane below; you have not specified a username or password, this will display brute errors.

The Threads option on the top-right limits the number of parallel tasks hydra will try to carry out. If you are connecting via SSH, Sparta will warn you that servers usually support a maximum of four. Click Stop at any time to reconfigure before launching the attack again.

## USE THE METASPLOIT FRAMEWORK
Test your server against thousands of exploits

The free version of Metasploit Framework (often shortened to 'msf') is bundled with Kali Linux. Msf is an open source framework for identifying vulnerabilities as well as developing and running exploit code.

![](img/1f330653f83dcf0397f7d224ce8bbc16_23_0.png)

Kali also comes with the excellent program Armitage, which serves as a GUI for msf. The commercial versions also have a web GUI, but when taking your first tentative steps with the framework, the command-line utility is less overwhelming.

Rapid7, the developer of msf, has also created Metasploitable 2, a virtual machine which intentionally contains a number of vulnerabilities that can be exploited by msf, which you can use for the purposes of this tutorial.

Kali has a built-in command-line tool, nmap, which can be accessed from within msf once a vulnerable port/service has been detected. For a more visually appealing, categorised view, visit Offensive Security's online exploit database: www.exploit-db.com.

The final step is to run the exploit to discover whether your server is vulnerable to this particular attack. Msf will inform you one way or the other and save the results to its database.

Once the exploit has been loaded, you can configure it further with the command show options.

### 01 Launch MetaSploit Framework
Launch msf from within Kali by clicking Applications > Exploitation Tools > Metasploit. As with other security tools, you may find msf in more than one category as it can be used in various ways. If you are using the Metasploitable 2 virtual machine in VirtualBox, which is highly recommended, make sure to create a host-only network to which both the Kali and Metasploitable machine are connected. This will prevent either machine from connecting to the real network or the internet.

![](img/1f330653f83dcf0397f7d224ce8bbc16_23_1.png)

> "Run the exploit to see if your server is vulnerable to this particular attack. Msf will inform you one way or another"

![](img/1f330653f83dcf0397f7d224ce8bbc16_23_2.png)

### 02 Identify remote hosts
This step simply involves identifying the remote host you wish to exploit through the use of nmap. If you wish, you can use nmap's GUI to do this. Alternatively, you can use nmap from the msf command line in the following format:

For instance:

```
nmap -v 192.168.56.102
```

If you wish to scan an entire subnet, use the ** wildcard. For example:

```
nmap -v 192.168.0.*
```

```
nmap -v address
```
