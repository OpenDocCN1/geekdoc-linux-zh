These log entries show a complete zone transfer process that was successful; however, you might see a log entry like the following:

```
Mar 27 21:58:45 ns2 named[22774]: zone example.net/IN/external: refused notify from no\n-master: 10.1.1.7#36515
```

Here the slave received a notify from a server (in this case 10.1.1.7) that it does not have configured as its master, so it rejected it. In this case, if the IP is a valid IP for the master, you will need to look into your BIND configuration for this zone on this slave and make sure that it is configured as a slave and that the IP of the master is configured as one of the master IPs.

You might, on the other hand, see a log entry like the following:

```
Mar 27 22:09:00 ns2 named[22774]: client 10.1.1.3#42895: view external: received notify for \n-zone 'example.net'
Mar 27 22:09:00 ns2 named[22774]: zone example.net/IN/external: notify from 10.1.1.3#42895: \n-zone is up to date
```

In this case the notification was sent to the slave; however, the serial number was not larger than the serial number on the slave, so it didn't bother updating. An administrator might accidentally set a very high serial number on the master (like using the date as a serial number but accidentally setting the year wrong) but doesn't realize it and sends out an update. Then when the next administrator comes around, they fix the error by setting the serial number to the current date again, but the slaves refuse to accept the update. When this happens, the fix is to log in to the slave and view the local cached zone files it has for that zone. Where it stores these files is something that is configured in BIND, but common locations include the /var/cache/ bind, /etc/bind, and /var/lib/bind directories. When you open this file you should see all of the records for your zone much like they are configured in the master, and at the top of the file you can see what the serial number is set to. If the serial number is too high, the easiest solution is to simply delete or move this file, then restart BIND on the slave. The BIND service should then request a zone transfer from the master and get up to date.