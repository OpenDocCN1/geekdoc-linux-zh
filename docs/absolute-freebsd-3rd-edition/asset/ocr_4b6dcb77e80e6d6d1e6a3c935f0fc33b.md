settings appear to match, reboot the BMC. Once it works, you can use SOL from another host.

The standard IPMI SOL client is IPMItool (https://sourceforge.net/projects/ipmitool/), available as the ipmitool package. (Chapter 15 discusses packages.) IPMItool can interact with your BMC over the network, granting you all of the BMC functions without logging into a clunky web interface. You can reboot the host, check hardware alarms and sensors, and more, all from the command line. But for the moment, we’ll stick with the SOL console. Use the BMC’s hostname or IP, the username, and the password to log into SOL.

```
# ipmitool -H bmc -U username -I lanplus sol activate
```

Here, I log into my web server’s BMC, with the hostname www-bmc, using the username “bert.”

```
# ipmitool -H www-kvm -U bert -I lanplus sol activate
```

Enter the password at the prompt, and the SOL will acknowledge your login.

```
[SOL Session operational.  Use ~? for help]
```

We have a console. Probably. Let’s do the final test.

# Working at the Console

The real test of a serial console is whether or not you can get data across it. Once you have your console connected, hit ENTER.

```
FreeBSD/amd64 (www) (ttyu2)
login:
```

FreeBSD permits logins on serial consoles by default. Log in to the host and reboot it, and you’ll get the usual console messages.

```
Jul 13 11:48:24 Stopping cron.
Stopping sshd.
```