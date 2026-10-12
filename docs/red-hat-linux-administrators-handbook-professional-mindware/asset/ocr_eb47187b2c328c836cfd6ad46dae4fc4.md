This rule may cause some controversy among your users. By setting this rule, you deny all packets that are using the ICMP protocol, the protocol used by programs such as ping and traceroute. By denying this traffic, you can limit a popular denial-of-service attack called a *ping of death* in which a miscreant uses the ping program to send packets of an obscenely large size. A ping flood attack will not destroy any data but can be used to consume all of your bandwidth with the ping packets, thus allowing no room for legitimate traffic. By disallowing ICMP traffic, you are also restricting your local network from using tools such as ping or traceroute to check the status of machines beyond the firewall. It is a tradeoff that you have to decide on.

```
/sbin/ipchains -A input -j ACCEPT -p tcp -d 206.170.189.3 smtpp
```

This rule allows all traffic using the TCP protocol with a destination of 206.170.189.3 to travel to the SMTP port. In this example, 206.170.189.3 is your mail server, and you will allow any mail from the outside world to the mail server. You can also use the lines

```
/sbin/ipchains -A input -j ACCEPT -p tcp -d 206.170.189.5 www

/sbin/ipchains -A input -j ACCEPT -p tcp -d 206.170.189.9 domain
```

to allow access to your Web server (206.170.189.5) and your DNS server (206.170.189.9). This process can be continued ad infinitum for any number of hosts and services.

# Using an application-level firewall

Situations will arise in which you need the ability to control your network at the application level rather than at the network level. You may need to restrict your users from sending e-mail to certain addresses, monitor the Web sites your users are hitting, or get a good idea of the average size of files users are sending through the firewall. When you want this type of information and control, you require an application-level firewall.

Application-level firewalls, sometimes called *application proxies* or *proxy servers*, work in a manner different from that of packet filters. Application-level firewalls work without a direct connection between the local and remote