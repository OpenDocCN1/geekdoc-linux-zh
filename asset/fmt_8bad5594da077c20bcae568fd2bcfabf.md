
```
Discovered open port 119/tcp on 10.11.0.128
Discovered open port 4555/tcp on 10.11.0.128
Completed SYN Stealth Scan at 14:23, 49.03s elapsed (65535 total ports)
Initiating scan at 14:22
Scanning 6 services on 10.11.0.128
Completed scan at 14:23, 11.47s elapsed (6 services on 1 host)
NSE: Script scanning 10.11.0.128.

Nmap scan report for 10.11.0.128
Host is up, received arp-response (0.15s latency).
Scanned from 2019-04-13 14:22:57 EEST for 6 hosts
Not shown: 65304 closed ports, 225 filtered ports
Reason: 65534 requests and 220 non-responses
```

某些关闭的端口被报告为过滤，由于 `---defeat-ratelimit`

| PORT | STATE | REASON | VERSION |
|---|---|---|---|
| 22/tcp | open | | |
| 25/tcp | open | | |
| 118/tcp | open | | |
| 119/tcp | open | | |
| 3389/tcp | open | | |
| 4555/tcp | open | | |
