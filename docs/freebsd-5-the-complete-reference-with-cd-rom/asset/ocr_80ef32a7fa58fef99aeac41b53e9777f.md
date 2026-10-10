The new rule is identical to the default rule, except that it specifies that packets be allowed rather than denied. (In listing the rule, `ipfw` has converted the `all` keyword to `ip`; the two are synonymous, so this change is unimportant in practice.)

Now, suppose you want to create a real firewall on a computer that functions as a client and runs an SMTP (mail) server. If you want to use a default-deny policy, you should clear the default-allow rule that was just created. You can do this with either of the following commands:

```
# ipfw delete 65534
# ipfw flush
```

The first command deletes just the one added rule, whereas the second deletes all the rules except the default rule. Because only one rule has been added, they have equivalent effects in this case. At this point, your system won't accept any incoming or outgoing traffic. You can add incoming traffic to your SMTP server with the following command:

```
# ipfw add allow tcp from any to 172.23.45.67 25
```

This command assumes that the server's IP address is 172.23.45.67; change that detail as required. SMTP servers must normally accept mail from any site, so the source specification is quite lenient. At this point, the system accepts incoming port-25 access, but the mail server can't send replies. To open port 25 to outgoing traffic, a rule like the following does the trick:

```
# ipfw add allow tcp from 172.23.45.67 25 to any
```

Now the computer's mail server should be accessible, assuming it's running. You can verify this configuration by sending mail from another system or by using Telnet on another computer to access port 25. (Consult Chapter 19 for information on configuring a mail server.) Chances are you won't be able to send mail from the system you're configuring, though, because the firewall blocks DNS queries, which go out on UDP port 53. You can rectify this problem with the following rules:

```
# ipfw add allow udp from 172.23.45.1 53 to 172.23.45.67
# ipfw add allow udp from 172.23.45.67 to 172.23.45.1 53
```

These commands permit the system to communicate with UDP port 53 on 172.23.45.1 (the DNS server in this example; this IP address should be changed for your network). If you have multiple DNS servers, you may need to duplicate these lines, with appropriate changes to the DNS server IP address for each DNS server.

The rules presented thus far enable servers to function, but what about clients? Part of the job is permitting outgoing connections. If you want to support particular protocols,