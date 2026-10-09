
Under the Security Level: drop-down list, the options are High, Medium, and No firewall:

- The **High** setting configures the firewall to reject all incoming TCP connections (by blocking TCP packets that have the SYN flag set, and ACK cleared), and reject all incoming UDP packets, with the exception of replies to DNS queries on port 53 that come from the name servers we told Red Hat Linux about when we configured the network settings. (If the DNS replies were blocked, then we would be unable to resolve any host names that aren't defined in the local /etc/hosts file, which would make using the Internet very tedious.)

> Note that, since incoming connections are blocked, we can't run a Web server or any other kind of server behind such a firewall.

- The **Medium** setting configures the firewall to reject all incoming TCP connections to ports in the range 0 to 1023, and also incoming UDP packets for these port numbers. NFS and X11 traffic are also blocked. The significance of the ports in the range 0 to 1023 is that these are "privileged" ports, and a program has to be running with root authority in order to open sockets on them. However, this does not mean that ports with numbers 1024 to 65536 can only have unprivileged programs opening sockets on them. It is quite possible to set up a Web server running with root authority listening on, say, port 8080.

- If we select **No firewall** as the security level, then the firewall is disabled.

If we find that the default firewall rules do not meet our requirements, then we can select the **Customize** radio button. This enables the remaining options on the window:

![](img/b852150740856958b10aff9e8c9d2adc_547_0.png)

If we check the box against a network interface in the **Trusted devices** section, this configures the firewall to allow all traffic to and from that interface (because we trust all the machines connecting via that interface). However, can we be sure that one of these machines has not been compromised and that the packets coming from it are the work of a hacker?

The other options on the dialogue enable us to allow incoming connections on a selection of well-known ports for different services. For example, let’s pretend that our example machine will be running a Web server, and we’ll need remote access via ssh for administration, so the WWW and SSH boxes need to be checked. This ends up looking like this:

![](img/b852150740856958b10aff9e8c9d2adc_548_0.png)

When we press the OK button, the firewall configuration is updated and saved so that the machine will reboot with the new configuration in place.

## Lokkit

There is another tool that we can use to configure the firewall on our Red Hat Linux systems. It’s called Lokkit (installed from the gnome-lokit RPM). It is a simple to use configuration tool that asks a series of simple questions and configures the firewall according to the answers you supply. It’s not as versatile or powerful as the method we’ve just discussed, so we’ll make no more mention of it here.

> Note that Lokkit is not meant for custom firewall configuration and has fewer options than the Red Hat redhat-config-securitylevel tool.

There is one significant drawback with using the Security Level Configuration or Lokkit applications to configure our packet filtering firewall; both configure only rules that selectively block incoming network traffic. Outgoing traffic and traffic that is forwarded (that is received on one network interface and sent out on another) by our Red Hat system are not checked in any way. This means that, should you have a system behind your firewall that has been compromised (hacked or maybe infected by a virus), it is free to transmit whatever it likes through your firewall. It is a good idea to configure your firewall to block selected outgoing and forwarded traffic too. For example, you may want to force all Internet access for machines behind the firewall to be handled by secure proxy servers. This can be done by blocking outgoing Internet access for all machines except the proxy servers. More detailed firewall configuration like this is done with the `iptables` command, so let's look at how to do that.

### iptables

> This section is a brief introduction to setting up customized security beyond what is possible with the GUI tools provided by Red Hat. It's not meant to be comprehensive, as everyone's needs are different, and it'd be impossible to cater to them all. However, hopefully it'll give you a taste of the tools available.

Blocking and allowing traffic based on direction (i.e. incoming or outgoing) and port number gives some degree of control over network traffic, but there are situations when we need finer control. For example, we may want to run a Web server that can be accessed only from machines within our department, and not from machines elsewhere. Or we may want to prevent users on certain machines from being able to FTP files from our machine while allowing others to do so. The firewalling code in Red Hat Linux 9 is perfectly able to cope with these situations, and far more complex ones, but we have to roll up our sleeves and configure it from the command line.

This is where the `iptables` command comes in. It is used to manipulate the kernel's packet filtering tables, so we can fine tune the firewall settings to our environment. Let's see how to implement a concrete example.

Imagine our Red Hat machine has two network interfaces: `eth0` has the IP address `192.168.1.1` and `eth1` has the IP address `192.168.10.1`. Both interfaces have netmasks of `255.255.255.0`. We're running a Web server listening on port `80`, and an FTP server that uses ports `20` and `21`. We need to allow machines with IP addresses starting with `192.168.10` access to the Web server, but nobody else. We also need to allow all machines in the `192.168.1.0` network access to the FTP server, except `192.168.1.57`. How do we configure this?

The first thing to do is look at the existing firewall configuration. Log on to the machine and switch to the root user. Run the following command to get a verbose listing of the current firewall rules:

```
# iptables -L -v
```

## Security

Rules are grouped together into **chains**. There are three default chains:

- INPUT, which handles incoming network packets destined for processes on the local machine
- OUTPUT, which handles outgoing network packets produced by the local machine
- FORWARD, which handles packets that arrive on one interface and leave on another (i.e. the local machine is forwarding them).

There may be other user defined chains too.

To set up our machine to meet the above specification, we'll clear out (or **flush**) the existing rules with the following command:

```
# iptables -F
```

*We can use this command to delete the named user-defined chain:*

```
# iptables -X name
```

We're going to be dealing only with packets coming into our machine in this example, so we'll be configuring rules in the INPUT chain. Our first step is to configure the default behaviors -- or Policy -- for the INPUT chain so that if it receives a packet that doesn't match any rules, it drops (discards) it. This is the most security conscious approach, as it means that everything is blocked unless we explicitly allow it. The command to set the policy on the INPUT chain to DROP is:

```
# iptables -P INPUT DROP
```

As soon as we type that in, all incoming network packets are dropped, so before we do so, we'd better make sure that we're logged in to the machine on the console. If not, then we'll lose our connection to the machine and won't be able to get it back!

> *We could also have used REJECT instead of DROP as the policy. This would result in a message being sent back to the sender of a blocked packet informing them that the port is not reachable. This is polite, and could prevent a hapless user from continually retrying a connection attempt that will never work. However, it also confirms our presence to a would-be hacker. The policy of DROP silently discards the incoming packet, so our would-be hacker won't even know there's anything listening at our IP address. Of course, this is only valid if we never respond to any requests -- once you've responded to one, you've given the game away.*
