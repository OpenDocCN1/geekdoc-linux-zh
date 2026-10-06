# Chapter 3: Enumeration 41

250-2.1.5 <alan@marketing.somecompanyanasexample.com>
250-2.1.5 <joe@marketing.somecompanyanasexample.com>
250-2.1.5 <dilip@marketing.somecompanyanasexample.com>
250-2.1.5 <john@legal.somecompanyanasexample.com>
250-2.1.5 <kavita@sales.somecompanyanasexample.com>

![](bbox=[0.098, 0.196, 0.135, 0.239])

# Turn Off EXPN and VRFY

Configure your SMTP server not to support EXPN and VRFY. To do this in Sendmail, edit /etc/sendmail.cf and set PrivacyOptions to authwarnings, noexpn, novrfy.

# DNS (Domain Name System): 53 (TCP/UDP)

DNS is a protocol used to translate between domain names and IP addresses.

# Obtain BIND Version Information

The widely used DNS server software on Linux and BIND (Berkeley Internet Name Domain). The dig tool can be used to query for the version of BIND running on a particular host.
As an example, if the IP address of the host running BIND is 192.168.1.1:

```
[bash] dig -t txt -c chaos VERSION.BIND @192.168.1.1
<<>> DIG 9.2.1 << -t txt -c chaos VERSION.BIND @192.168.1.1
;; global options: printcmd
;; Got answer:
;; >>HEADER<< opcode, status: NOERROR, id: 22464
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0,
;; ADDITIONAL:0

;; QUESTION SECTION:
;;VERSION.BIND.		CH	TXT

;; ANSWER SECTION:
VERSION.BIND.	CH	TXT	"8.3.3-REL"

;; Query time: 40 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
;; WHEN: Wed Jan 15 09:46:22 2003
;; MSG SIZE rcvd: 64
```

Enumerate Remote Services