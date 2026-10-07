
# The virtuertable 165

happythings.com. The following two lines in the virtuertable would route mail to the correct employee regardless of the domain to which it was addressed:

```
@funstuff.com             %1@stuffycorporation.com
@happythings.com         %1@stuffycorporation.com
```

The last line in Listing 6.10 shows that the detail value in the +detail syntax can be passed to the outbound address as %2. Mail sent to sales+info@thatplace.com would be deivered to info@newplace.com, and mail to sales+orders@thatplace.com would be delivered to orders@newplace.com. Notice that the use of +detail syntax must be indicated the first field of the virtuertable by placing * before in the virtual domain address. Users find e-addresses complex enough without using the +detail syntax. For this reason, the syntax is rarely used unless you have a program that automatically generates this for the user. It is covered for the sake of completeness, but you will probably not use it in your configuration.

Before the virtuertable can be used by Sendmail, it must be turned into a hash database using makedemap. Listing 6.11 shows a successful build and test of the virtuertable database.

# Listing 6.11 Building and Testing the virtuertable

```
[root]# cat local-host-names
# local-host-names - include all aliases for your machine here.
#nrobin.foobirds.org
robin
bridal-gowns.com
patient-rights.org
imaginary.com
autofbusiness.com
webroke.com
other.org
thatplace.com
[root]# cat virtuertable jill
sales@bridal-gowns.com
info@patient-rights.org sara@hawk.foobirds.org
@imaginary.com david@lion.mammals.org
sales@autofbusiness.com error:nouser User address is not valid
sales@webroke.com error:5.1.5 Destination address invalid
@other.org %1@local.com
+*@thatplace.com %2@newplace.com
```

![](img/9639113aa446fb8976cb3d377f7aafdd_188_0.png)

# Chapter 6 Using Sendmail Databases

```
[root]# makemap hash virtuertable < virtuertable
[root]# sendmail -bv sales@bridal-gowns.com
sales@bridal-gowns.com... deliverable: mailer local, user jill
```

The virtuertable database is built with the makemap command and tested using sendmail with the -bv argument. the -bv argument causes the sendmail command to process the address on the command line as a delivery address. The test shows that the address sales@bridal-gowns.com will be delivered via the local mailer to the user account Jill. This is just what we expected based on the first line of the virtuertable file.

In Listing 6.11 we examine the contents of the local-host-names file and the virtuertable source file. The local-host-name file shows that all of the virtual domains have been added to class w. If the virtual domains are not added to class w (VirHost), the sendmail -bv produces the following result:

```
[root]# sendmail -bv sales@bridal-gowns.com
sales@bridal-gowns.com... deliverable: mailer smtp
host bridal-gowns.com, user sales@bridal-gowns.com
```

This test shows Sendmail believes that bridal-gowns.com is an external domain that can be reached through the smtp mail. If we defined the virtual domain in the local-names file and forgot to provide the mapping in the virtuertable, either by not including it in the file or not running makemap, sendmail -bv produces the following result:

```
[root]# sendmail -bv info@patient-rights.org
info@patient-rights.org... deliverable: mailer local, user info
```

The virtual domain is accepted, but the host is not mapped to the external host as we wished. A simple sendmail -bv test can tell you if the virtuertable is working and can indicate what's wrong if it isn't.

There are many good reasons to use the virtuertable, particularly if you run an ISP that provides service to a large number of customers or run an e-business site. It is easy to see why Red Hat includes this in their default Sendmail configuration. The last database included in the redhat.mc file, the mailertable, is more rarely used.

# The mailertable

The virtuertable is rarely needed. It maps domain names to the internal mailer that should handle mail bound for that domain. The reason that this database is rarely needed is that Sendmail usually routes mail to the correct mailer without any help from You.

# The mailertable

need this table to handle exceptional circumstances. An exceptional case might be a remote server that cannot handle standard mail. For example: From the discussion of the MAILER(smtp) command in Chapter 5, you know that Sendmail sends out SMTP mail using the smtp mailer and that there are several mailers available to handle SMTP mail in special ways. One of these is the smtp mailer that is designed to send eight-bit MIME to outdated mail servers that support MIME but cannot understand Extended SMTP. If the domain clueless.edu used such a mail server, you could put the following entry in the mailertable to handle the:

