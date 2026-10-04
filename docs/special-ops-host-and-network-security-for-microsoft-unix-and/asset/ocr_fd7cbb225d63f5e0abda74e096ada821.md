# 406 Chapter 8 · Attacking and Defending DNS

Among the TLDs, delegated authority is in effect. TLDs are not always directly served by root servers, they are commonly hosted on TLD operatorcontrolled systems that receive delegation from the root servers.You can obtain a listing of the specific TLD servers via dig. For example, if you want to know what servers host the .mil TLD you would run the following command:

```
ambient[specialops]# dig mil. NS

; << DIG 9.2.1 <<>> mil. NS
;; global options: printcmd
;; Got answer:
;; ->HEADER<< opcode: query, status: NOERROR, id: 50277
;;; flags: qd ra; QUERY: 1, ANSWER: 11, ADDITIONAL: 11

;; QUESTION SECTION:
;mil. IN NS

;; ANSWER SECTION:
mil. 86151 IN NS CON1.NIPR.mil.
mil. 86151 IN NS B.ROOT-SERVERS.NET.
mil. 86151 IN NS A.ROOT-SERVERS.NET.
mil. 86151 IN NS EUR1.NIPR.mil.
mil. 86151 IN NS PAC1.NIPR.mil.
mil. 86151 IN NS H.ROOT-SERVERS.NET.
mil. 86151 IN NS G.ROOT-SERVERS.NET.
mil. 86151 IN NS CON2.NIPR.mil.
mil. 86151 IN NS EUR2.NIPR.mil.
mil. 86151 IN NS E.ROOT-SERVERS.NET.
mil. 86151 IN NS PAC2.NIPR.mil.

;; ADDITIONAL SECTION:
CON1.NIPR.mil. 172551 IN A 199.252.175.234
B.ROOT-SERVERS.NET. 154404 IN A 128.9.0.107
A.ROOT-SERVERS.NET. 154404 IN A 198.41.0.4
EUR1.NIPR.mil. 172551 IN A 199.252.154.234
PAC1.NIPR.mil. 172551 IN A 199.252.180.234
H.ROOT-SERVERS.NET. 154404 IN A 128.63.2.53
```

![](bbox=[0.082, 0.943, 0.255, 0.966])