# Hacking Exposed Web Applications

![](bbox=[0.144, 0.115, 0.856, 0.555])

**Figure D-9.** A successfully loaded UrlScan ISAPI filter

> NOTE UrlScan priority can also be set with the AllowLateScanning setting in UrlScan.ini.

# Removing UrlScan

If you should ever need to disable/or remove UrlScan, you have a few options. If, after you install UrlScan, your application begins dropping certain client requests, you can set UrlScan into a logging-only mode that will permit all requests, but will log any requests that would normally reject. This could be helpful for troubleshooting. To set UrlScan in logging-only mode, add the value /* (slash-tilde-asterisk) to the RejectResponseUrl line in UrlScan.ini so that it looks like:

```
RejectResponseUrl=*
```

Then restart IIS to load the config. If you simply want to disable UrlScan, you can uninstall the ISAPI filter by reversing the steps discussed earlier in the section "Installing the UrlScan ISAPI Filter in IIS.\ Simply select the UrlScan filter on the ISAPI Filters tab and click Remove, then restart IIS.