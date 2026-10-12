Once you’ve installed a package such as MRTG (Multi-Router Traffic Grapher, available in Red Hat Linux 8.0) to monitor bandwidth, you will quickly get a criterion for what “normal” looks like on your site. A substantial drop or increase in utilization is something to investigate. Check your logs, and look for configuration files with odd or unusual entries.

# ## COPS

The COPS tool (Computer Oracle and Password System) provides a simple and automated way of checking for unusual settings in the system. Such checks include looking for SetUID programs in home directories, unusual permission settings on home directories, configuration files that expose your system to outside access without authorization, and so on.

One of the most significant features of COPS is that it is designed to be automatically run from a cron entry (see Module 8 for more about cron) every night. The report, if there is anything to report, is e-mailed to you.

You can research and download the latest and greatest version of COPS at ftp://ftp.cert.org/pub/tools.

# ## Tripwire

Tripwire, distributed as a standard Red Hat Linux 8.0 package, takes a very paranoid approach to security: If something changes, Tripwire tells you. This comprehensive protection removes the opportunity for someone to place a “backdoor” or “time bomb” in your system.

Tripwire generates MD5 checksums of every file on your system and saves them in an encrypted format. When you want to check on differences, you can recall the saved checksums and compare all of the files on the system to their known good MD5 checksum. Differences are reported.

The idea here is for you to perform an install and then ready a system for network deployment. But before actually putting the system onto the network, you run the Tripwire tool to generate and store all of the checksums. You can be confident that your list of MD5 checksums is safe in its encrypted domicile.

The process of setting up a Tripwire arrangement is time consuming. And if you use it on a system you’re fiddling with, you’ll get lots and lots of change notifications. However, short of cutting off network connectivity, it’s hard to tighten up a system any more than this.

# ## Nessus

Nessus is a very flexible security scanner with a modular architecture that helps it keep up with the latest threatening developments. While it’s not the final word in threat assessment (there isn’t one), it’s very capable and full-featured, with a variety of scanning and reporting options. See http://www.nessus.org for more information. You can also install Nessus via a