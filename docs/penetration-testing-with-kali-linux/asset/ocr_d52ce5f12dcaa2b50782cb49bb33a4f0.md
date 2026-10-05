# OffSec

beta.megacorp.com. 5 IN A 51.222.169.209
fs1.megacorp.com. 5 IN A 51.222.169.210
inetranet.megacorp.com. 5 IN A 51.222.169.211
mail.megacorp.com. 5 IN A 51.222.169.212
mail12.megacorp.com. 5 IN A 51.222.169.213
ns1.megacorp.com. 5 IN A 51.79.37.11
ns2.megacorp.com. 5 IN A 51.222.39.63
ns3.megacorp.com. 5 IN A 66.70.207.188
router.megacorp.com. 5 IN A 51.222.169.214
sitem.megacorp.com. 5 IN A 51.222.169.215
snmp.megacorp.com. 5 IN A 51.222.169.216
syslog.megacorp.com. 5 IN A 51.222.169.217
test.megacorp.com. 5 IN A 51.222.169.219
vpn.megacorp.com. 5 IN A 51.222.169.220
www.megacorp.com. 5 IN A 149.56.244.887
ww2.megacorp.com. 5 IN A 149.56.244.887

megacorp.com class C netranges:

```
51.79.37.0/24
51.222.39.0/24
51.222.169.0/24
66.70.207.0/24
149.56.244.0/24
```

Performing reverse lookup on 1280 ip addresses:

```
18.37.79.51-in-addr.arpa. 86400 PTR ns1.megacorpone.com.
...
```

> List 49 - Using Denum to automate hosts enumeration

We have discovered several previously-unknown hosts as a result of our extensive DNS enumeration. As mentioned in this Module, information gathering has a cyclic pattern, we will need to perform all the other passive and active enumeration tasks on this new subset of hosts to disclose any new details.

The enumeration tools covered are practical and straightforward, and we should familiarize ourselves with each before continuing.

Having covered tools, let's explore what kind of DNS enumeration we can perform from a Windows perspective.

Although not in the LOLBAS listing, nslookup is another great utility for Windows DNS enumeration and still used during ‘Living off the Land’ scenarios.

> Applications that can provide unintended code execution are normally listed under the LOLBAS project