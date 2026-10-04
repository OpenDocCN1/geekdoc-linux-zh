# Attacking and Defending DNS • Chapter 8

LW ; expiry
1D ) ; minimum
CHAOS NS ; localhost.
version.bind. CHAOS TXT *Super Secure DNS version 0.31337 alpha*
authors.bind. CHAOS TXT *Kamadis Quintin Kaze

Specifically restrict and monitor as much as possible.The Secure Bind Template by Rob Thomas (www.cynru.com/Documents/secure-bind-template.html) is a good start. Check the cynru Web site for a regular basis for updates or changes. Of course, no guide should be blindly implemented. Understanding the settings and how it works a must.

The BIND configuration file follows a simple Unix configuration file syntax. Specific options are set and their associated parameters are set within parentheses. The following sections explain the security-related configurations, followed by code examples. Some syntax may be dropped or manipulated by documentation ease of use for Windows users. For easy-to-understand BIND configuration details, see www.nlias/reference/bind-doc/html/config.html.

# General BIND Options

The required configurations are included in the options field. The directory of files and common operational settings need to be specified. Remember to log both memory and general statistics for a baseline. When problems arise, a baseline will help in troubleshooting.

```
statistics-file "/bind_directory/named.stats"
memstats-file "/bind_directory/named.memstats"
dump-file "/var/adm/bind.dump"
zone-statistics yes;
```

There is a possibility of DoS attack via the DNS NOTIFY messages, therefore they should be turned off or limited to systems accessible only over a trusted medium (SSH tunnel):

notify no;
The Maximum transfer timeout for zone transfers should be set low:
max-transfer-time-in 60;

If BIND is running on an interface that is static, the dynamic interface option should be set to zero:
interface-interval 0;

![](bbox=[0.708, 0.943, 0.931, 0.966])