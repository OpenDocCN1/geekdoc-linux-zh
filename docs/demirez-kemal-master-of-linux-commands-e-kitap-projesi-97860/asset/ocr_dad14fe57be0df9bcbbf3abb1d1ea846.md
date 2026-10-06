# 216 | Master of Linux Commands

```
root@kemal:~# host vodafone.com.tr
vodafone.com.tr has address 212.65.152.27
vodafone.com.tr mail is handled by 10 mmsc.vodafone.com.tr
root@kemal:~# -t MX vodafone.com.tr
vodafone.com.tr mail is handled by 10 mmsc.vodafone.com.tr
root@kemal:~# -t NS vodafone.com.tr
vodafone.com.tr name server ns1.vodafone.com.tr
vodafone.com.tr name server ns2.vodafone.com.tr
vodafone.com.tr name server ns3.vodafone.com.tr
root@kemal:~#
```

# Dig

One of the tools to get detailed information is the dig tool.
Usage is as a host and nslookup.

```
root@kemal:~# dig vodafone.com.tr

;<< DIG 9.9.5-9-Debian << vodafone.com.tr
;; global options: +ccmd
;; answer:
;;>>HEADER<< opcode: QUERY, status: NOERROR, id: 4663
;; flags: qr rd ra: QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 7

;; OPT PSEUDOSECTION
;; EDNS: version: 0; flags:; udp: 4096
;; QUESTION SECTION:
vodafone.com.tr. 15497 IN A 212.65.152.27

;; ANSWER SECTION:
vodafone.com.tr. 

;; AUTHORITY SECTION:
vododafone.com.tr. 12669 IN NS ns2.vodafone.com.tr
vodafone.com.tr. 12669 IN NS ns3.vodafone.com.tr
vodafone.com.tr. 12669 IN NS ns1.vodafone.com.tr.
```

The command can be used without parameters as above, it is also used with t MX and -t NS.

# Arp

The system has a table IP address-to-MAC address mappings stored. This table is called the arp table, arp or arp -a commands can be used to view this table.