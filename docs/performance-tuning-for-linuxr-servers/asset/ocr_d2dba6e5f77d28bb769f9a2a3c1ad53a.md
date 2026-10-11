The number 1 turns `using_dma` on; the number 0 turns `using_dma` off.

None of these settings is saved over a reboot. You have to add the appropriate commands to your /etc/rc.d/rc.sysinit file if you are using Red Hat to be sure they are run automatically on startup. If you are not running a Red Hat distribution, an easy way to find the file to change is to do a grep in the /etc directory, as shown in the following example:

```
# cd /etc
# grep -r hdparm . | more
```

After you find the configuration file that sets the options through hdparm, change that file to use the new parameters that were set with hdparm.

It is a good idea to run with the new settings for a while to ensure they are right for the system before they are permanently updated in a configuration file.