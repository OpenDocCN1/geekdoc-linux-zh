To do this, select Feature from the drop-down list at the bottom of the page, and click the Add new entry of type button. Then, select genericstable (Outgoing Addresses). Next in the parameters field you specify the type and location of the table file, hash -o /etc/mail/genericstable. The single quote marks are not required, as Webmin will insert them for you. For later convenience it is probably wise to use the arrow buttons on the right of the page to raise the new entry to be just below the other FEATURE lines in your file. It isn’t strictly necessary, but it is nice to have neat configuration files, even if Webmin hides them from you most of the time.

After saving the changed file, you will generate the new sendmail.cf (don’t forget to back up the old one to another file if you’ve already set up Sendmail). To create a new sendmail.cf based on your .mc file, click the Rebuild Sendmail Configuration button. You’ll then be able to open the Outgoing Domains page, and create the new genericstable file and edit it normally. A restart of Sendmail will be required to apply the changes you’ve made.

# Tutorial: Setting Up Sendmail

When first installed Sendmail will only need a few small changes in order to begin providing service for sending and receiving mail. The first step is to specify for whom mail will be accepted, which you will specify in the Local Domains page, while the second step will be to permit local network users to send, or relay, email through the server, which will be specified in the Spam Control page.

NOTE This tutorial assumes you have already configured DNS service for your network, including an MX record for your domain. If you haven’t already done so, refer back to the BIND chapter, and configure name resolution before attempting the steps in this tutorial.

# Configuring Domains to Receive Mail For

By default, Sendmail is not configured to receive mail for any host or network other than the machine on which it is running. So you must first configure Sendmail to permit anyone to send mail for delivery to your domain through your server. Open the Local Domains page, and enter the domains for which your server will accept mail. In my case, I would enter swelltech.com. Any number of domains can be entered here, as can host names, so I could also enter www.swelltech.com if ever I expected mail to be delivered to that address.

Click the Save button to update the sendmail.cf file. This will add new Cw lines to include your specified domains.

# Permitting Local Users to Relay

The next step to achieving a simple mail server is to permit your local users to send mail through your server. Click the Spam Control icon, and create one or more rules matching your local networks. To create a new rule, first select a Mail source of Network, and specify the IP of the network you’d like to relay for. For example, on a local network using private IP addresses, one might enter 192.168.1 to specify all of the hosts in the 192.168.1.0/24 network. Then, select Allow relaying, and click Create to add the new rule to the access file.