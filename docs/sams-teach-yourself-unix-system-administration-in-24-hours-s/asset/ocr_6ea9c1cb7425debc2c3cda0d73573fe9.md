```
; ; Query time: 5 msec
; ; SERVER: 192.168.1.250#53(192.168.1.250)
; ; WHEN: Fri Apr 12 01:23:58 2002
; ; MSG SIZE  rcvd: 113
```

If you get back something that looks similar to this, everything is working fine with your configuration. If not, go back and double-check your settings.

> If you find that dig can't report information on domains on which you have set up master records, check the syslog log file for detailed problems encountered by named upon startup. Most likely, the syslog output will be called /var/log/messages.

2. The fourth line of the output gives us a status code status: NOERROR telling us that our query was completed successfully. Line five gives us some stats: how many queries, answers, authorities, and additional information was found for the specified domain.

The next lines are broken up into sections detailing the question asked, the answer found, the authority providing the answer, and any additional information.

We asked the simple question, "Who is intuitive.com?" The answer is IP address 161.58.20.91. The authority answering the question is the two name servers ns11a.verio-web.com and ns11b.verio-web.com. And finally, the additional section gives us the IP address of ns11b.verio-web.com.

3. This was a simple example to ensure named responds to requests, but clearly it didn't return all the information in our zone file.

How can we see it all? By asking for a zone transfer. The wrinkle is that you can only request a zone transfer from the authoritative server, whether it's an NS or SOA. The solution is to ask dig for it explicitly:

```
# dig intuitive.com soa
; <<>> DiG 9.1.3 <<>> intuitive.com soa
;; global options:  printcmd
;; Got answer:
;; ->HEADER<<- opcode: QUERY, status: NOERROR, id: 19035
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 1

;; QUESTION SECTION:
;intuitive.com.          IN      SOA
```