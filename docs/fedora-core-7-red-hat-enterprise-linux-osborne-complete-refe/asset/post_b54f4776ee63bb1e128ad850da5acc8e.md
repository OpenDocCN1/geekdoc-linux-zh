
The local macro and configuration option definitions that affect a particular feature need to be entered before the **FEATURE** entry. For example, the **redirect** feature uses the aliases file. Any local definition of the aliases file needs to be entered before the **redirect** feature.

```
define('ALIAS_FILE', '/etc/aliases')
FEATURE(redirect)
```

You need to be careful how you enter comments into a **sendmail.mc** file. This file is read as a stream of macros, ignoring all white spaces, including newlines. No special comment characters are looked for. Instead, you have to simulate comment indicators using the **dnl** or **divert** commands. The **dnl** command instructs that all characters following that **dnl** command up to and including the next newline are to be ignored. If you place a **dnl** command at the beginning of a text line in the **sendmail.mc** file, it has the effect of turning that line into a comment, ignoring everything on that line—including its newline. Even empty lines will require a **dnl** entry to ignore the newline character:

```
dnl you will have to /etc/mail/sendmail.cf by running this the m4
dnl macro config through preprocessor:
dnl
```

Alternatively, you can use the **divert** command. The **divert** command will ignore all data until another **divert** command is reached:

```
divert(-1)
This is the macro config file used to generate
the /etc/mail/sendmail.cf file. If you modify the file regenerate
you will have to regenerate /etc/mail/sendmail.cf by running the m4
macro
divert(0)
```

For Sendmail to work at all, it requires only that the **OSTYPE** and **MAILERS** macros be defined, along with any needed features and options. A very simple Sendmail file is shown here:

```
mysendmail.mc
dnl My sendmail.mc file
OSTYPE(`linux')
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
FEATURE(redirect)
MAILER(procmail)
MAILER(smtp)
```

A **sendmail.mc** file usually contains many more entries, particularly for parameters and features. Check the /etc/mail/sendmail.mc file on your Red Hat or Fedora system to see the standard default entries for Sendmail.

## Sendmail Masquerading

For a mail server that is relaying messages from local hosts to the Internet, you may want to masquerade the source of the messages. In large networks that have their own mail servers connected to the Internet, Sendmail masquerading can make messages sent by local hosts appear to be sent by the mail server. Their host address will be replaced by the mail server’s address. Returned mail can then be sent to the mail server and held in POP or IMAP server mailboxes that can be accessed later by users on the local hosts. Also, entries in the server’s virtual user table could forward mail to corresponding users in local hosts.

Masquerading is often used to mask local hosts with a domain name. Any subdomains can also be masqueraded. This method can be applied to situations where an ISP or your network administrator has assigned your network its own domain name. You can then mask all mail messages as coming from your domain name instead of from particular hosts or from any subdomains you may have. For example, if a network’s official domain name is mytrek.com, all messages from the hosts in the mytrek.com network, such as rabbit.mytrek.com and turtle.mytrek.com, could be masqueraded to appear as just coming from mytrek.com. Should the mytrek.com network have a subnetwork whose domain is mybeach.com, any messages from mybeach.com could also be masqueraded as coming from mytrek.com.

Masquerading is turned on with the MASQUERADE_AS command. This takes as its argument the name you want to masquerade your mail as. Normally, the name used is just the domain name, without the mail host. In the following example, the mail is masqueraded as simply mytrek.com. Mail sent from a local host like turtle.mytrek.com will appear to be sent by just mytrek.com:

```
MASQUERADE_AS( 'mytrek.com' )dnl
```

You will also have to specify the hosts and domains on your local network that your Sendmail server should masquerade. If you have decided to masquerade all the hosts in your local network, you just need to set the masquerade_entire_domain feature, as in

```
FEATURE( 'masquerade_entire_domain' )dnl
```

If, instead, you want to masquerade particular hosts or your domain has several subdomains that you want masqueraded, you list them in the MASQUERADE_DOMAIN entry. You can list either particular hosts or entire domains. For example, given a local network with the local hosts turtle.mytrek.com and rabbit.mytrek.com, you can list them with the MASQUERADE_DOMAIN to have them masqueraded. The domain they are masqueraded as is specified in the MASQUERADE_AS entry.

```
MASQUERADE_DOMAIN( 'turtle.mytrek.com rabbit.mytrek.com' )dnl
```

If you want to masquerade all the hosts in your local network, you can simply list your local network’s domain name. If your local network also supports several subdomains, you can list those as well to masquerade them. For example, to masquerade all the hosts in the mybeach.com domain, you would use the following entry:

```
MASQUERADE_DOMAIN( 'mytrek.com mybeach.com' )dnl
```

If you have a long list of domains or hosts, or if you want to be able to easily change those that should be masqueraded, you can place them in a file to be read by Sendmail. Specify the file with the MASQUERADE_DOMAIN_FILE command:

```
MASQUERADE_DOMAIN_FILE( 'mydomains' )dnl
```

If you just want to masquerade all the hosts in your local domain, you use the **masquerade_entire_domain** feature:

```
FEATURE (masquerade_entire_domain)dnl
```

A common configuration for a local network would specify the domain name in the **MASQUERADE_AS** entry and in the **MASQUERADE_DOMAIN** entry. Using the example **myisp.com** for the domain, the entries would look like this:

```
MASQUERADE_AS ('mytrek.com')dnl
FEATURE (masquerade_entire_domain)dnl
```

If you wanted to masquerade as an ISP’s mail domain, you would use the ISP’s domain in the **MASQUERADE_AS** entry as shown here:

```
MASQUERADE_AS ('myisp.com')dnl
MASQUERADE_DOMAIN ('mytrek.com')dnl
```

When mail is received from the outside bearing just the address **mytrek.com**, your network needs to know what host to send it to. This is the host designated as the mail server for the **mytrek.com** network. This information is provided by a mail exchange record (MX) in your DNS configuration that will specify that mail sent to **mytrek.com** will be handled by the mail server—in this case, **turtle.mytrek.com**:

```
mytrek.com.   IN     MX      0       turtle.mytrek.com.
```

You further have to be sure that MX relaying is enabled with the **relay_based_on_MX** feature:

```
FEATURE (relay_based_on_MX)dnl
```

All messages will appear to originate from the mail server’s host. For example, if your Sendmail mail server is running on **turtle.mytrek.com**, mail sent from a local host called **rabbit.mytrek.com** will appear to have been sent from **turtle.mytrek.com**.

You can also masquerade recipient addresses, so that mail sent to users on your local host will be sent instead to the masqueraded address. Use the **allmasquerade** feature to enable recipient masquerading:

```
FEATURE (allmasquerade)dnl
```

## Configuring Mail Servers and Mail Clients

Sendmail can be used either as a mail server, handling mail for various hosts on a network, or as a mail client, managing mail for local users on a particular host. In a simple network configuration, you would have each host running Sendmail in a client configuration, and one host operating as a mail server, relaying mail for the network hosts. For a local network connected to the Internet, your local hosts would run Sendmail in a client configuration, and your gateway would run Sendmail in a server configuration (though the mail server would not have to necessarily run on the gateway). The mail server would relay messages from the local network hosts out to the Internet. The mail server could also be used to block
