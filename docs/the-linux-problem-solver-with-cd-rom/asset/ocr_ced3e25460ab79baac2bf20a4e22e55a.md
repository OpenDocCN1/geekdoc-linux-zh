```
$ nslookup www.userfriendly.org
Server:  alexandria.cs.uchicago.edu
Address:  128.135.11.87

Non-authoritative answer:
Name:    www.userfriendly.org
Address:  207.6.140.17

$ nslookup
> set q=ptr
> 207.6.140.17
Server:  alexandria.cs.uchicago.edu
Address:  128.135.11.87

Non-authoritative answer:
17.140.6.207.in-addr.arpa    name = www.userfriendly.org

Authoritative answers can be found from:
140.6.207.in-addr.arpa  nameserver = dewey.mindlink.net
140.6.207.in-addr.arpa  nameserver = giant.mindlink.net
dewey.mindlink.net      internet address = 204.174.16.4
giant.mindlink.net      internet address = 204.174.18.2
> ^D
```

For a more detailed explanation of the above examples, see DNS and BIND, 3rd Edition (O'Reilly & Associates).