
## NOTE

The rc.firewall script basically adds iptables rules to your DSL system. Because the rc.firewall package also includes the iptables facility itself, you can instead configure your firewall using the iptables command directly or by grabbing other scripts that set up iptables rules. A great place to find such scripts, particularly for more complex firewalls, is the LinuxGuruz site (www.linuxguruz.com/iptables).

## Installing Firewall Software

To use the rc.firewall package in DSL, you must install both the rc.firewall package and gnu-utils package from the MyDSL facility. First, select the MyDSL icon from the desktop. After that, select the following:

- **Firewall Package**—Select UNC→ rc.firewall.unc.info. When the rc.firewall.unc.info page appears, select Download and download the package to the /tmp directory.

- **GNU Utils Package**—Select UNC→ gnu-utils.unc.info. When the gnu-utils.unc.info page appears, select Download and download the package to the /tmp directory.

Both the rc.firewall and gnu-utils packages are installed automatically after the download. Although iptables is immediately enabled, the rc.firewall script is not run at installation and no incoming connections are blocked. The next step is to configure and run the rc.firewall script.

## Configuring the rc.firewall Script

As delivered, the rc.firewall script is configured to block all incoming connections to your computer. It's your job to open access to those ports associated with the services you want to allow outside people to use: namely Web and FTP services.

Because rc.firewall is a shell script, you can edit it using any text editor. I'm going to start by making a copy of rc.firewall to the /opt directory, so you can run it from there. (Also, if you screw up, you can just make a fresh copy of the file.) For example, open a root Terminal window and run this copy command, then use the vi command or the Beaver editor and open the file as follows:

```
# cp /etc/init.d/rc.firewall /opt/
# beaver /opt/rc.firewall
```

There are many ways you can change your firewall configuration in the rc.firewall file. For our purposes, we are only going to open a few ports to allow outside access to the web server (port 80) and the FTP server (port 21).

With the rc.firewall script open, you can open access to the web server and FTP server ports by adding those port numbers to the PERMIT="" line. So, for the easiest case, edit the permit line so it appears as follows:

```
PERMIT="80 21"
```

The preceding PERMIT line opens access to the standard web service port (80) and FTP service port (21). Notice that a space is needed to separate the entries. With this line, all network interfaces allow anyone accessing those interfaces to request Web and FTP service. Of course, if you protected those services with passwords, users also need that username/password information to ultimately view the content associated with those services.

Here are a few different ways that you could configure your PERMIT line to open access to your Web and FTP services:

```
PERMIT="80/tcp 21/tcp"
PERMIT="192.168.0.0/24:80 192.168.0.0/24:21"
PERMIT="192.168.0.0/24 10.0.0.150"
```

You can use the examples in any of the preceding PERMIT lines to allow access to your server. In the first example, tcp is added to each port number, to indicate that only TCP protocols can access those services (by default, both TCP and UDP are allowed). The next example only allows access to ports 80 and 21 from computers on the 192.168.0 network (a good approach if you want to limit access to computers on your LAN). The final example allows access to any available port on the 192.168.0 network, as well as specifically permits access from the host at IP address 10.0.0.50.

There are many, many other ways to configure firewall services in your rc.firewall script. For example, if your web server is also being used as a router between your LAN and the Internet (not a terribly secure arrangement, but one that many people do), the script lets you set up your firewall for that. Assuming you want to allow routing to the Internet (eth0 interface) from computers on your LAN (eth1 interface), the following line would tell your firewall to allow that:

```
INTERNAL_INTERFACES="eth0"
```

A more secure approach to having your servers and the workstations on your LAN exist behind the same Internet connection is to configure what is called a Demilitarized Zone (DMZ). With a DMZ configuration, servers are behind one firewall, whereas your private LAN (generally your user workstations) is behind
