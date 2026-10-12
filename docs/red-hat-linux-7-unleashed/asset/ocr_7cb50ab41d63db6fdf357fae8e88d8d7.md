# The H Operator: Header Definitions

You probably won’t want to change the header definitions given in the V.8 sendmail configuration files because they already follow accepted standards. Here are some sample headers:

+   H?D?Date: $a  
+   H?F?Recent-From: $q  
+   H?F?From: $q  
+   H?x?Full-Name: $x

Note that header definitions can use macros, which are expanded when inserted into a letter. For example, the $x macro used in the preceding Full-Name: header definition expands to the full name of the sender.

The optional ?mailerflag? construct tells sendmail to insert a header only if the chosen mailer has that mailer flag set (see “The M Operator: Mailer Definitions” later in this chapter).

Suppose the definition of your local mailer has a flag Q, and sendmail selects that mailer to deliver a letter. If your configuration file contains a header definition like the following one, sendmail inserts that header into letters delivered through the local mailer, substituting the value of the macro $F:

```
H?Q?X-Fruit-of-the-day: $F
```

Why would you use the ?mailerflag? feature? Different protocols can require different mail headers. Because they also need different mailers, you can define appropriate mailer flags for each in the mailer definition and use the ?mailerflag? construct in the header definition to tell sendmail whether to insert the header.

# The O Operator: Setting Options

sendmail has many options that change its operation or tell it the location of files it uses. Most of them can be given either on the command line or in the configuration file. For example, you can specify the location of the aliases file in either place. To specify the aliases file on the command line, you use the -oA option:

```
$ /usr/sbin/sendmail -oA/etc/aliases [other arguments...]
```

To do the same thing in the configuration file, you include a line like this:

```
OA/etc/aliases
```

Either use is equivalent, but options such as the location of the aliases file rarely change, and most people set them in sendmail.cf. The V.8 sendmail options are fully described in the SiOG.

![](bbox=[0.9, 0.72, 0.97, 0.95])