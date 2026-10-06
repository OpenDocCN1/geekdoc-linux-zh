# 508 Linux Administration: A Beginner's Guide

myorigin
All e-mail sent from this e-mail server will look as though it came from this parameter.
You can set this to either $myhostname or $mydomain, like so:

```
myorigin = $mydomain
```

Notice that you can use the value of other parameters in the configuration file by placing a $ sign in front of the variable name.

mydestination
This parameter lists the domains that the Postfix server will take as its final destination for incoming e-mail. Typically, this value is set to the hostname of the server and the domain name, but can contain other names, as shown here:

```
mydestination = $hostname, localhost.$mydomain, $mydomain, \
mail.$mydomain, www.$mydomain, ftp.$mydomain
```

If your server has more than one name, for example, server.example.org and serverA.another-example.org, you will want to make sure you use all list names.

mail_spool_directory
You can run the Postfix server in two modes of delivery: directly to a user's mailbox or to a central spool directory. The typical way is to store the mail in /var/spool/mail. The variable will look like this in the configuration file:

```
mail_spool_directory = /var/spool/mail
```

The result is that mail will be stored for each user under the /var/spool/mail directory, with each user's mailbox represented as a file. For example, e-mail sent to yyang@example.org will be stored in /var/spool/mail/yyang.

mynworks
The mynetworks variable is an important configuration option: limits what servers can relay through your Postfix server. You will usually want to allow relaying from local clients and nothing else. Otherwise, spammers can use your mail server to relay messages. Here is an example of this:

```
mynetworks = 192.168.1.0/24, 127.0.0.0/8
```

If you define this parameter, it will override the mynetworks_style parameter. The mynetworks_style parameter allows you to specify any of the keywords class, subnet, or host. These settings tell the server to trust these networks to which the server belongs.