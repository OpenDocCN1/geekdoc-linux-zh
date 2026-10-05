Connection 'static' (ac8620e6-b77e-499f-9931-118b0b15807) successfully added.

3.2. Use the nmcli command to activate the connection settings.

```
[student@server ~]$ sudo nmcli connection up
```

+   4. Use the hostnamectl command to statically set the name of server to server-review4.lab.com and verify the new name using the hostname command.

```
[student@server ~]$ sudo hostnamectl set-hostname server-review4.lab.com
[sudo] password for student: student
[student@server4 ~]$ hostname
server-review4.lab.com
```

+   5. On server, edit the /etc/hosts file to set client-review4 as the canonical host name for the IPv4 address 172.250.250.10 of the host server.lab.example.com.

+   5.1. Edit the /etc/hosts file to add client-review4 as a name for the 172.250.250.10 IPv4 address. You may use the sudo vim /etc/hosts command to edit the file.

```
172.250.250.10 servera.lab.example.com servera client-review4
```

+   5.2. Use the ping command to verify that you can reach 172.250.250.10 using the canonical host name client-review4.

```
[student@server ~]$ ping -c2 client-review4
PING server.lab.com (172.250.250.10) 56(84) bytes of data.
64 bytes from server.lab.com (172.250.250.10): icmp_seq=1 ttl=64 time=259 ms
64 bytes from server.lab.com (172.250.250.10): icmp_seq=2 ttl=64 time=391 ms

--- server.lab.com ping statistics ---
2 packets received, 0% packet loss, time 33ms
rtt min/avg/mdev = 259/325/66/0.066 ms
```

+   6. Adjust the network connection to configure the additional IPv4 address 172.250.250.211 with the mask 255.255.255.0 on the same interface of serverb that has the existing static settings. Do not remove the existing IPv4 address. Make sure that serverb responds to all addresses when the connection you statically configured on its interface.

+   6.1. Use the nmcli command to add the new IP address.

```
[student@server ~]$ sudo nmcli connection modify static \\
+ipv4.addresses "172.250.250.211/24"
```

+   6.2. Use the nmcli command to activate the new IP address.

```
[student@server ~]$ sudo nmcli connection up
```