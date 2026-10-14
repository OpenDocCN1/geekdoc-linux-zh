The beginning of the file mostly sets Ubuntu defaults that differ from standard Postfix defaults. The core configuration for you to tweak starts at myhostname. To get full documentation on each of these options, type man 5 postconf. That manual contains all of the Postfix configuration options along with a description of their use. Here are a few of the options in the sample configuration file that you will use frequently:

+   - **myhostname**
+     This is the Internet hostname of the mail server. If you haven’t set it explicitly in this file, it will use gethostname() and use that value. A number of other options, such as myorigin, will use or reference the myhostname value if it isn’t explicitly set.

+   - **myorigin**
+     The domain name listed here is the domain that mail sent from this machine appears to come from. If, for instance, your server is named mail1.example.org but you want e-mail sent from it to appear to come from example.org, you would set this value to example.org.

+   - **mydestination**
+     This is a list of domain names for which this mail server will accept mail and consider itself the final destination. If mail arrives on this server addressed to one of these domains, Postfix will deliver it locally.

+   - **relayhost**
+     In this example this value is blank, but if you did want to route all of your outbound mail through a different mail server, you would set this value to the hostname of that server. You might use this value on all of your servers in a data center so they all point to a single outbound mail host. You could then more tightly control firewall access and have a single choke point from which to view all outbound messages.

+   - **mynetworks**
+     This value is a comma-separated list of networks (IP addresses and subnet masks) for which this server will relay mail. Be very careful with this value! If you were to set this to too broad a value and allow