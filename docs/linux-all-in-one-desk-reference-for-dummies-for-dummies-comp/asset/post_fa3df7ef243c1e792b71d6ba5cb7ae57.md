
If you want to try out `nmap` to scan your local area network, just type a command similar to the following (replace the IP address range with addresses appropriate for your network):

```
nmap -O -sS 192.168.0.4-8
```

Here’s a typical output listing from that command:

```
Starting nmap 3.81 ( http://www.insecure.org/nmap/ ) at 2005-08-28 16:20 EDT
Interesting ports on 192.168.0.4:
(The 1659 ports scanned but not shown below are in state: closed)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
111/tcp open rpcbind
631/tcp open ipp
MAC Address: 00:C0:49:63:78:3A (U.S. Robotics)
Device type: general purpose
Running: Linux 2.4.X|2.5.X|2.6.X
OS details: Linux 2.4.18 - 2.6.7
Uptime 9.919 days (since Thu Aug 18 18:18:15 2005)
... Lines deleted ...
Nmap finished: 5 IP addresses (5 hosts up) scanned in 30.846 seconds
```

As you can see, `nmap` displays the names of the open ports and hazards a guess at the operating system name and version number.

## Nessus

The Nessus Security Scanner is a modular security auditing tool that uses plugins written in the Nessus scripting language to test for a wide variety of network vulnerabilities. Nessus uses a client/server software architecture with a server called nessusd and a client called nessus.

Knoppix already comes with Nessus, so you don’t have to download or install anything. To start Nessus, choose Main Menu→System→Security→NESSUS Security Tool.

To install Nessus, first try your Linux distribution’s usual method for installing new software packages. In Debian, MEPIS, and Ubuntu, type `apt-get install nessus` to install the packages. In SUSE, click Install and Remove Software from the Software category in YaST Control Center — Main Menu→System→Control Center (YaST) — and use YaST’s search facility to find the nessus packages. Select the packages and click Accept to install them. In Xandros, choose Edit→Set Application Sources and click the Debian Unsupported Site link as a source. Then type `apt-get install nessus` nessusd.

![](img/11709a8f88c8cd03868a929dc94c0e2b_584_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_584_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_585_0.png)

For Fedora Core, you have to download Nessus from www.nessus.org/download/ and install it. Before you try to install Nessus, you must install the sharutils RPM. That package includes the uudecode utility that the Nessus installation script needs. The sharutils package isn't installed with any of the standard package groups in Fedora Core, so you have to install it yourself. To install sharutils, mount the companion DVD and install it with the following commands:

```
cd /media/cdrom/Fedora/RPMS
rpm -ivh sharutils*.rpm
```

To download and install Nessus, follow these steps. (These instructions work on all Linux distributions.)

1. At www.nessus.org/download, select the version of Nessus you want to download. For Linux systems, download the Nessus 2.2.5 installer.
2. Type the following command to install Nessus. (You must have the development tools, including The GIMP Toolkit, installed.)

   ```
   sh nessus-installer-2.2.5.sh
   ```

   Respond to the prompts from the installer script to finish the installation. You can usually press Enter to accept the default choices.

After the installation completes, follow these steps to use Nessus. (In Knoppix, choose Main Menu→System→Security→NESSUS Security Tool, and then go to Step 8.)

3. Log in as root and type the following command to create the Nessus SSL certificate used for secure communication between the Nessus client and the Nessus server:

   ```
   nessus-mkcert
   ```

4. Provide the requested information to complete the certificate generation process.
5. Create a nessusd account with the following command:

   ```
   nessusd-adduser
   ```

6. When prompted, enter your username, password, and any rules. (Press Ctrl+D if you don't know what rules to enter.) Then press the Y key.
7. If you want to, you can configure nessusd by editing the configuration file `/usr/local/etc/nessus/nessusd.conf`.

   If you want to try out Nessus, you can proceed with the default configuration file.
8. Start the Nessus server with this command:

   ```
   nessusd -D
   ```

9. Run the Nessus client by typing the following command in a terminal window:

   ```
   nessus
   ```

   The Nessus Setup window appears.
10. Type a nessusd username and password and click the Log In button.
11. When Nessus displays the certificate used to establish the secure connection and asks if you accept it, click Yes.

    After the client connects to the server, the Log In button changes to Log Out, and a Connected label appears at its left.

    nessusd gives you an option to enable plugins that can scan for specific vulnerabilities, but some of these may crash hosts and disrupt your network during the scan. If you want to try any of the plugins, select and enable them. If you want to be safe, click the Enable All but Dangerous Plugins link.
12. Click the Target Selection tab and enter a range of IP addresses to scan all hosts in a network.

    For example, to scan the first eight hosts in a private network 192.168.0.0/24, enter the address as:

    ```
    192.168.0.0/29
    ```

    Don't use Nessus to scan any network that you do not own. Scanning other networks is usually against the law, and there could be serious consequences if you break the applicable laws.
13. Click Start the Scan.

    Nessus starts scanning the IP addresses and checks for many different vulnerabilities. Progress bars show the status of the scan.

    After Nessus completes the vulnerability scan of the hosts, it displays the result in a nice combination of graphical and text formats. The report is interactive — you can select a host address to view the report on that host, and you can drill down on a specific vulnerability to find details, such as the CVE number that identifies the vulnerability and a description of the vulnerability.

# Book VII

# Internet Servers

The 5th Wave By Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_588_0.png)

> I'll be right there. Let me just take care of this user. He's about halfway through a 3 hour download.

# Contents at a Glance

1. Chapter 1: Managing Internet Services...565
2. Chapter 2: Running a Web Server ...583
3. Chapter 3: Setting Up the FTP Server ...607
4. Chapter 4: Managing Mail and News Servers ...613
5. Chapter 5: Managing DNS ...639
6. Chapter 6: Using Samba and DNS...661

## Chapter 1: Managing Internet Services

### In This Chapter

- Understanding Internet services
- Controlling servers through inetd or xinetd
- Using chkconfig or update-rc.d to manage servers
- Using GUI utilities to configure services to start at boot time

The Internet is a world of clients and servers. Clients make requests to servers, and servers respond to the requests. For example, your Web browser is a client that downloads information from Web servers and displays it to you. Of course, the clients and servers are computer programs that run on a wide variety of computers. A Linux system is an ideal system to run a wide variety of servers — from a Web server to a Windows file and print server. In this chapter, I provide an overview of a typical Internet service, its client/server architecture, and how to manage the servers in Linux. You can use the information in this chapter to manage any server running on your Linux system.

### Understanding Internet Services

Internet services are network applications designed to deliver information from one system to another. By design, each Internet service is implemented in two parts — a server that provides information and one or more clients that request information.

Such a client/server architecture is the most common way to build distributed information systems. The clients and servers are computer programs that run on these computers and communicate through the network. The neat part is that you can run a client at your desktop computer and access information from a server running on a computer anywhere in the world (as long as it’s on the Internet).
