# Attacking and Defending DNS · Chapter 8 409

```
1STGOVT.GOV.                  NS NS-WEST.CERF.NET.
1STGOVT.GOV.                  NS NS-EAST.CERF.NET.
21STCENTURY.GOV.             NS AUTH00.NS.UU.NET.
21STCENTURY.GOV.             NS AUTH61.NS.UU.NET.
4GIRLS.GOV.                   NS CHERRY.HHS.GOV.
4GIRLS.GOV.                   NS DNS001.SYS.GI.NET.
4GIRLS.GOV.                   NS DNS003.SYS.GI.NET.
4WOMAN.GOV.                   NS CHERRY.HHS.GOV.
DAVISBACON.GOV.               NS AUTH40.NS.UU.NET.
                               NS
CROW.SEC.GOV.                  A 204.192.28.11
GOTCHA.TREAS.GOV.             A 204.151.246.80
PENGUIN.SEC.GOV.             A 204.192.28.20
PUFFIN.SEC.GOV.               A 12.40.163.140
PEEWEE.USDCHI.GOV.             A 198.180.232.65
DRACULA.USPSPOIG.GOV.          A 208.181.82.66
```

... Truncated root zone file is good for verifying information or troubleshooting an authoritative server; overall, this is an uncommon practice, but because it provides proprietary information, general questions such as “What are all the educational domain names?” or “How many government domains are hosted on commercial DNS servers?” can be answered easily.

As mentioned previously, the .arpa TLD is used for infrastructure purposes. To understand this, you'll examine the reverse DNS hierarchy. While submitting a reverse DNS query, you will find out what domain name 65.205.249.60. Similar to domain names, zone authority works backwards. For the PTR record of 65.205.249.60, you would look up 60.249.205.65-in-addr.arpa., as illustrated in Figure 8.5.

![](bbox=[0.697, 0.944, 0.929, 0.966])