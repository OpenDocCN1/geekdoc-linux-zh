# LISTING 5.9 ntp.conf Using Keys (Client)

```
enable auth
keys /etc/ntp.keys
broadcastclient key 5
```

It is possible to use these keys for the queries as well, if you need to make sure your systems know to whom they are talking. You have to change the client entry as shown in Listing 5.10 to make use of the facility.

# LISTING 5.10 Query Using Keys

```
enable auth
keys /etc/ntp.keys
trustedkey 10
server address.of.your.internal.time-server key 10
```

You can achieve a lot more by using ntp, but the information presented so far should be sufficient to set up a basic network of servers and clients.

# 5.2 HOW TO READY A SYSTEM FOR PRODUCTION

Installing a system and getting it ready for production are two sides of the same coin. Installing a system is step one. Step two, equally important—some say even more important—is to modify the system until all requirements regarding the network it is connected to and the other systems in it are fulfilled. The PATH needs to be configured to match the approved standards in your infrastructure, catering for additional software that is installed on the new machine. syslog needs to know what to report and to do so in a way consistent with the rest of your systems. Important files like /etc/hosts should contain all the necessary entries to make the new system a well-behaved citizen in the LAN. If all these steps are completed and tested, you should still take a look at Chapter 7 on security before releasing the system in the wild.

Another aspect worthy of reevaluation comprises the running services on the new system. Are there active services not needed for the intended use of the system? Does a file server really need a running Web server or an active mail server process? Many services that are not necessary for the purpose of the system can be turned off during the installation or were not installed in the first place. Sometimes one or two of them sneak back on the system; getting rid of unwanted services depends heavily on the manufacturer of the operating system. It never hurts to check again, just to ensure that only needed services are running on a production system.