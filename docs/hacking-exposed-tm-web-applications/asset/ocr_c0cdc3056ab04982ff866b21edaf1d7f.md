# UPDATING WINDOWS FAMILY PRODUCTS

Neither the IISdown tool nor UrlScan requires that the latest Windows family product Service Packs and Hotfixes are installed. You must make sure of this on your own!

# hfnetchk

The best way to check if your Windows systems have the most up-to-date patches is to use a tool such as the Network Hotfix Checker (hfnetchk), available free from Microsoft (see the "References and Further Reading" section in this chapter for links). hfnetchk currently verifies the most recent patches for the following Windows products are installed:

+   - Windows NT4, Windows 2000, and XP

+   - IIS

+   - SQL

+   - Internet Explorer (IE)

To run hfnetchk, you must be initially connected to the Internet in order to obtain the list of current patches from Microsoft.com. Once the XML list is downloaded (it's called mssecure), you can then use it to determine which machines on a given network have the latest patches installed. In order to scan a machine, you must have administrative privileges on that system. The output of hfnetchk looks like this:

```
Scanning WEBSRV01

Done scanning WEBSRV01

WEBSRV01 (192.168.234.32)
```

| Note | MS01-022 | Q296441 |
| Patch NOT Found MS02-001 | Q311401 |
| Patch NOT Found MS02-006 | Q314147 |
| Patch NOT Found MS02-008 | Q318202 |
| Patch NOT Found MS02-008 | Q318203 |
| Patch NOT Found MS02-013 | Q300845 |
| Patch NOT Found MS02-014 | Q313829 |
| Patch NOT Found MS02-017 | Q311967 |