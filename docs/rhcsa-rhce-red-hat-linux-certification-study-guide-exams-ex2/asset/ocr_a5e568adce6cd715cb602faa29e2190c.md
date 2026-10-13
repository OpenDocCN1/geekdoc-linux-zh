The directive that follows allows authentication from nonstandard clients such as Microsoft Outlook Express:

```
broken_sasl_auth_clients = yes
```

This allows authenticated users, allows access from networks configured with the mynetworks directive, and rejects destinations other than the Postfix server:

```
smtpd_recipient_restrictions = permit_sasl_authenticated,
permit_mynetworks, reject_unauth_destination
```

# Configure Incoming E-Mail

The directives required to set up Postfix to accept incoming e-mail from other system have been previously described in the description of the main.cf file. But that was a more comprehensive description of that file. This section just covers the minimum requirements to configure Postfix, in the words of the RHCE objectives, "to accept inbound e-mail from other systems." Given a Postfix server configured on the server1.example.com system, on the 192.168.122.0/24 network, you'd make the following changes to the main.cf file in the /etc/postfix directory:

```
myhostname = server1.example.com
mydomain = example.com
myorigin = mydomain
inet_interfaces = all
mynetworks = 192.168.122.0/24, 127.0.0.0/8
```

Each of these options replaces either a comment or an active directive in the default /etc/postfix/main.cf file. For example, you should at least comment out the following directive:

```
#inet_interfaces = localhost
```

# Configure a Relay Through a Smart Host

A smart host has all of the functionality of a regular SMTP server, except for the forwarding of all e-mail through a second SMTP server. The location of the smart host can be specified with the relayhost directive. For example, if the remote smart host is outsider1.example.org, you'd add the following directive to the /etc/postfix/main.cf file:

```
relayhost = outsider1.example.org
```