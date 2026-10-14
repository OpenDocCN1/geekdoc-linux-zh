
A good example of why you might want to limit based on IP address is an intranet site, like an internal wiki. If you use a wiki for your internal documentation, you probably don’t want the entire world to read it. You might even host a wiki just for a particular group of users and want to restrict access so that only their network can see it. When you define more advanced ufw rules, you must use the extended ufw syntax. This syntax requires you to specify the protocol and port number explicitly, so you can’t use the same shortcuts as in the simpler commands. Here’s an example command to limit Web access (port 80) to just the 10.1.1.0 network:

```
$ sudo ufw allow proto tcp from 10.1.1.0/24 to any port 80
```

Let’s break this command down. The proto tcp section defines whether this rule applies to TCP or UDP. I limit what networks this rule applies to with from 10.1.1.0/24. The to any port 80 section of the command says that this rule applies to port 80 on any destination address on the machine.

Even if you deny by default, there might be circumstances when you also add a deny rule. For instance, let’s say that you are running an external SMTP (mail) server and you notice that a host inside your network at 10.1.1.75 appears to be infected with a virus and is flooding your mail server with invalid messages. To block just that IP address, you would type

```
$ sudo ufw deny proto tcp from 10.1.1.75 to any port 25
```

If you wanted to block all packets from that host, not just SMTP, you wouldn’t need to define the proto or to arguments:

```
$ sudo ufw deny from 10.1.1.75
```

Later on, once the virus has been removed and the host is back to normal, you can remove the rule with

```
$ sudo ufw delete deny proto tcp from 10.1.1.75 to any port 25
```

or, if you dropped all packets from the host, this command would remove it:

```
$ sudo ufw delete deny from 10.1.1.75
```

## ufw Examples

The following is a list of start-to-finish ufw commands to set up a firewall for a particular service. I assume you are starting from the default state, that is, ufw is disabled. Also, I assume you will probably want to manage your server remotely with SSH even if it’s a Web, mail, or DNS server, so I add rules to enable SSH in each example.

### NOTE

**About Remote Firewall Management**

If this is the first time you have enabled ufw, and you plan to set this up remotely over the network, you should be careful about your steps. It’s very easy to make a mistake and lock yourself out. Specifically, when ufw is enabled, it flushes all connection data, so if you manage the server over SSH, your connection will be closed, and if you deny by default and haven’t set up an SSH rule yet, when ufw is enabled, you will be locked out. One simple safeguard you can put in place is a cron job that disables ufw every 15 minutes or so. That way, if you make a mistake and lock yourself out, you just have to wait at most 15 minutes for the firewall to be reset. To do this, add the following line to your /etc/crontab file:

```
*/15 * * * * root  ufw disable
```

Of course, the downside to this is that every 15 minutes while you are tweaking your firewall, ufw will be disabled and you will have to remember to enable it. Still, it’s better than being locked out of the system completely. Just remember to delete the crontab rule once you are finished tweaking. On Ubuntu 8.10 and later, ufw actually warns you if you enable ufw while using SSH and prompts you before it enables.

### SSH

I’m assuming you will probably want to have SSH enabled on just about any server you manage. Note the order in which I run the commands here, as I enable ufw at the very end. That way I don’t risk locking myself out because the SSH rule is defined before ufw is enabled:

```
$ sudo ufw allow ssh
$ sudo ufw default deny
$ sudo ufw enable
$ sudo ufw status
Status: active
```

| To | Action | From |
|---|---|---|
| 22 | ALLOW | Anywhere |

### DNS

```
$ sudo ufw allow ssh
$ sudo ufw allow domain
$ sudo ufw default deny
$ sudo ufw enable
$ sudo ufw status
Status: active
```

| To | Action | From |
|---|---|---|
| 22 | ALLOW | Anywhere |
| 53 | ALLOW | Anywhere |

### Web

Here I open up ports for both HTTP (80) and HTTPS (443), but if you don’t use HTTPS, you can remove that particular rule from the list:

```
$ sudo ufw allow ssh
$ sudo ufw allow www
$ sudo ufw allow https
$ sudo ufw default deny
$ sudo ufw enable
$ sudo ufw status
Status: active
```

| To | Action | From |
|---|---|---|
| 22 | ALLOW | Anywhere |
| 80 | ALLOW | Anywhere |
| 443 | ALLOW | Anywhere |

### SMTP

```
$ sudo ufw allow ssh
$ sudo ufw allow smtp
$ sudo ufw default deny
$ sudo ufw enable
$ sudo ufw status
Status: active
```

| To | Action | From |
|---|---|---|
| 22 | ALLOW | Anywhere |
| 25/tcp | ALLOW | Anywhere |
