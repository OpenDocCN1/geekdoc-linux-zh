# CHAPTER 13 Testing and Reporting

# The nmap Command

The nmap command is an incredible tool. Several books have been written about this network exploration tool and port scanner. To get a taste of what it can do, run the nmap command by itself. Now run it on the system of your choice, using an IP address or hostname. If a firewall has been configured on a system, it's interesting to note the differences from inside and outside the firewall.

The following sections address some of the options described in the nmap output. Those commands that require administrative privileges are preceded by the standard root prompt, #. Be aware, nmap can take several minutes to run over a network. If you're just learning the nmap command, it may be better to run the commands in the following subsections against an IP address on local network. Of course, if you are testing a system behind a firewall, you can't measure the effectiveness of that firewall unless the nmap command is run on a system on the other side of that firewall.

In general, if you want information in the output, the (-v) switch can help. If you need more information, the -vv switch adds more verbosity. The description in this chapter is far from complete; there are several books written on the intricacies of the nmap command.

# Target Specification

The nmap command can be targeted at a group of systems, an IP address, hostname, or fully qualified domain name formats. For example, the following command reviews the systems with IP addresses 192.168.0.1 through 192.168.0.3:

```
$ nmap 192.168.0.1-3
```

The following command reviews all systems on the noted network, in Classless Domain Routing (CIDR) notation:

```
$ nmap 192.168.0.0/24
```

# Host Discovery

A black-hat hacker with access to a private network might start with a ping scan. In the following command, the -s switch scans and the -P switch applies the ping command to the systems on the target addresses:

```
$ nmap -sP 10.0.0.0/
```

It takes a few seconds to display a list of active systems on that network. One other useful switch from this section is the -n, which avoids the use of DNS servers for name resolution. If there is an excessive delay when running nmap commands, the -n may help.

![](bbox=[0.615, 0.075, 0.905, 0.313])