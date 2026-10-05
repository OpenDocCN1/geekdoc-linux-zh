# CRITERIA | Comprehensive review

...output omitted...

6.3. From workstation, use the ping c2 command to verify that you can reach the host with the IPv4 address 172.25.250.211.

```
[student@workstation ~]$ ping -c2 172.25.250.211
PING 172.25.250.211: 56(84) bytes of data.
64 bytes from 172.25.250.211: icmp_seq=1 ttl=64 time=0.246 ms
64 bytes from 172.25.250.211: icmp_seq=2 ttl=64 time=0.296 ms

--- 172.25.250.211 statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 50ms
rtt min/avg/max/mdev = 0.246/0.271/0.296/0.025 ms
```

7. On serverb, restore the original network settings by activating the original network connection.

7.1. Go back to the console and use the nmcli command to activate the original network profile.

```
[student@server ~]$ sudo nmcli connection on "Wired connection 1"
...output omitted...
```

The name of the original connection profile might differ on your server. If so, replace the name shown in this solution with the name you actually saw on your system. You should be able to find it with nmcli connection show if you have forgotten it.

7.2. From workstation, open an SSH session to serverb as student to ensure that the original network settings are successfully activated.

```
[student@workstation ~]$ ssh serverb
...output omitted-review4~
[student@server-review4 ~]$
```

7.3. Log out of server-review4 and exit all one terminal on workstation.

```
[student@server-review4 ~]$ exit
logout
Connection to serverb closed.
[student@workstation ~]$
```

# Evaluation

On workstation, run the lab rhcsa-rh124-review4 grade command to confirm success of this exercise.

```
[student@workstation ~]$ lab rhcsa-rh124-review4 grade
```