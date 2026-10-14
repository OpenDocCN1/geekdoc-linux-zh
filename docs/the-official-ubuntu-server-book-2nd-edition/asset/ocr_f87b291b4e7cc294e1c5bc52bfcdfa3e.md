# ufw Examples

The following is a list of start-to-finish ufw commands to set up a firewall for a particular service. I assume you are starting from the default state, that is, ufw is disabled. Also, I assume you will probably want to manage your server remotely with SSH even if it’s a Web, mail, or DNS server, so I add rules to enable SSH in each example.

# NOTE

**About Remote Firewall Management**
If this is the first time you have enabled ufw, and you plan to set this up remotely over the network, you should be careful about your steps. It’s very easy to make a mistake and lock yourself out. Specifically, when ufw is enabled, it flushes all connection data, so if you manage the server over SSH, your connection will be closed, and if you deny by default and haven’t set up an SSH rule yet, when ufw is enabled, you will be locked out. One simple safeguard you can put in place is a cron job that disables ufw every 15 minutes or so. That way, if you make a mistake and lock yourself out, you just have to wait at most 15 minutes for the firewall to be reset. To do this, add the following line to your /etc/crontab file:

```
*/15 * * * * root  ufw disable
```

Of course, the downside to this is that every 15 minutes while you are tweaking your firewall, ufw will be disabled and you will have to remember to enable it. Still, it’s better than being locked out of the system completely. Just remember to delete the crontab rule once you are finished tweaking. On Ubuntu 8.10 and later, ufw actually warns you if you enable ufw while using SSH and prompts you before it enables.

# SSH

I’m assuming you will probably want to have SSH enabled on just about any server you manage. Note the order in which I run the commands here, as I enable ufw at the very end. That way I don’t risk locking myself out because the SSH rule is defined before ufw is enabled:

```
$ sudo ufw allow ssh
$ sudo ufw default deny
$ sudo ufw enable
$ sudo ufw status
Status: active
```