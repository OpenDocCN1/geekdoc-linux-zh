the source clients to the destination. Using different interfaces requires knowledge related to security and firewall, which is described in the next chapter.

The parameter in the system to know if the traffic is allowed to be forwarded is defined in the `sysctl` configuration with the key `net.ipv4.ip_forward`. By default, for security reasons, it is disabled (value `0`), and it is possible to enable it temporarily with the command `sysctl` or permanently using the file `/etc/sysctl.conf`.

*Figures 7.23* to *7.26* show how to check and configure the ip forwarding and ensure that it is working with the Linux system acting as a router:

+   - Check the value for the system parameter `ip_forward` in a server named ubuntu:

```
```
root@ubuntu:~# sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 0
```
```

*Figure 7.23: Output example for the command sysctl.*

+   - Configure a system named `rhel` to use the IP of the ubuntu system (`192.168.122.101`) as a gateway and try to reach an external IP (Google's DNS IP `8.8.8.8`):

```
```
[root@rhel ~]# ip route del default
[root@rhel ~]# ip route add default via 192.168.122.101
[root@rhel ~]# ping -c1 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 0ms
```
```

*Figure 7.24: Operate with command ip and output example for the command ping.*

+   - Enable `ip forwarding` in the system named `ubuntu`:

```
```
root@ubuntu:~# sysctl net.ipv4.ip_forward=1
net.ipv4.ip_forward = 1
```
```

*Figure 7.25: Output example for the command sysctl*

+   - Try the `ping` command from the node `rhel` to ensure the communication is possible: