
The next section explains how to download and install the latest version of the Nmap package.

## Installing Nmap

The main source of Nmap distribution is www.insecure.org. You can download both the full sources or the RPM packages from this site. The simplest way to install it is by using the remote source, as follows:

```bash
[ramon]:~$ rpm -vhU http://www.insecure.org/nmap/dist/nmap-2.53-1.i386.rpm
```

Once installed, you’ll use the main Nmap executable, located at `/usr/bin/nmap` by default. The following section describes some common uses of the Nmap tool.

## Using Nmap

Although Nmap is a comprehensive network-auditing tool, its discussion in this book focuses on its ability to identify live hosts, active network services, and remote operating system type because these are the areas where Nmap is most useful.

The simplest use of Nmap is to identify which hosts are *live* (up and available) on the network at any one time. This task is called a *port scan*. Listing 5.5 illustrates an example of using Nmap to perform a port scan on a subnet.

### Listing 5.5 Using Nmap to perform a port scan on an entire subnet

```bash
[ramon]:~$ sudo nmap -sP 192.168.1.0/24

Starting nmap V. 2.53 by fyodor@insecure.org
(http://www.insecure.org/nmap/)
Host plus (192.168.1.5) appears to be up.
Host donald (192.168.1.7) appears to be up.
Host minnie (192.168.1.44) appears to be up.
Host dumbo (192.168.1.67) appears to be up.
Nmap run completed - 256 IP addresses (4 hosts up) scanned in 9 seconds
```

Nmap considers a host to be *up* if it responds to either an ICMP Echo request or to a TCP ACK.

Another popular use of Nmap is to identify which ports (TCP, UDP) are open on a remote host. This is called a *TCP scan*. A port is *open* when there is a listener daemon that responds to network requests to that port on the target system.

Listing 5.6 illustrates an example of using Nmap to perform a TCP scan. In this example, Nmap has found that the target hosts have a total of three HTTP ports open: Secure Shell (TCP service number 22), SMTP Mail (TCP service 25) and Secure HTTP (TCP service 443). Note that by default, Nmap only scans the first 1500 or so TCP ports.

### Listing 5.6 Using Nmap to perform a TCP scan on a single target host

```bash
[ramon]:~$ sudo nmap -sS target.example.com

Starting nmap V. 2.53 by fyodor@insecure.org
(www.insecure.org/nmap/)
Interesting ports on target.example.com (192.168.1.1):
(The 1520 ports scanned but not shown below are in state: filtered)
    Port      State      Service
    22/tcp    open       ssh
    25/tcp    open       smtp
    443/tcp   closed     https
Nmap run completed -- 1 IP address (1 host up) scanned in 178 seconds
```

The third example illustrates Nmap's ability to identify the type of operating system running on a remote host and to examine the particularities of the host's TCP implementation. The Nmap authors call this *TCP fingerprinting*, and their implementation is fairly sophisticated, using a constantly updated file containing fingerprint templates that it compares to the target's TCP responses.

Listing 5.7 shows a sample run of Nmap to identify the operating system for three target hosts: a Lucent Pipeline PL75 router, a Solaris 2.5.1 workstation, and a Linux server. Note that part of the output in Listing 5.7 includes the degree of difficulty (Difficulty), which tells you how hard it is to identify the target operating system over the network. Note that Linux earned the highest degree out of the three targets!

### Listing 5.7 Using Nmap to identify a remote host's operating system

