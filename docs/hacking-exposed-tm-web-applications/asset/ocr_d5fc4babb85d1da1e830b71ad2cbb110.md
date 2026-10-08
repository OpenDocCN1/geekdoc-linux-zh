# Hacking Exposed Web Applications

If you are deploying UrlScan to any of the Microsoft product types identified in the previous list (for example, Commerce Server), use that template file. For maximum security, we recommend the urlscan_static.ini file. If you require dynamic content generation by scripts (as Active Server Page scripts), use the urlscan_dynamic.ini file. Don't sweat this thing too much—you can edit this file at any time.

Whichever file you choose, copy it to the directory where you installed UrlScan.dll. Then rename it to UrlScan.ini.

Now you have to edit it so that UrlScan.dll rejects the requests you want it to. The syntax for UrlScan is pretty straightforward, and we've included a complete command reference in the section titled "UrlScan Command Reference" later in this chapter. If you've chosen your template well, you'll only need to make configuration changes at this point. However, there are a few edits that we recommend you perform right away.

# Specify AlternateServerName

First, as we've noted before, you should specify an alternate server name by editing or creating a line that:

```
AlternateServerName=Webserver 1.0
```

You can select any non-IIS server name

# Add Updates

Next, we recommend making the appropriate changes to update your UrlScan.ini to version 2.5. Remember, there are two version 2.5 configurations, Baseline and SRP. The differences are minimal, and we'll note them next. We favor the SRP settings, as they are more restrictive security-wise. To your UrlScan, add the following lines to the end:

```
[RequestLimits]
MaxAllowedContentLength=30,000,000 ;30MB
ForBaseline, set previous to 2,000,000,000
MaxUrl=16384 ;16K
MaxQueryString=4096 ;4K
```

The next addition is optional, but recommended. It protects IIS servers from exploits of a serious buffer overflow announced in April 2002, and this added setting is the main