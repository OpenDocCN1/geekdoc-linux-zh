# # HP-UX System

# ## Description

This system, called dip, provides many of the standard services and includes Klogin/Kshell for security login and remote shell execution on ports 543 and 544, respectively.

# ## Report Results

Starting nmap V. 2.12 by Fyodor (fyodor@nnp.com, www.insecure.org/nmap/)

Interesting ports on dip.home.com (10.0.2.198):

| Port | State | Protocol | Service |
| --- | --- | --- | --- |
| 7 | open | tcp | echo |
| 9 | open | tcp | discard |
| 13 | open | tcp | daytime |
| 19 | open | tcp | chargen |
| 21 | open | tcp | ftp |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smtp |
| 37 | open | tcp | time |
| 53 | open | tcp | domain |
| 94 | open | tcp | objcall |
| 111 | open | tcp | sunrpc |
| 113 | open | tcp | auth |
| 135 | open | tcp | loc-srv |
| 382 | open | tcp | hp-managed-node |
| 512 | open | tcp | exec |
| 513 | open | tcp | login |
| 514 | open | tcp | shell |
| 515 | open | tcp | printer |
| 543 | open | tcp | klogin |
| 544 | open | tcp | kshell |
| 590 | open | tcp | tns-cm1 |
| 659 | open | tcp | unknown |
| 661 | open | tcp | unknown |
| 816 | open | tcp | unknown |
| 980 | open | tcp | unknown |
| 984 | open | tcp | unknown |
| 988 | open | tcp | unknown |
| 993 | open | tcp | simap |
| 996 | open | tcp | xtrea1ic |
| 1501 | open | tcp | sas-3 |
| 5520 | open | tcp | sdlog |
| 6111 | open | tcp | spc |
| 6112 | open | tcp | dtspc |