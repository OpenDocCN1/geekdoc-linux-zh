# ## Setting Incoming Hostnames

Consider Figure 19-1 once again. How does any given computer in this delivery chain know when to send a message on to another computer and when to store a message in a local user's mail queue? In a default FreeBSD sendmail configuration, the answer relates exclusively to the hostname in the address. When **franklin.threeroomco.com**, for instance, receives a message addressed to **ben@franklin.threeroomco.com**, the server treats the message as destined for the local account called ben. This approach is adequate for most workstations that receive little or no direct outside mail, and even for some mail server computers. In the example of mail delivery that Figure 19-1 illustrates, though, the mail was not addressed to **ben@franklin.threeroomco.com**—it was sent to **ben@threeroomco.com**. A default FreeBSD sendmail installation will fail on such a message because the computer's name is not **threeroomco.com**, although the computer is in this domain.

This problem can be overcome by using the `/etc/mail/local-host-names` file. (This file doesn't exist in a default FreeBSD installation, so you'll have to create it.) This file contains all the hostnames that sendmail is to treat as local, in addition to its standard DNS hostname. For instance, to have sendmail accept mail addressed to users at **threeroomco.com**, `/etc/mail/local-host-names` should contain that domain name. You can add more lines in order to support additional hostnames or domains. For instance, if you're configuring a computer to handle the mail for several domains, you might include lines such as the following:

```
twoomco.com
threomco.com
fouromco.com
luna.edu
```

To do any good, of course, you'd need to configure the DNS servers for these domains to point to your mail server in their MX records. This configuration tells other mail servers to deliver mail to your system, and the domain names in `/etc/mail/local-host-names` tells your server to accept this mail as local rather than treat it as a relay attempt.

> **Note**
> 
> The filename `/etc/mail/local-host-names` isn't carved in source code; it's set by a define statement in `/etc/mail/freebsd.mc`. Look for the line that defines CONFW_FILE and change it if you want to use another filename. You can also look for such a line if you're using a configuration file other than the standard FreeBSD file, to determine what file to use for this purpose.

If a sender attempts to send a message through sendmail to a domain that sendmail isn't configured to accept as local, sendmail treats it as a relay attempt. Depending upon sendmail's relay configuration and factors such as the sending machine's IP address, the server may refuse such an attempt, or accept it and send the mail to the ultimate