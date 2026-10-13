You could also drop this into a loop, as in the following:

```
cd /var/named
for name in *
do
  domain=`echo $name | sed 's/\.zone//'`
  echo "Domain $domain:"
  /etc/named-checkzone $domain /var/named/$name
done
```

A simple utility, the rndc command is critical to effective management of named and your local name server.

# Testing DNS Setups

Now that you have your configuration and zone files straight, it's time to test it and make sure everything is copacetic.

In the old days, there was a great utility called nslookup that offered a simple way to interact with name servers. In the last few years, nslookup has been put out to the proverbial pasture and replaced with two new tools, dig and host.

# Task 18.4: Testing with dig and host

Of the two tools, you'll doubtless find dig (the Domain Information Groper) the most useful, but let's look at both of them and see what they can offer.

+   1. In its basic form, dig just needs a domain name to retrieve information:
+   ```
+   # dig intuitive.com
+   ;; <<>> DiG 9.1.3 <<>> intuitive.com
+   ;; global options: printcmd
+   ;; Got answer:
+   ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51083
+   ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 1
+   
+   ;; QUESTION SECTION:
+   ;intuitive.com.             IN      A
+   
+   ;; ANSWER SECTION:
+   intuitive.com.      28067   IN      A       161.58.20.91
+   
+   ;; AUTHORITY SECTION:
+   intuitive.com.      79973   IN      NS      ns11a.verio-web.com.
+   intuitive.com.      79973   IN      NS      ns11b.verio-web.com.
+   
+   ;; ADDITIONAL SECTION:
+   ns11b.verio-web.com. 149498 IN      A       161.58.148.98
+   ```