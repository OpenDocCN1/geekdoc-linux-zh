After your system has rebooted, ensure that the new versions of /srv and /home reflect the new configuration. Because they are now mount points instead of traditional subdirectories of /, a df command should show a value for the amount of available disk space for each mount point. An additional quick check would be to test services that depend on the contents that were migrated:

```
```text
Athena:/ # df -h
Filesystem              Size  Used Avail Use% Mounted on
/dev/sda1               9.4G  2.2G  6.8G  25% /
tmpfs                   93.0K  0.0K   93M   1% /dev/shm
/dev/sdb1                20G   34M   19G   1% /home
/dev/sdb2                20G   34M   19G   1% /srv
```
```

In one of the preceding steps, you removed the network cables from the server. In some instances, the network environment will not initialize properly without live network cables connected to each NIC. To test, you may need to connect to a test network or simply to a laptop with a crossover cable. This should provide the appropriate signals for the card to initialize properly. You may have to restart the network services before continuing with testing. You accomplish this by rebooting the server or, more gently, by issuing the following command.

```
```text
Athena:/ # /etc/init.d/network restart
```
```

In the case of Athena being a web server, checking the default server web page as well as accessing a few user public_html directories should suffice. This would verify that the Apache service found both environments and that the permissions associated with the locations are correct. Secondary checks should include testing the users’ publishing access to the server through FTP or Samba shares. At this point, you can place the machine back in service. Users should be able to connect to their environment, and all service should be running.

# Changing Network Configuration

There are several reasons why you might need to change the network configuration of your server. Your company has changed ISPs, and the server is moving from your intranet to the Internet are possible scenarios.

One of the more frequent reasons is that you have built your server in a test environment behind a firewall. Servers are typically built from original distribution CDs that, over time, become outdated. This has the drawback of generating a first cut of the machine that could present several critical vulnerabilities to the network.