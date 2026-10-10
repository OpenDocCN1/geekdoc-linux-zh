you have a choice. You should note that the licensing of NEC's version is not open how- ever, and, while it is a good product, you should be certain you meet its licensing requirements before you use it.

Another well-developed SOCKS v4/v5 product is Dante, developed by Inferno Nettverk in Norway. This is available at `http://www.inet.no/dante/`. Full source code is available with a `BSD-style` license. Inferno also packages its source in an RPM-friendly way, so you can build a binary RPM from the tarballs by typing

```
`rpm -ta dante-VERSION.tar.gz.`
```

There are still several versions of the original NEC reference software for the SOCKS version 4 server. Versions up to 4.2.2 and the 4.3 betas (which implement SOCKS version 4A with DNS resolution like version 5) are publicly available. These can be found on Sunsite, mirrors, and other FTP archives. These are getting on in years, though, and are not being developed any more. If you want more detailed knowledge of the SOCKS protocol, these are good examples, but you may have considerable difficulty building and working with this code.

SOCKS offers the following assets:

+   • Proxy clients “hidden” behind the server
+   • “Transparency” to other network systems
+   • Simple network security policy implementation on one machine
+   • Flexible filtering and screening of traffic from both directions
+   • Comparatively easy configuration

# ## TIS

Another strong proxy software package is the TIS (Trusted Information System) Firewall Toolkit. This is available at `http://www.tis.com/fwtk/` in source code form and uses a proprietary licensing arrangement instead of the `GNU Public License`. Registration is mandatory prior to download.

TIS differs from SOCKS in several key areas:

+   • Configuration is significantly more complex but versatile.
+   • It rides on top of designated firewalls.
+   • It is comprised of separate protocol proxies.
+   • It adds a layer of user interface that may hinder local transparency.
+   • It is very secure.