UNIX, the hostname is tied into many services, including the Domain Name Service (DNS), Network Information Service (NIS), and Network Filesystem (NFS). Choose your hostnames wisely, as changing the hostname later can be a difficult and highly unrewarding exercise.

Choosing a hostname, and at a higher level a hostname scheme, can sometimes be as difficult as installing the system. You can choose a rigid scheme such as f2r3c5.yourdomain.com (for Floor 2, Room 3, and Cube 5), or something more fun such as animals.yourdomain.edu (and then choose the world's most obscure creatures). Be creative, but be consistent. Also try to choose hostnames that are easy to remember and spell. Nothing is more frustrating than attempting to telnet to an obscure server when you are blessed with poor spelling skills.

Your hostname will appear in a number of different places depending on your flavor of UNIX. In /etc/hosts, the hostname will appear on the line with the host IP address.

```
#
# Internet host table
#
127.0.0.1    localhost
10.1.1.15    mars.somedomain.com loghost
```

It is wise to always fully qualify your hostname. What this means is that your system knows itself as host.yourdomain.com, and not just a host, as we see from the output of the hostname command:

```
mars#hostname

mars.somedomain.com
```

This helps avoid confusion when your system is interacting with network services such as DNS, LDAP, and NFS. More confusion can arise when you have to manage systems in multiple domains that share resources. While fully qualifying your hostname may cause you a bit of extra effort if you move your system to a new domain or subnet, the problems you eliminate easily outweigh any extra work you may have to do down the line.