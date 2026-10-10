+   • Do monitor the size of your log files. Apache’s `httpd-access.log` and `httpd-error.log` are notorious for eating up disk space if your Web server gets any kind of significant traffic. Use Apache’s built-in `rotatelogs` utility or run a cron job to flush the logs occasionaly. If your `/var` partition fills up, your mail, databases, and runtime files will not work.

Also, do be sure to *read* your logs! The system isn’t just writing out all that data for its health. Well, it is, actually, but it only works if you pay attention to what the system has to say.

+   • Do fly the Daemon banner proudly!

# DON’T:

+   • Don’t use experimental features on a production server. This isn’t the place to try out new ideas such as Soft Updates and unsupported filesystem kernel modules. Try these things out on a cheaply built “hobbyist” machine or a mirrored “backup” server; then put them into practice only once you’re comfortable with their use.

Beware, however, that if your test environment is not absolutely identical to your live machine, you run the risk of software failing in the production environment even if it worked on the test bed.

+   • Don’t port-scan your server if you’re running PortSentry or another tool that blocks your route to the machine when it detects an intrusion coming from your IP address. You’ll lose connectivity until you find an alternate direction from which to reach your server and delete the “blackhole” route.

Try to be aware of any action or situation that might block remote access to your machine. If that happens, you’ll require physical access to the machine in order to restore remote access.

+   • Don’t use `shutdown` to drop to single-user mode (for high-privilege activities such as replacing the kernel) if you’re running with the `securelevel` setting at 1 or higher. Using `shutdown` won’t decrement the kernel security level. Instead, reboot the machine and enter **boot -s** at the loader prompt to boot into single-user mode. Simply exit the single-user shell to come back up the rest of the way. You must boot in to and exit from single-user mode at the physical console!

+   • Don’t get hung up on uptime. If a system has 350-day uptime, this means the system has been sitting unused in a closet for a year or has not been conscientiously upgraded to keep up with security bulletins. Nonstop uptime doesn’t make for such great bragging rights as one might think.

+   • Don’t forget to add yourself to the “wheel” group at installation time! Very little is more disheartening than building a new server, driving 50 miles to the co-location