```bash
[ramon]:~$ sudo nmap -O 192.168.1.1 192.168.1.100 192.168.1.200

Starting nmap V. 2.53 by fyodor@insecure.org
(www.insecure.org/nmap/)
Interesting ports on router (192.168.1.1):
(The 1522 ports scanned but not shown below are in state: closed)
    Port      State      Service
    23/tcp    open       telnet
TCP Sequence Prediction: Class=random positive increments
Difficulty=15144 (Worthy challenge)
Remote OS guesses: Ascend P130 Router, Ascend P75
Interesting ports on fantasia (192.168.1.100):
(The 1519 ports scanned but not shown below are in state: closed)
    Port      State      Service
    21/tcp    open       ftp
    22/tcp    open       ssh
    139/tcp   open       netbios-ssn
    6000/tcp  open       X11
TCP Sequence Prediction: Class=random positive increments
Difficulty=23419 (Worthy challenge)
Remote operating system guess: Solaris 2.5, 2.5.1
Interesting ports on penguin (192.168.1.200):
(The 1516 ports scanned but not shown below are in state: closed)
    Port      State      Service
    21/tcp    open       ftp
    22/tcp    open       ssh
    23/tcp    open       telnet
    80/tcp    open       http
    989/tcp   open       ftps-data
    1080/tcp  open       socks
    3001/tcp  open       nessusd
TCP Sequence Prediction: Class=random positive increments
Difficulty=2630920 (Good luck!)
Remote operating system guess: Linux 2.1.122 - 2.2.14
Nmap run completed -- 3 IP addresses (3 hosts up) scanned in 10 seconds
```

As always, the use of Nmap is a double-edged sword. Although this utility should be in every security administrator’s toolkit, always be vigilant and look for evidence of an Nmap scan on your network because that is typically the precursor of an attack. The swatch and logcheck utilities discussed in Chapter 3, “System Monitoring and Auditing,” are well suited for this purpose.

Both Nessus and Nmap identify potential exploits on a target system by contacting it via the network. An alternative class of host-based auditing tools accomplishes the same task, but the tools are executed on the target system itself. The next section in this book explores host-based auditing in more detail and introduces some examples of the host-based approach to network security auditing.

## Host-Based Auditing Tools

While Nessus and Nmap allow you to play the part of the “bad guy” attempting to break into your Linux server from the public network, the majority of successful network attacks are actually staged from the inside. This fact prompted the Unix community to design a tool that could be used on the system itself, to identify vulnerabilities from inside attacks.

In 1993, Dan Farmer, who is also the author of the SATAN network-based audit tool, released a utility called COPS (Computer Oracle and Password System). A pioneer in the field of host-based security auditing, COPS is actually a collection of smaller tools, each of which targets a specific vulnerability in a typical Unix system that can lead to a network attack. These checks extend to areas like the anonymous FTP server, the /etc/rc.* directories, cron entries, and NFS and Sunmail vulnerabilities.

Texas A&M University released a set of host-based auditing scripts (code-named Tiger) as a follow-up to COPS, but stopped developing new features in 1994. Both COPS and Tiger are now hopelessly out of date, but a worthy successor has emerged. The next section describes the Advanced Research Corporation's TARA package.

## TARA

TARA (Tiger Auditors Research Assistant) is a 1999 update of the Tiger system from Texas A&M by a private company (Advanced Research Corporation) working under funding from the National Institutes of Health (NIH). The resulting package was released to the public domain under the auspices of the GNU General Public License (GPL).

As was the case with Tiger, TARA is a set of shell scripts controlled by a central utility, which is still named tiger to honor its direct ancestor. The main goal of this tool is to identify settings on your Linux server that would make it easier for an intruder to gain root privileges over the network. TARA is meant to run both interactively and periodically in batch mode. Either way, the result is a report of the potential vulnerabilities found at the time of its execution.

The next section explains how to download and install the latest versions of the TARA scripts on your Linux server.

### Installing TARA

The TARA distribution can be obtained directly from the ARC Web site at http://www-arc.com/tara/. There is no RPM package available, so you have to download the source archive. Simply decompress and extract the archive as shown in Listing 5.8.

### Listing 5.8 Extracting the TARA archive

```bash
[ramon]:~$ ls -l tara-2.0.9.tar.gz
-rw-r-- 1 ramon users 355267 Nov 18 17:13 tara-2.0.9.tar.gz
[ramon]:~$ gzip -dc tara-2.0.9.tar.gz | tar -xf -
[ramon]:~$ cd tara-2.0.9
[ramon]:~$ sudo mkdir -p /usr/spool/tiger/work
```
