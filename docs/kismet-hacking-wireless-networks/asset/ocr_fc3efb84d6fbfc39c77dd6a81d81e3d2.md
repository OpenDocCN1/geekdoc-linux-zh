host system has to work harder to decrypt everything on the fly, and that the captured data will be in plaintext in the dump file. You want to keep access to it secure.

Hopefully you are not running WEP and are using something stronger like WPA. WEP can be cracked in less than *60* seconds using freely available tools. At this time, there is no way to decrypt a WPA network on the fly through Kismet.

```
# Is transmision of the keys to the client allowed? This may be a security
# risk for some. If you disable this, you will not be able to query keys from
# a client.
allowkeytransmit=true
```

Depending on your configuration and monitoring needs, you may not want the Kismet server to inform the Kismet client what the keys are. Change to `false` if you don’t want this, particularly if others can read the data from the server or the dump file.

```
# How often (in seconds) do we write all our data files (0 to disable)
writeinterval=300
```

By default, Kismet writes the logs to disk every 5 minutes (300 seconds). You can adjust this if you like, but as the size of the logs grow, the longer it takes to save them. If you specify a time too low, then it might cause your system to thrash its hard disk in a constant save cycle.

```
# How old (and inactive) does a network need to be before we expire it?
# This is really only good for limited ram environments where keeping a
# total log of all networks is problematic. This is in seconds, and should
# be set to a large value like 12 or 24 hours. This is intended for use
# on stationary systems like an IDS
# logexpiry=86400
```

In some situations you may want to have networks expire from the list. If you are running the server for several days and want to limit the amount of resources used, you can set the `logexpiry=` parameter to a reasonable expiry time. This is particularly of interest when used as an IDS and you want to automatically remove networks that haven’t been active for quite a while (such as clients passing by or way off nets that you might have gotten a lucky reflection and a single packet).

```
# Do we limit the number of networks we log? This is for low-ram situations
# when tracking everything could lead to the system falling down. This
# should be combined with a sane logexpiry value to flush out very old
# inactive networks. This is mainly for stationary systems like an IDS.
# limitnets=10000
```