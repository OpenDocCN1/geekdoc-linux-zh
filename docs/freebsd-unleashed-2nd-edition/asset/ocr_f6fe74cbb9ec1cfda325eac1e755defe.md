another server in the same network), which tells all the machines within that network that your SMTP server (S1) is a legitimate mail exchanger for them.

Sendmail, in its default configuration on FreeBSD, will accept mail from senders whose MX record points to S1, defining it as the MTA for the network. This prevents people from outside the network from using S1 as a relay; if they try, they'll get their messages bounced back with a **Relaying denied** error.

![](bbox=[0.14, 0.24, 0.87, 0.42])

# Configuring S1 to Allow Users to Relay

This configuration is great for ISPs or enterprise networks that have a fully defined network, DNS entries for all the hosts in that network, and a proper MX record pointing to the relaying SMTP server. But what about standalone Internet hosts, which might have users all over the world trying to use their Sendmail servers to transmit mail? Each of these users, when trying to send a message through S1, from wherever they happen to be, will get a **Relaying denied** error back.

To avoid this problem, you can specifically configure S1 to allow these users to relay. There are a number of ways to do this, many of which are extremely inadvisable in some situations:

+   - Add “trusted” sender domains to the file `/etc/mail/relay-domains`, which doesn’t exist in the default installation. Any host within a listed domain will be permitted to relay through your server. You have to restart Sendmail after modifying this file. This is easy and effective, but as soon as you add a large, popular domain to this file that might contain spammers as well as legitimate senders, its benefit is lost.

Add domains to this file one per line, as with `/etc/mail/local-host-names` (which you saw earlier in this chapter):

```
```
# cat /etc/mail/relay-domains
good.host.com
23.144.12.115
```
```





![](bbox=[0.94, 0.34, 0.97, 0.38])