Even if you are serving only one domain with your mail server, it is a good idea to identify that domain in this file. When messages come to the server for the domains listed here, sendmail knows to try to deliver the messages locally. Sendmail interprets messages for domains not listed here as needing to be relayed.

> **NOTE:** If you want to off-load the processing of mail for a particular domain that is currently being directed to your sendmail server, you can use the `/etc/mail/mailertable` file. After setting up a DNS MX record to point to your sendmail server for this domain, and listing that domain name in the `mailertable` file, you can identify another computer that sendmail will forward all the traffic to for that domain. For example:
> 
> ```text
> example.com         smtp:mx1.linuxtoys.net
> ```
> 
> This example shows that all messages destined for example.com that are received by your sendmail server are forwarded to the server named mx1.linuxtoys.net. The `smtp` indicates that the server supports Simple Mail Transfer Protocol.

# ## Configuring virtual users

Incoming mail to your sendmail server will be directed to your machine with a request to deliver the message to a particular person at a particular domain name. For each domain that the sendmail server supports, you can identify how e-mail to mail recipients of that domain is treated.

With sendmail, you set up virtual user definitions in the `/etc/mail/virtusertable` file. Essentially, you are telling sendmail to redirect messages addressed to particular user names or domain names based on definitions you set up.

Configuring the `virtusertable` file is particularly important if your server is handling mail for multiple domains. That's because, by default, mail for the same user name (regardless of the domain name) will be stored in the same mailbox. For example, if your server handles mail for example.com and linuxtoys.net domains, mail for chris@example.com and chris@linuxtoys.net would all be directed to `/var/spool/mail/chris` mailbox. With the `virtusertable` file, you can change that behavior in a lot of ways.

The `virtusertable` file is empty by default. The following are some examples that illustrate how incoming messages can be directed in different ways based on virtusertable definitions.

| Left Column       | Right Column                        |
| :---------------- | :---------------------------------- |
| chris@linuxtoys.net | chris                          |
| cnegus@linuxtoys.net| chris                          |
| francois@linuxtoys.net| francois@spidmaker.com        |
| info@linuxtoys.net  | info-list                       |
| bogus@linuxtoys.net | error:nonuser No such user here |
| @example.net        | error:catchall                  |
| @example.com        | $1@linuxtoys.net                |