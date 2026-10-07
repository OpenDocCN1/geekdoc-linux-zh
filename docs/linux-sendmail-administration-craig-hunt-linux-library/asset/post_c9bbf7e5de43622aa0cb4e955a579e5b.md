
TIP If you don't have anything else in your database, you probably want an entry like the one for network 129.6 for your own network. As discussed above, Sendmail blocks all mail relaying, even mail from your clients. You use the access database and an entry like 129.6 RELAY to enable relaying for every host attached to your local network.

Once you build your access list, it must be converted into a database before Sendmail can use it. Use the makemap command to do the job, as shown below.

```bash
makemap hash /etc/mail/access.db < /etc/mail/access.txt
```

This command reads the entries in a text file named /etc/mail/access and uses them to build a hash type database in the file named /etc/mail/access.

The local-hosts and relay-domains files, the aliases and access databases are probably the most important databases that were configured in the redhat.mc configuration file. But they are not the only databases configured. Two others, virtertable and mailertable, are configured in redhat.mc. Of these, virtertable is the most useful.

## The virtertable

The virtertable is a database that routes mail for virtual mail domains. A virtual mail domain is similar to a virtual host in the Apache Web server. In the same way that a Web server can be configured to serve Web pages for host computers that do not physically exist, the Sendmail server can be configured to provide mail service for domains that do not have any existence beyond the Sendmail server itself. Creating a virtual domain allows you to advertise a meaningful domain to the outside world without having to create all of the services necessary to support a full domain.

## Defining a Virtual Domain

Each entry in the virtertable has two fields: a virtual domain and a delivery address. The first field contains the virtual domain name found in the e-mail address. The second field contains the address to which the mail is really delivered. The virtual domain name contained in the first field can be a complete address in the form of user@domain or it can be a partial address in the form of @domain. When the @domain format is used, mail to any user in the specified domain is routed to the mail address contained in the second field. Some sample virtertable entries are shown in Listing 6.9.

### Listing 6.9 Sample Virtual Domains

```
sales@bridal-gowns.com jill
info@patient-rights.org sara@hawk.foobirds.org
@imaginary.com david@lion.mammals.org
```

These three examples show basic virtual domains and delivery addresses. Mail addressed to sales@bridal-gowns.com is really delivered to the Jill account on the Sendmail server. (Like Jill is in the business of selling bridal gowns.) Requests e-mailed to info@patient-rights.org are forwarded to sara@hawk.foobirds.org. Mail sent to any user in the imaginary.com domain is forwarded to david.lion.mammals.org.

Sendmail must be configured to accept mail addressed to the virtual domains. In Listing 6.9, Sendmail must either accept bridal-gowns.com, patient-rights.org, and imaginary.com aliases for the local host or recognize them as virtual domains. You know from the discussion of the local-host-names earlier in this chapter that Sendmail accepts any name contained in class as an alias for the local host. From earlier discussion, you know how to add the three virtual domains to class. But it is not necessary to turn a virtual domain into a hostname alias to get the virtertable working. An alternative is to tell Sendmail that the virtual domain is a virtual domain by storing the domain name in the (VirthHost) class.

Domain names can be added to the (VirthHost) class one at a time using the VIRTUAL_DOMAIN macro inside the Sendmail configuration. For example, the three from Listing 6.9 can be added with the following macros:

```bash
VIRTUAL_DOMAIN('bridal-gowns.com')
VIRTUAL_DOMAIN('patient-rights.org')
VIRTUAL_DOMAIN('imaginary.com')
```

Once these lines are inserted in the macro configuration file, rerun m4 to build the new sendmail.cf file and reload Sendmail to the new configuration. This technique is complex and not very flexible, so the VIRTUAL_DOMAIN macro is only suitable if you have a few virtual domains and they do not change often.

An alternate to load the (VirthHost) class is a file. Use the VIRTUAL_DOMAIN_FILE macro to specify the path to the file that contains the list of virtual domains. For example, the following command tells Sendmail to copy /etc/mail/virtual-domains to class (VirthHost):

```bash
VIRTUAL_DOMAIN_FILE('/etc/mail/virtual-domains')
```

After adding the VIRTUSER_DOMAIN_FILE command to the macro configuration file, rerun m4 to build the new sendmail.cf file. Then add the virtual domains from Listing 6.9 to the new virtual-domains file, one domain per line, as shown below:

```bash
[craig]$ cat /etc/mail/virtual-domains
bridal-gowns.com
patient-rights.org
imaginary.com
```

Whenever new virtual domains are added to the file, send Sendmail SIGHUP signal to make sure it reads the new values and loads them into class {VirthHost}.

TIP Both the VIRTUSER_DOMAIN and VIRTUSER_DOMAIN_FILE macros require changing and rebuilding the sample configuration. Because we already had the local-host-name file in our configuration, it would be easier to add the virtual domains to that file.

Both the VIRTUSER_DOMAIN and VIRTUSER_DOMAIN_FILE macros require changing and rebuilding the sample configuration. Because we already had the local-host-name file in our configuration, it would be easier to add the virtual domains to that file.

## Defining Delivery Addresses

Each entry in the virtertable has two fields: a virtual domain and a delivery address. The first field contains the virtual domain name found in the e-mail address. The second field contains the address to which the mail is really delivered. The virtual domain name contained in the first field can be a complete address in the form of user@domain or it can be a partial address in the form of @domain. When the @domain format is used, mail to any user in the specified domain is routed to the mail address contained in the second field. Some sample virtertable entries are shown in Listing 6.9.

### Listing 6.9 Sample Virtual Domains

```
sales@bridal-gowns.com jill
info@patient-rights.org sara@hawk.foobirds.org
@imaginary.com david@lion.mammals.org
```

