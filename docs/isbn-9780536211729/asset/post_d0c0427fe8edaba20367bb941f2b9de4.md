
software that’s both widely deployed and mature. Snort works using the concept of intrusion signatures. The theory is that many attacks follow the same pattern or look the same or very similar at the network level.

Consider this example: Assume that a packet is received on a certain port with its header flags set a certain way. When this occurs, it is always a precursor to an attack or an attempt to exploit a certain vulnerability. It can be said that this particular attack has, therefore, a signature that identifies it as malicious traffic. This signature, unique to the exploit of this vulnerability, can then be used by software such as Snort to detect that there was an attempt to exploit the vulnerability. Snort can then perform an action based on this detection (or can take no action).

Snort is quite powerful and, when combined with reporting software called ACID, can produce complex reports in addition to the main function of intrusion detection.

Ntop is network analysis software, as opposed to the sniffer that produces reports of usage based on protocol, flow, host, and other parameters. Using ntop is recommended at strategic points in the network to establish a baseline of the normal traffic flows on the network. A sample page with one of ntop’s reports is shown in Figure 10.1.

![](img/7d04225c75a86d3cf4bd6077596f35b2_437_0.png)

Figure 10.1 An example of one of ntop’s reports.

Ntop is just one such analyzer. I chose to feature ntop here because it’s simple to get working quickly. However, I also recommend other analysis software for network traffic. Among other analysis software, MRTG and Cricket are two excellent choices for traffic analysis.

Creating baseline traffic reports and keeping them up-to-date helps not only to spot anomalies including both unexpected increases and decreases in the traffic but also to track when new bandwidth might be necessary. It is this dual use—security anomalies and bandwidth usage monitoring—that makes traffic analysis invaluable.

To establish traffic baselines and effectively monitor the network for intrusions using Snort and TCPDump on large networks, it’s important to place the tools at strategic locations within the network. Most large networks (even medium and small) use switches to pass traffic. Understanding the difference between switches and hubs is important when considering where to place network tools.

### 10.1.1 Switches and Hubs and Why You Care

On a switched network, any given network interface would receive only traffic destined for it as well as broadcast traffic. In a hub network environment the network interface receives all traffic, whether that traffic is destined for it or for another device. This is why switched networks are faster than hubbed networks—the unnecessary traffic isn’t sent to all ports of the switch.

There are situations in which a network interface might receive all traffic or a greater subset than merely its own in a switched network, such as those when a switch is configured to mirror the traffic to a specific port. In practice this can be done, but it may result in performance problems for the switch because it now has to copy all traffic to two ports instead of one. Refer to your switch’s documentation for more information. For example, Cisco Catalyst switches call this feature “Switched Port Analyzer,” or SPAN. More information on SPAN can be found at http://www.cisco.com/warp/public/473/41.html.

Regardless of where the traffic originates, if it comes into the interface where the sniffer is running, the traffic can be captured. The key, at a network level, is to place sniffer and the related intrusion detection software in the right locations. For host-based traffic sniffing, the placement of the sniffer is obvious, on the host itself.

### 10.1.2 Sniffer Placement

The placement of network sniffers and traffic-analysis software is key to successfully analyzing the traffic. In a switched network, the switch needs to be configured to mirror all traffic out the sniffer’s switch port. Chapter 11 discusses the placement of sniffers. In essence, I recommend placing them in as many points as you can, notably near termination points such as firewalls.

### 10.1.3 ARPWatch

Another item to be discussed in Chapter 11 is ARPWatch. ARPWatch is software to watch for new network devices on the network. ARPWatch can be helpful for auditing the devices on the network, especially wireless networks.

## 10.2 Rootkit Checkers

A rootkit is a piece of software or a grouping of software that attempts to exploit one or more vulnerabilities with the goal of enabling an attacker to gain elevated privileges or perform any other type of attack against the target. Frequently, rootkits are used by less skilled attackers who use the software built by another attacker but don't really understand the underlying exploit; they're just interested in the results.

Many rootkits not only run the initial exploit to give the attacker root privileges but also attempt to mask or hide the fact that an attack has been launched. They do this by deleting log files or certain entries from log files, planting trojan-horse versions of programs, and employing other means. There is also nothing stopping an attacker from chaining rootkits together for multiple levels of deception and possible exploit.

Like network-centric attacks, rootkits frequently have signatures or leave other traces that identify them. These traces and signatures might be the aforementioned removal of log files, the presence of one or more processes, or other changes to the system that are specific to the rootkit software or the exploit.

Also as with network-centric attacks, there is software to search for the signatures and traces of rootkits as well. One such application is Chkrootkit.

### 10.2.1 Running Chkrootkit

Before you can run Chkrootkit, you need to get it. Chkrootkit can be downloaded from http://www.chkrootkit.org/. After it's downloaded, Chkrootkit needs to be unpacked and compiled:

```
tar -zxvf chkrootkit.tar.gz
cd chkrootkit-<NNNN>
make sense
```

Yes, that does say `make sense` in the code example. Although Chkrootkit is a shell script, there is some additional functionality gained by compiling the code. Compiling is not required, but because it's quick and adds some additional levels of checking, I'd recommend doing so. Specifically, compiling Chkrootkit will enable these additional checks:

- ifpromisc
- chklastlog
- chkwtmp
- check_wtmpx
- chkproc
- chkdirs
- strings

Of all the tools used in this book, Chkrootkit is probably the easiest to use. To run Chkrootkit, from within the `chkrootkit` source directory you simply type this:

```
./chkrootkit | less
```

You aren’t required to pipe the output to less but there is a copious amount of output. So if you actually want to read the output, you’ll probably need to pipe it somewhere—unless, of course, you have a huge scrollback buffer.

Because running Chkrootkit produces a lot of output, it is wise to pipe the output to more or less, depending on your preference. Alternatively, you could redirect the output to a file:

```
./chkrootkit > output.txt
```

Chkrootkit will output a number of lines informing you what it is currently checking for along with the ultimate status of the check. The output will look similar to this:

```
Checking `amd`... not found
Checking `basename`... not infected
Checking `biff`... not infected
Checking `chfn`... not infected
Checking `chsh`... not infected
Searching for ShitC Worm... nothing found
Searching for Ome ga Worm... nothing found
Searching for Sadmin/IIIS Worm... nothing found
Searching for MonKit... nothing found
Searching for Showtee... nothing found
```

As you can see from the output sample, it doesn’t appear that any trojaned files or rootkits were detected. An infected file or detection of a rootkit will look similar to the following:

```
Checking `bindshell`... INFECTED (PORTS: 1524 31337)
```

Even though the output from Chkrootkit seems to indicate that the computer is infected with bindshell, Chkrootkit does sometimes produce false positives. However, if you see the INFECTED output from Chkrootkit, it’s in your best interest to assume that Chkrootkit reported correctly and take steps to mitigate the damage.

A false positive occurs when a tool detects and reports a problem when in fact there is no problem. The underlying cause for false positives varies depending on the nature of the software reporting the occurrence. False positives are not as bad as false negatives. A false negative occurs when there really is a problem but the problem is not reported by tools that should find the problem.
