This makes the rest of the (unsuspecting) world think that your client.com has a real mail server, as long as you have sendmail set up with the virtual configuration discussed previously.

Virtual mail service is often requested by Web site clients of ISPs. In other words, people or companies that pay an ISP to do Web site hosting (www.client-domain.com) also often request to have virtual mail service. In such a case, creating a single /etc/mail/virtusertable often is unmanageable. For example, if you are hosting hundreds of domains, /etc/mail/virtusertable will be a point of human error every time you (or your assistant administrators) modify the file. In such a case, you can create a more manageable solution. For example, to create two virtual mail services for two clients called client-a.com and client-b.com, do the following:

+   1. Create a separate virtual e-mail map file for each domain. Use a naming convention such as domain.ftr (.ftr is short for fake-to-real).
+   2. Create an /etc/mail/client-a.ftr file, which contains the content of what will normally go in /etc/mail/virtusertable for this domain. For example, this file could look like the following:
+   3. Create the /etc/mail/client-b.ftr file for the second client. This file is likely to be similar to the previous example; but, suppose that the client-b.com owner wants all e-mail addresses to be automatically mapped to her existing accounts in your hometown ISP mail server. In such a case, this map file looks as follows:

```
user1@client-1.com client1
webmaster@client-1.com unix@home-town-isp.com
@client-1.com client1
```

In this example file, the user1@client-1.com address is mapped to the local account client1; the webmaster@client-1.com is mapped to a remote ISP account; and all other possible e-mail addresses for the domain are mapped to the local account. The last entry is quite useful and often requested by virtual domain owners. It allows the client-1.com domain owner to use whatever e-mail address s/he wants on the Web site or other business publications and advertising, and still get the mail in the right place. For example, if www.client-1.com publishes an e-mail address called info@client-1.com, anyone sending mail to that account will be happily serviced by the client1 user.