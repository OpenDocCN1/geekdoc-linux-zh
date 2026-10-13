Note that the rules are read in sequential order. In other words, the first rule the firewall comes to that matches the traffic being sent or received is the one that will be applied. If this seems confusing, the following rule set might clear things up:

```
add deny all from any to any
add allow tcp from any to www.simba.org 80
add allow all from lion.simba.org to www.simba.org
```

Even though the same rules are present in this set that were present in the previous one, the results of this rule set will be very different from the intended results for it. This is because the first rule will match all traffic; therefore, the next two rules will be ignored and the first rule will be applied. Of course, this means that because the first rule applies to all traffic (which includes lion.simba.org), the traffic will be denied—even though the second two rules allow it. As you can see, it is very important in which order you list the rules in the set.

The first rule set that was given previously is an example of the "deny everything that is not specifically allowed" strategy. The following gives an example of how the "allow everything that is not specifically denied" strategy would work.

```
add deny all from nasty.hacker.org to any
add deny all from any to www.simba.org 80
add 65000 allow all from any to any
```

In this case, everything is allowed except for traffic that comes from nasty.hacker.org, which is denied access to all systems that are behind this firewall. In addition, all traffic from any system is denied to www.simba.org if it is directed toward port 80. (Port 80 is normally where a Web server could be running. In other words, this rule would have the effect of blocking any attempts to access the Web server port.)

![](bbox=[0.2, 0.8, 0.28, 0.9])

> It is a good idea to set your firewall rule file so that it can only be accessed by the root user. There is a small security risk involved in letting other users know what firewall rules your system is using. For example, if a hacker can obtain an IP address that your firewall allows to access the network, he can potentially spoof the IP address and thus fool your firewall into thinking that the traffic is coming from an authorized system when, in fact, it is not.

# Enabling the Firewall

After you have saved the firewall configuration file, you need to configure the /etc/rc.conf file to enable it. This can be done by adding the following two lines: