# 3.4.1.8 Allowing Controlled Uploading.

Allowing public anonymous uploading generally is a bad idea. When allowed, crackers and other undesirables discover this quickly and use your site for their evil purposes. This will usually be to crack systems, pornography (no doubt different from any that you might be interested in), and other things that you do not want on your system. If you choose not to allow uploading, simply have the directories 755 (or 555) and owned by ftpdadmin. Then, the ftp user, known as anonymous, will be prevented from uploading any pages.

If you choose to have an unrestricted upload facility, the convention is to have ~ftp/incoming directory for this purpose and for it to be owned by ftpdadmin. For full access it should be mode 777 but this is not recommended if the system is accessible from the Internet, possibly, the directory is checked frequently for undesired files and are removed promptly. An alternative would be to have the file mode 733. This means that the owner, ftpdadmin, has full access but others have only write and execute access. This account, ftpdadmin, should be different from the account that is used for anonymous FTP login, typically ftp. This allows the anonymous user to upload files ftp users cannot see what is in that directory, preventing the directory from being used for public exchange.

Certainly, the person uploading can tell others the file name and then they could download it. A solution would be to periodically "sweep" these files into a different directory that is not accessible at all by ftp, via a cron job. The sweep directory might be ~ftp/sweep, owned by ftpdadmin and mode 700. This is a simple ftpdadmin cron job to sweep files into this directory hourly. It does not have protection against a file that it is overwriting an earlier file of the same name but then this will allow someone to update an submission.

```
* /bin/mv /home/ftp/incoming/* /home/ftp/sweep/ >dev/null 2>&1
```

Some sites will have ~ftp/incoming mode 711 with subdirectories of secret names being named 733. Someone wanting to upload a file will first have to ask the SysAdmin for the name of one of these secret directories and upload to it, but I do not see that this is a significant improvement on the method discussed earlier and requires more overhead.

# 3.4.2 FTP Proxy Dangers

![](bbox=[0.2, 0.733, 0.8, 0.803])

Older FTP servers allow a client to request that the server do operations to any arbitrary third system. This allowed a variety of security breaches, including sending e-mail that appears to come from an FTP server's system and tunneling through firewalls. If your FTP server was inside your network and the firewall allowed Internet access only to your FTP server, the proxy feature then could be used to access any system inside the firewall. The nmap network mapper can make use of this feature to probe behind firewalls. To see if