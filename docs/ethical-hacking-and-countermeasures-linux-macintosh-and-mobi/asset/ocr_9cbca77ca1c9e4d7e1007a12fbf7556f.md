![](bbox=[0.27, 0.08, 0.78, 0.38])

Figure 3-6 Cisco routers request authentication when they are accessed.

# HTTP Configuration Arbitrary Administrative Access Vulnerability

A vulnerability that affects most Cisco routers (when conditions are right) is the HTTP Configuration Arbitrary Administrative Access Vulnerability. Arbitrary commands can be executed on a remote Cisco router by a request through HTTP as in the following:

```
/level1-<$NUMBER>/exec/show/config/cr
```

In this string, $NUMBER is an integer between 16 and 99.
An attacker can use this to cut down network access and can even lock users out of a router. Any Web browser can be used to exploit this vulnerability. If an attacker navigates to a particular router—the IP address 10.0.1.252 is used in the example—the image may look like the one shown in Figure 3-6.
If the attacker clicks the Cancel button and adds /level/99/exec/show/config to the router's IP address, the startup configuration of the device will be presented (Figure 3-7).
This vulnerability exploit reveals the configuration of the router, interfaces, access control lists (ACLs), and SNMP community string. In the example, the Vigenere encryption scheme was used to encrypt the password. This encryption scheme can be easily cracked with the help of the GetPass! tool (Figure 3-8).
If a password is stored in the form of an MD5 hash, a dictionary attack can be used to crack it with tools like John the Ripper and Cain and Abel.
After cracking the password, the attacker can log in via telnet and gain complete administrative control of the router. This vulnerability can be eliminated by completely disabling all Web configuration interfaces.

# Router Attacks

Router attack topology is illustrated in Figure 3-9. Routers can reveal an immense amount of sensitive information and allow access to important network functions if they are compromised. If a router is accessed, an attacker can do the following:

+   - Gain knowledge about all the possible vulnerabilities in the network
+   - Interrupt communication by dropping or misrouting packets passing through the router
+   - Completely disable the router and its network
+   - Compromise other routers in the network and possibly also the neighboring networks