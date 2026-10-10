Make sure nothing is running on the Telnet port (23) and start `upnetcl` as follows:

```
# /usr/local/tis/netacl -daemon telnet telnctd
```

Alternatively, the system's /etc/inetd.conf file, which controls the behavior of the "super server" daemon known as inetd (it acts as overseer of many typical Internet protocols on a local UNIX or Linux machine), may be edited to include specific instructions on how the new TIS protocol versions will be handled.

The following is an example of how the line would look in /etc/inetd.conf:

```
telnet stream tcp nowait root /usr/local/tis/netacl telnctd
```

Once this is done, users should be greeted by the following:

```
$ telnet comnet
Trying 192.168.7.1 ... 
Connected to comnet.thenetoffect.com.
Escape character is '^]' .
comnet.thenetoffect.com telnet proxy (Version V2.1) ready:
tn-gw->
```

At the `tn-gw->` prompt, the user can then connect to an outside host by typing connect hostname or `c hostname`.

The important point is that forwarding is shut off and no services, except of course the FWTK ones you need, are used. This will provide an extremely secure proxy setup.

With TIS, Telnet and FTP sessions are not transparently conducted for end users, but external access points using those protocols are. Thus, a user would open a Telnet session with the TIS Telnet daemon, which would open an acceptable portal through the firewall and allow the external session to piggyback over it. FTP is handled similarly.

# ## Putting Squid to Work

The proxy server known as Squid uses Internet caching to reduce the number of external connections from a local area network, while also speeding up the response to the local clients if the material is within the cache.

Many philosophical issues are at play when implementing any sort of Internet caching. The server is effectively making an external connection on behalf of the local client and conducting all of the transactions as if it was the inner client.

The implication is that the contents of the cache may now contain extremely private or sensitive material, such as credit card numbers, personal data, corporate secrets, and other highly important items. Additionally, legal precedent has yet to be set on whether the caching (copying) of material constitutes copyright infringement.