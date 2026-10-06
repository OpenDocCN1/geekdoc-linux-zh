
# Part IV: Fedora and RHEL Network and Server Setup

- **Save on telephone lines** — Instead of a telephone line for each person who wants to get to the Internet, you can use one line to your ISP (In the case of DSL, the telephone company will even let you use the same telephone line for both analog voice and high-speed digital data).

- **Central maintenance** — If information related to your Internet connection changes (such as your dial-out number or server addresses), you can administer those changes in one location instead of having to change it every computer.

- **Central security** — You can better control the Internet traffic that comes in and goes out of your network.

The procedures in this section assume you have already set up a LAN, as described in Chapter 15. It is also assumed that you have an outgoing connection from your Linux system to the Internet that all traffic between the computers on your LAN and the Internet can pass through. That outgoing connection may be dial-up or may come through another LAN card connected (a DSL router) or other LAN. This section describes two ways to set up your Linux system so that the LAN can access the Internet:

- **As a router** — By configuring Linux as a router, it can route IP packets from clients on the LAN to the Internet through the dial-up connection.

- **As a proxy server** — You can configure Linux as a proxy server. In this way, client computers on your LAN can access the Internet although the connection were coming from the Linux computer.

## Setting Up Linux as a Router

There are several different ways to set up routing from your LAN to the Internet. You can have a dedicated router or you can have a computer already connected to your LAN that will act as a router. This section describes how to use your Linux system as a router.

A computer may have several network interfaces, such as a loopback, a direct line to another computer, or a dial-up interface. For a client computer to use a router to reach the Internet, it may have a private IP address assigned to it on the LAN. A connection to a routing computer would act as the gateway to all other addresses.

Here’s an example of Linux being used as a router between a LAN and the Internet:

- The Linux system has at least two network interfaces: one for the LAN and one for the Internet. The interface to the Internet may be a dial-up PPP connection or, more these days, a higher-speed DSL or cable modem connection.

- Packets on the LAN that are not addressed to a known computer on the LAN are forwarded to the router (that is, the Linux system acting as a router). So, each client identifies Linux system as the gateway system.

- The Linux router/firewall is set up to receive packets from the local LAN, then forwards those packets to its other interface (possibly a PPP connection to the Internet). If the LAN uses private IP addresses, the firewall is also configured to use IP masquerading Network Address Translation.

The following sections describe how to set up the Linux router, as well as the client computers from your LAN (Linux and MS Windows clients) that will use this router. Using Linux as a router also provides an excellent opportunity to improve the security of your Internet connection by setting up a firewall to filter traffic and hide the identity of the computers on your LAN (IP masquerading).

## Configuring the Linux router

To configure your Linux computer as a router, you need to have a few things in place. Here's what you need to do before you set up:

- Connect to your LAN. Add a network card and configure the computers on your LAN (as described in Chapter 15).
- Connect to the Internet. Set up a dial-up or other type of connection from your Linux computer to your ISP. This is described earlier in this chapter in the section on setting up outgoing PPP connections.
- Configure your Linux computer as a router. See the rest of this section.

## Selecting IP addresses

The type of IP addresses you are using on your LAN will have an impact on a couple of steps in this procedure. Here are the differences:

- **Private IP addresses** — If the computers on your LAN use private IP addresses (described in Chapter 15), you need to set up Linux as a firewall to do IP masquerading or NAT (as described in Chapter 14). Because those numbers are private, they must be hidden from the Internet when the router forwards their requests. Packets forwarded with masquerading or NAT look to the outside world as though they came from the Linux computer forwarding the packets.
- **Valid IP addresses** — If your LAN uses addresses that were officially assigned by your ISP or other registration authority, you don't need to do IP masquerading or NAT. (Actually, for any machine you want to expose to the world, such as a public server, you will want to have a valid, public IP address.)

In most cases you are not configuring the computers on your LAN as servers, you will probably want to use private IP addresses.

## Configuring forwarding and masquerading

With your Linux computer's LAN and Internet interfaces in place, use the following procedure to set up Linux as a router. After this procedure is completed, any client computer on your LAN can identify your Linux computer as its gateway so it can use Linux to get to the Internet.

1. Open the /etc/sysconfig/network file in a text editor as the root user. Then add either a default gateway or default gateway device as described below.

Your default gateway is where traffic destined for networks outside of your own is sent. This is where you would identify your Internet connection. Here is how you choose which to enter:

- **Default Gateway** — If there is a static IP address you use to reach the Internet, enter that IP address here. For example, if your Internet connection goes through a DSL modem connected to your NIC card at address 192.168.0.1, enter that address as follows:

```
GATEWAY=192.168.0.1
```

- **Default Gateway Device** — If you reach the Internet using a dynamic address that is assigned when you connect to a particular interface, that interface here. For example, if you have a dial-up interface to the first device, you would enter ppp0 as the default gateway device as follows:

```
GATEWAY=ppp0
```

2. Turn on IP forwarding. One way to do this is to change the value of net4.ip_forward in /etc/sysctl.conf. Open that file and change the line to appear:

```
net4.ip_forward = 1
```

NOTE: You can restart your network for this change to take effect. To have the change take place without a network restart, type echo 1 > /proc/sys/net4/ip_forward.

3. If your computers have valid IP addresses, skip ahead to the “Configuring network clients” section. If your computers have private addresses, continue with this procedure.

4. To get IP masquerading going on your router, you need to define which addresses will be masqueraded, using iptables.
The following examples show that you are masquerading all computers on your private LAN 10.0.0.0/24. 
Type the following rules:

```bash
iptables -t nat -A POSTROUTING -o ppp0 -j MASQUERADE
iptables -A FORWARD -s 10.0.0.0/24 -j ACCEPT
iptables -A FORWARD -d 10.0.0.0/24 -j ACCEPT
```

The previous lines add to your running iptables firewall in the Linux kernel. To make the current rules permanent, save them as:

```bash
iptables-save > /etc/sysconfig/iptables
```
This copies all the current rules to the /etc/sysconfig/iptables file, from which the rules are read each time you reboot your system. If the new rules don't work, just copy the iptables.save file back to the original iptables file.

5. At this point, you may want to restart your network as follows:

```bash
/etc/init.d/network restart
```

6. To, restart your firewall, type the following:

```bash
/etc/init.d/iptables restart
```

7. To see if your new rules have gone into effect, type iptables -L. To view NAT rules, type iptables -L t nat.

## Configuring network clients

In this example, there are a variety of Linux and Windows system clients on a LAN. One Linux computer has a connection to the Internet and is set up as act a router between
