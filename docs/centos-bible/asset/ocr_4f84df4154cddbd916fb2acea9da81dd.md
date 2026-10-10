# Part IV Networking

+   - You don't want to be bothered clicking an extra icon when you just want to browse the Web a bit.

The risk of on-demand dialing is that dial-up connections can start up when you don't want them to because the connection starts automatically (some people get worried when their computer starts dialing by itself in the middle of the night).

Here is an example of settings you can add to your dial-up configuration file (/etc/sysconfig/network-scripts/ifcfg-xxx where xxx is replaced by your provider name) to configure on-demand dialing:

```
ONBOOT=yes
DEMAND=yes
IDLETIMEOUT=600
RETRYTIMEOUT=30
```

The ONBOOT=yes starts the pppd daemon but doesn't immediately begin dialing because DEMAND is set to yes. Also, because DEMAND=yes, a dial-up connection attempt is made any time traffic tries to use your dial-up connection. With IDLETIMEOUT set to 600, the connection is dropped after 600 seconds (10 minutes) with no traffic on the connection. With RETRYTIMEOUT set to 30, a dropped connection is retried after 30 seconds unless the connection was dropped by an idle timeout, in which case there is no retry. You can change the time-out values as it suits you.

> **NOTE** Because it can take time for dial-up connections to be established, operations may fail while dialing occurs. In particular, DNS requests can time out in 30 seconds, which may not be long enough to establish a dial-up connection. If you have three DNS servers configured for each client, you have a 90-second time-out period. As a result, the modem connection may be running before the request fails.

# Checking Your PPP Connection

To debug your PPP connection or simply to better understand how it works, you can run through the steps below. They will help you understand where information is being stored and how tools can be used to track this information.

# Checking That Your Modem Was Detected

It is possible that your modem is not supported under Linux. If that is the case, your PPP connection might be failing because the modem was not detected at all. To scan your serial ports to see where your modem might be, type the following as *root*:

```
$ wdialconf /etc/wdial.conf.new
```

The wdialconf command is really made to build a configuration file (/etc/wdial.conf) that is used by the dialer command (wdial). If it succeeds, you can copy the wdial.conf.new file to the /etc/wdial.conf. Its first action, however, is to scan the serial ports on your computer and