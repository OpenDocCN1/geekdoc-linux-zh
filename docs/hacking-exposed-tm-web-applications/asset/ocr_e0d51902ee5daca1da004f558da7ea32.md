# Hacking Exposed Web Applications

To restart IIS on Windows 2000, open a command prompt and type IISreset. On Windows NT, to restart the World Web service, type net stop w3svc and net start w3svc.

To update UrlScan to the most recent version (2.5 of this writing), run the UrlScan executable that you downloaded according to the steps in the section entitled “Updating UrlScan” earlier in this chapter. This updates the UrlScan code to the most recent version, makes a few modifications to the UrlScan configuration file, and resets the IIS service. When it finishes, see the following screen:

![](bbox=[0.363, 0.273, 0.636, 0.375])

With IISLockdown and UrlScan in operation, the behavior of your Web server is now drastically altered, depending on what template or other options you selected during the IISLockdown wizard. You may be disconcert to see “Object disabled” in your browser when you attempt to connect to your newly secured server—remember, if you selected the Static Web Server template, or manually disabled the ASP script mapping, the server will no longer serve ASP scripts, which are the default content provided with IIS.

What are your next steps? If you need to roll back IISLockdown for some reason, read the next section. If you need to tune your UrlScan configuration more specifically, move on to the section “Advanced UrlScan Deployment” later in this chapter. Otherwise, congratulations—your server is now protected by UrlScan 2.5!

# Rolling Back IISLockdown

OK, something went wrong, and now your Web server is completely broken after you ran IISLockdown on it. How can you reverse the effects of IISLockdown?

Simple—rerun iislock.exe. The first time it runs, IISLockdown keeps a log of all the configurations it makes in the file %windir%\system2\inetrs\oblt-log.log. As long as this file is not removed or altered, when you rerun iislock.exe, it will present the screen shown in Figure D-6.