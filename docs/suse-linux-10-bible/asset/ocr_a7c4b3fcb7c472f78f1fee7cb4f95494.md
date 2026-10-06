# Chapter 17 ♦ Mail Servers – Postfix, Sendmail, Qpopper, and Cyrus 475

+   ♦ To allow relays from machines that are in myynetworks

+   ♦ To deny all relays using the reject_unauth_destination (reject all unauthorized connections) clause

![](bbox=[0.131, 0.198, 0.193, 0.246])

Be careful with what you put into the myynetworks clause because this is the easiest way to configure Postfix as an open relay. We pointed out the DMZ issue so you can understand that if you think locally the configuration is secure, as soon as you add the Internet to that equation, it can get a lot more difficult to see the picture.

Postfix also allows relays to any domains listed in relay_domains. This parameter by default contains whatever is in $mydomain parameter, which by default is your machine's domain. If you use the default setting, any untrusted sender (in myynetworks) can relay mail through Postfix to any user at $mydomain. It should be obvious why this is the default, as this would mean that Postfix would accept mail for the domain it is hosting.

# Virtual Domains

Another parameter that is very useful is mydestination. In a real world example, we host our domain, pacemaker.net, and also the domain planetsme.org. Even though by default Postfix installation configures itself to accept mail for the pacemaker.net, we need to tell it it should accept mail for the planetsme.org domain (if we don't, it will be rejected). To do this, we have updated mydestination clause.

```
mydestination = pacemaker.net, planetsme.org
```

In this example, we are creating a virtual domain—that is, a domain that physically (in terms of our server's configuration) does not exist, but we are hosting in the same realm as pacemaker.net (our physical server domain).

Our list on in is just, and it exists as a real user. Any mail for just@pacemaker.net is delivered to Justin's mailbox, and with the mydestination clause, any mail for planetsme.org is delivered to the same mailbox.

This works because Postfix believes it is the final destination for pacemaker.net and planetsme.org. When the mail has gone through the mail system, Postfix will decide that the user just does exist and will deliver any mail on any domain that is listed in destination to just.

This type of virtual domain is called a sendvirtual domain because it makes no distinction between one user and another regardless of the destination domain listed in the mydestination clause.

If you want to make that distinction, you use a Postfix-style virtual domain that correlates the fact that a user and domain make up a unique order on the system.