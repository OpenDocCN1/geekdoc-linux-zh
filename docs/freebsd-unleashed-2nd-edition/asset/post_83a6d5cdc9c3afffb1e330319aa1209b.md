
:memoryuse=16m:
:tc=default:

Then, use `cap_mkdb /etc/login.conf` to enable this new class and enforce these limits on any user in it.

## Defending Against Springboard Attacks

A *springboard attack* leverages the resources of your own network to achieve its ends. Whereas brute-force and forking attacks require a high-powered attacker doing a lot of work, an attacker can launch a springboard attack simply by injecting a carefully constructed set of requests into the network. Those requests make the network’s own infrastructure its own worst enemy.

An attacker can launch a broadcast ping (or *Smurf*) attack, for example, by sending normal ping requests to your network’s broadcast address (which multiplexes the requests out to all hosts on the network). The hacker spoofs the requests’ source address so it appears to be a different host. Typically, that host is a hapless victim who suffers a lot more than you do in this type of attack, because every host in your network turns around and floods the victim with ping responses. The multiplication effect of this kind of attack can be disastrous for the victim, and the source is very difficult (if not impossible) to trace.

> NOTE
> Another kind of springboard attack injects a UDP packet between two servers’ `echo` service ports. This packet causes the servers to enter into an “echo war” that can be stopped only by shutting off the `echo` port (FreeBSD shuts off the `echo` port by default).

Springboard attacks are best prevented at the network’s edge router; Smurf attacks can be prevented by configuring your router not to respond to broadcast ping requests. If your router is a FreeBSD machine (see Chapter 27 for information on using FreeBSD as a router), the `icmp_bcastecho="NO"` setting in `/etc/defaults/rc.conf` prevents it from responding to these kinds of requests, which are almost never used for any good purpose.

ICMP error messages are another common source of springboard attacks. The `ICMP_BANDLIM` tool (compiled into the GENERIC kernel by default) limits the rate at which responses to ICMP error messages are sent, limiting such an attack’s effectiveness. In FreeBSD 5.0 and later, `ICMP_BANDLIM` is no longer even an option—it can’t be disabled. You can, however, tune the number of ICMP responses your machine will handle per second with the `sysctl` command:

```
# sysctl net.inet.icmp.icmplim=100
net.inet.icmp.icmplim: 200 -> 100
```

Use `sysctl -a` to determine what the currently set value for the variable is, as shown here:

```
# sysctl -a net.inet.icmp.icmplim
net.inet.icmp.icmplim: 100
```

## Physical Security

The most secure system in the world can always be compromised if there’s a possibility that an unauthorized person can gain physical access to the server machine itself, because no amount of software security can defend against someone with a screwdriver.

Secure co-location facilities are vital for a commercial or otherwise high-profile Internet server. Such a facility provides locked server cabinets in locked machine rooms, and only employees of the facility are generally allowed to open the cabinets and physically access the machines. Your system might itself be in a rack-mounted case with a locked front panel and BIOS security measures that warn you if the panel has been removed.

Anybody with physical access to the machine can reboot it into single-user mode, which doesn’t prompt for the root password in the default configuration. You can change this so that it does prompt for a password by telling `/etc/ttys` that the console is “insecure,” meaning that you can’t guarantee that anybody accessing it is authorized:

```
console none                  unknown off insecure
```

However, this doesn’t stop an intruder from being able to boot from a floppy disk or CD to compromise your system. Other devices attached to the machine can also be used to gain unauthorized access: modems, for example, or wireless networks, which should not be a part of any machine from which you’re trying to restrict physical access. The bottom line is that you cannot secure your system unless you control all physical access to it.

## Other Security Resources

This chapter has covered a few general security topics as they apply specifically to FreeBSD. However, the subject of network security is vast, and it grows each day as more and more malicious users try to find ways to bring down the Internet’s core services.

A number of excellent resources are available on security, both FreeBSD specific and general, that you would do well to check out.

### The man security Page

Compiled by Matthew Dillon, the man security page contains a long discussion of general security topics and good administrative habits. It also provides miscellaneous tips for preventing break-ins and DOS attacks. This page is the basis for a number of online resources, including part of the *FreeBSD Handbook*.

### Mailing Lists

Join the freebsd-security@freebsd.org mailing list. Do this by sending a message to majordomo@freebsd.org, with `subscribe freebsd-security` in the message body. This list is where the most up-to-date discussion of security issues takes place. As an administrator, you will need to keep abreast of the most recent developments so you can defend against each new vulnerability as it becomes known.

Another useful security list, geared toward Unix security issues in general, is Bugtraq. This list receives advisories of all major issues that arise in Internet security, sometimes before their full impact on FreeBSD is known. Bugtraq is hosted at `http://www.securityfocus.com`, where you can subscribe to the list or search its archives.

### FreeBSD Security Advisories

Security advisories are sent out by the FreeBSD Security Officer onto the `freebsd-announce@freebsd.org` and `freebsd-security@freebsd.org` lists to warn of newly discovered vulnerabilities. Each advisory is also archived at `http://www.freebsd.org/security/`.

An advisory contains a complete discussion of the nature and impact of a vulnerability, whether it exists in part of the core FreeBSD system or in a program in the ports collection, whether it’s FreeBSD specific or not, and how to work around or solve the problem. Because it would be inviting hackers to a free lunch to disclose the exact nature of a vulnerability before a fix is available, advisories are released only after a solution has been found. This is one good reason to be subscribed to `freebsd-security@freebsd.org`, because there will be discussion of a vulnerability there even before the advisory is released.

Fixes to vulnerabilities in ports or packages usually mean simply synchronizing your ports tree and rebuilding the port in question (see Chapter 14). A fix to the core FreeBSD system, though, is usually checked into the appropriate -STABLE or -CURRENT source tree; to take advantage of it, you will need to rebuild that part of your system after synchronizing your sources. If the fix is in a sufficiently fundamental part of the system code, you may need to do a complete `make world` to make your system secure. Instructions on how to do this are in Chapter 17, “Keeping Up to Date with FreeBSD.”

### Web Resources

The FreeBSD Security Information page, `http://www.freebsd.org/security/`, contains resources and links geared toward the FreeBSD administrator or developer. Security advisories are archived here, as are various tips and tricks for reducing your risk factors.

The FreeBSD Security How-To (`http://people.freebsd.org/~jkb/howto.html`) is a lengthy discussion of various methods by which you can secure your FreeBSD system. It covers many topics discussed in this chapter, and many more that are not.

CERT (http://www.cert.org), the Internet's foremost security advisory site, maintains resources on security vulnerabilities in all different operating systems and is widely regarded as the authoritative source of alerts and recovery information. CERT also handles incident reports; you can report a break-in there, and they will work with the proper authorities to catch the perpetrator.

SecurityFocus, the site that hosts Bugtraq, is a security news site covering topics from intrusion-detection systems to virus protection. It also has numerous articles on good security practices and how to run a system responsibly. It doesn't have much in the way of FreeBSD-specific material, but much of its information can be applied to any platform. The URL is http://www.securityfocus.com.

### Books

Two books suggested in /etc/rc.firewall are Firewalls & Internet Security, by William R. Cheswick and Steven M. Bellovin, for general network security topics, and Building Internet Firewalls, 2nd Edition, by Brent Chapman and Elizabeth Zwicky, for fuller coverage of fire-wall theory and practice.

Further books and papers on security are listed and scored for usefulness at the SecurityFocus site, under the "Library" link.
