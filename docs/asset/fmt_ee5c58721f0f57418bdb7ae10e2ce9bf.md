
As discussed earlier in the Apache chapter, a name-based virtual host has to have a name mapped to an IP address before you can even access its contents with a browser. BIND, of course, will be our means of providing lookup of those names. Because we're only concerned with web service for this tutorial, we only need to concern ourselves with the creation of a forward zone (a forward zone maps names to addresses).

## Create a New Master Forward Zone

Assuming you've already allowed Webmin to initialize your `named` configuration files, you're ready to add a master forward zone for your domain (Figure 8-11). Click the Create a new master zone link on the front page of the BIND module.

The Zone type should remain at its default of Forward. The Domain name/ Network field should contain the second level domain name under which your virtual hosts will reside. For example, if I had one or more virtual hosts under the `swelltech.com` domain, that would be the domain name I would enter here. If you have other second level domains, you will create a zone for each. It is easiest to allow Webmin to automatically name the Records file, and the Master server will probably be correct if your host name is configured correctly. Enter your email address, or the address you would like to be the administrative contact for this zone, into the Email address field. Finally, click Create. You will immediately be directed to the new zone for further configuration.

![](img/d84604054810a13cacfdac212ebee2f7_168_0.png)

Figure 8-11: An example master zone

## Adding Address Records

Now we can begin adding records to our new zone. The first record I would add to my `swelltech.com` domain would be `swelltech.com` itself, and it will be an address record, also known as an `A` record. Clicking the Addresses icon provides a simple form for adding the new record. Because this first record is for a host named simply `swelltech.com`, we enter nothing in the Name field. Then we enter the IP address of the server we'd like this name to point to, in my case it is the same address on which my Webmin server is running. All other fields can remain at their defaults. Clicking Create adds the record.

Follow the same steps to add another address record for `www.swelltech.com`, presumably on the same IP. All that changes from the above steps is to enter `www` in the Name field instead of leaving it blank. If you've worked through the examples in the Apache tutorial on virtual hosting, you'll now have all of the pieces for web service on both domain names.

## Adding a Mail Server Record for Mail

Because no domain would be complete without mail service, and mail service for a domain does not have to reside on the same server as web service, we need to have some way to tell mail servers where to direct our mail. Luckily, the designers of DNS have thought of that already and provide the `MX`, or mail server, record as a means of notifying other mail servers where to send email destined for the domain.

Adding a mail server is usually a two-part process. First, a new record is created pointing to the address of the mail server. In the case of small networks, this will likely be a machine that is providing other services. For example, the Swell Technology mail server resides on the same machine as our web server and our NTP time server. So, in most cases we can use a Name Alias record, also known as a `CNAME` record, for our mail server name. If you have a dedicated mail server you will use an address record instead.

## Adding a Name Alias
