provided by your organization or ISP and it does all of the DNS heavy lifting for you. In many cases, unless the DNS server already has the answer cached, it usually does not already know the answer to your question, so it has to do what is known as recursive DNS resolution. If we assume no cache is involved, a recursive DNS resolver has to go through quite a few steps before it can get your answer.

In the case of web1.example.net, first the resolver sends the request to one of the 13 root name servers—the most important name servers on the Internet. These name servers are crucial for recursive queries, so all name servers that are going to perform recursive queries have the root name server IP addresses hard-coded. The root name servers don’t know the address for web1.example.net, but they do have a list of all the .net name servers, so they reply with those along with their IP addresses. Then the resolver asks one of the .net name servers for the address for web1.example.net. The .net name servers don’t have that information either, but they do know the list of name servers responsible for example.net, so they reply with that, along with their IPs. Finally, when the resolver asks one of those servers for the address for web1.example.net, it replies back with the record (if it exists) and the resolver finally returns back to you with your answer.

That was a lot of steps, and if you are new to DNS, sometimes it can be hard to remember how recursive DNS resolution works, but dig provides a nice feature in that it can perform complete, uncached, recursive DNS requests for you and show you the complete trace for the request. You can think about it sort of like traceroute for DNS. To enable this feature, just add +trace to the end of your dig request:

```
$ dig web1.example.net +trace

;; <<> DiG 9.7.0-P1 <<> web1.example.net +trace
;; global options: +cmd
;; global options: +cmd
.             143557 IN NS m.root-servers.net.
.             143557 IN NS a.root-servers.net.
.             143557 IN NS B.root-servers.net.
.             143557 IN NS c.root-servers.net.
.             143557 IN NS D.root-servers.net.
.             143557 IN NS e.root-servers.net.
```