These three examples show basic virtual domains and delivery addresses. Mail addressed to sales@bridal-gowns.com is really delivered to the Jill account on the Sendmail server. (Like Jill is in the business of selling bridal gowns.) Requests e-mailed to info@patient-rights.org are forwarded to sara@hawk.foobirds.org. Mail sent to any user in the imaginary.com domain is forwarded to david.lion.mammals.org.

Sendmail must be configured to accept mail addressed to the virtual domains. In Listing 6.9, Sendmail must either accept bridal-gowns.com, patient-rights.org, and imaginary.com aliases for the local host or recognize them as virtual domains. You know from the discussion of the local-host-names earlier in this chapter that Sendmail accepts any name contained in class as an alias for the local host. From earlier discussion, you know how to add the three virtual domains to class. But it is not necessary to turn a virtual domain into a hostname alias to get the virtertable working. An alternative is to tell Sendmail that the virtual domain is a virtual domain by storing the domain name in the (VirthHost) class.

Domain names can be added to the (VirthHost) class one at a time using the VIRTUAL_DOMAIN macro inside the Sendmail configuration. For example, the three from Listing 6.9 can be added with the following macros:

```bash
VIRTUAL_DOMAIN('bridal-gowns.com')
VIRTUAL_DOMAIN('patient-rights.org')
VIRTUAL_DOMAIN('imaginary.com')
```

Once these lines are inserted in the macro configuration file, rerun m4 to build the new sendmail.cf file and reload Sendmail to the new configuration. This technique is complex and not very flexible, so the VIRTUAL_DOMAIN macro is only suitable if you have a few virtual domains and they do not change often.

An alternate to load the (VirthHost) class is a file. Use the VIRTUAL_DOMAIN_FILE macro to specify the path to the file that contains the list of virtual domains. For example, the following command tells Sendmail to copy /etc/mail/virtual-domains to class (VirthHost):

```bash
VIRTUAL_DOMAIN_FILE('/etc/mail/virtual-domains')
```

After adding the VIRTUSER_DOMAIN_FILE command to the macro configuration file, rerun m4 to build the new sendmail.cf file. Then add the virtual domains from Listing 6.9 to the new virtual-domains file, one domain per line, as shown below:

```bash
[craig]$ cat /etc/mail/virtual-domains
bridal-gowns.com
patient-rights.org
imaginary.com
```

Whenever new virtual domains are added to the file, send Sendmail SIGHUP signal to make sure it reads the new values and loads them into class {VirthHost}.

TIP Both the VIRTUSER_DOMAIN and VIRTUSER_DOMAIN_FILE macros require changing and rebuilding the sample configuration. Because we already had the local-host-name file in our configuration, it would be easier to add the virtual domains to that file.

## Defining Delivery Addresses

Each entry in the virtertable has two fields: a virtual domain and a delivery address. The first field contains the virtual domain name found in the e-mail address. The second field contains the address to which the mail is really delivered. The virtual domain name contained in the first field can be a complete address in the form of user@domain or it can be a partial address in the form of @domain. When the @domain format is used, mail to any user in the specified domain is routed to the mail address contained in the second field. Some sample virtertable entries are shown in Listing 6.9.

### Listing 6.10 Sample Virtual Domains

```
sales@bridal-gowns.com      jill
info@patient-rights.org      sara@hawk.foobirds.org
@imaginary.com               david@lion.mammals.org
sales@outofbusiness.com      error:User address is not valid
sales@werbroke.com           error:Destination invalid
@other.org                   %1@local.org
+thatplace.com                %2@local.com
```

These three examples show basic virtual domains and delivery addresses. Mail addressed to sales@bridal-gowns.com is really delivered to the Jill account on the Sendmail server. (Like Jill is in the business of selling bridal gowns.) Requests e-mailed to info@patient-rights.org are forwarded to sara@hawk.foobirds.org. Mail sent to any user in the imaginary.com domain is forwarded to david.lion.mammals.org.

Sendmail must be configured to accept mail addressed to the virtual domains. In Listing 6.9, Sendmail must either accept bridal-gowns.com, patient-rights.org, and imaginary.com aliases for the local host or recognize them as virtual domains. You know from the discussion of the local-host-names earlier in this chapter that Sendmail accepts any name contained in class as an alias for the local host. From earlier discussion, you know how to add the three virtual domains to class. But it is not necessary to turn a virtual domain into a hostname alias to get the virtertable working. An alternative is to tell Sendmail that the virtual domain is a virtual domain by storing the domain name in the (VirthHost) class.

The next two lines in Listing 6.10 illustrate the use of error messages. Mail addressed to outofbusiness.com is not delivered. Instead, an error message says “User is not valid” is returned to the sender. Mail sent to werbroke.com returns “Destination invalid” to the sender.

Error messages start with the keyword error, which is the name of a special mail that is built into Sendmail. Separated by a colon from the keyword error is an error condition, specified either as a keyword or as a DSN code. The DSN code can be any value defined in RFC 1893. The error condition keyword must be a keyword recognized by the error mailer. A list of valid error condition keywords is found in Chapter 8, “Understanding Rewrite Rules,” in the discussion of the error mailer.

The two lines in Listing 6.10 provide examples of how values from the input address can be used in the outbound address. The username of the input address is passed in the %s variable, so that %s in the outbound address is replaced by the username from the input address. Using the viruertable shown in Listing 6.10, mail addressed to pat@other.org would be delivered to pat@local.org and mail sent to doris@other.org would be forwarded to doris@local.org.

This is a powerful feature. Obviously, it can be used to ease the transition when you change domain names, but that is rare occurrence. More importantly, this feature can be used when the products you sell are not clearly associated with your official domain name. Assume you have an online mall that sells party products. The real name of your domain is stuffycorporation.com, but you also own the domains funstuff.com and