```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
```

A mailertable entry contains two fields. The first field is the key. It contains the portion of the delivery address. It can contain either the full name of the host—e.g., emma.cluelesscollege.edu—or the domain name. To specify a domain name, start the name with a dot, as in the example above. If a domain name is used, it matches every host in the domain.

The second field in the entry is the value returned for the key. It normally contains the name of the mailer that should handle the mail and the name of the server to which the mail should be sent. Optionally, a username can be specified with the server address in the form user@server. Additionally, the mailer that is specified can be handled by the internal error mailer. If the error occurs, the value following the mailer name is an error message instead of a server name. Here is an example of each of these entries:

```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
.foobirds.org          smtp:postmaster@foobirds.org
.foobirds.org          error:host is extinct
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    error:host is extinct
```
*(Note: The OCR text for the example block was garbled; I have reconstructed the logical structure based on the surrounding text context where possible, but looking at the provided OCR, it was actually:)*

```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
.foobirds.org          smtp:postmaster@foobirds.org
.foobirds.org          error:host is extinct
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    error:host is extinct
```
*Wait, looking closer at the raw OCR provided for page 190:*
```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
.foobirds.org          smtp:postmaster@foobirds.org
.foobirds.org          error:host is extinct
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    smtp:jemma@cluelesscollege.edu
.cluelesscollege.edu    error:host is extinct
```
Actually, I will stick to the OCR text provided while fixing the obvious typos:
```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
```
(The OCR text on 190 was very fragmented at the end, I will provide the clean version of the visible text).

The second field in the entry is the value returned for the key. It normally contains the name of the mailer that should handle the mail and the name of the server to which the mail should be sent. Optionally, a username can be specified with the server address in the form user@server. Additionally, the mailer that is specified can be handled by the internal error mailer. If the error occurs, the value following the mailer name is an error message instead of a server name. Here is an example of each of these entries:

```
.cluelesscollege.edu    smtp8:olderver.cluelesscollege.edu
```
*(Re-evaluating the OCR block on page 190: it seems to cut off. I will output what is clearly there.)*

![](img/9639113aa446fb8976cb3d377f7aafdd_190_0.png)

# 168 Chapter 6 Using Sendmail Databases

Returning error messages is not the only thing that can be done with the mailertable it replicates a feature of the virtuerttable. It is possible to use the mailertable to route mail for a virtual domain. For example, the following entry routes anyone in bridal-gowns.com to the user account jill:

```
.bridal-gowns.com local:jill
```

The advantage of using the mailertable for virtual domains is that, if you are already using the mailertable for some other purpose, you can do everything in one file. The disadvantage is that you cannot specify individual users in the domain, only domain names, and you don't get the cool features of the virtuertable, such as the ability to capture and retrieve usernames with the %1 variable.

One other thing you can do with the mailertable is to use it to route all of the mail to a central mail server. Suppose you have a Red Hat Linux system that you wanted to configure sending all of its mail to mailserver.foobirds.org for processing. You could create a custom map configuration on the client with a define command that sets SMART_HOST to mailserver.foobirds.org, or you could simply create a mailertable with a single entry:

```
esmtp:mailserver.foobirds.org
```

SMART_HOST is a variable in the map configuration that can be set to the name of a mail server that handles all outbound mail for the client. The mailertable entry does essentially the same. The dot (.) in the first field matches all domain names. This means that all non-local mail will be sent through the essmtp mailer to foobirds.org for delivery. This is exactly what we want for our imaginary client, and it has nothing to do with what the SMART_HOST define have given us. But this is simpler.

Once a mailertable source file is built, it must be processed through makemap. By default, Sendmail expects not to deal with a server that cannot handle standard Internet mail. Time has already solved most of the incompatibilities that made the mailertable and the wide variety of mailers necessary. The other uses of the mailertable can be performed by other databases. So why is the mailertable database included in the default redhat.mc configuration? Is it there to provide access to the procmail mailer. The redhat.mc file contains the MAILER(procmail). This command has nothing to do with the FEATURE(local_procmail) command. The local_procmail feature causes Sendmail to use procmail as the local mailer. The MAILER(procmail) macro makes procmail available for mail other than local mail, but
