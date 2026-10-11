
To begin, we will set up the Windows 10 target by opening the XAMPP Control panel and clicking Start for both Apache and MySQL.

![](img/ec25e59d75726b7041242a56d3376832_276_0.png)

> Figure 117: XAMPP Control Panel

Next, we'll run **dirb** from Kali, targeting our Windows 10 machine.

```
kali@kali:--$ dirb http://10.11.0.22 -r
...
URL_BASE: http://10.11.0.22/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt
OPTION: Not Recursive
------------

GENERATED WORDS: 4612

---- Scanning URL: http://10.11.0.22/ ----
...
+ http://10.11.0.22/lpt1 (CODE:403|SIZE:1047)
+ http://10.11.0.22/lpt2 (CODE:403|SIZE:1047)
+ http://10.11.0.22/nul (CODE:403|SIZE:1047)
==> DIRECTORY: http://10.11.0.22/phpmyadmin/
+ http://10.11.0.22/prn (CODE:403|SIZE:1047)
+ http://10.11.0.22/robots.txt (CODE:200|SIZE:79)
...
```

> Listing 284 - Running dirb on our Windows 10 lab machine

The output lists several interesting URLs including the highlighted reference to phpMyAdmin, an administration tool for MySQL databases, which is particularly interesting.

Entering the corresponding URL into our browser produces a phpMyAdmin login page:

![](img/ec25e59d75726b7041242a56d3376832_277_0.png)

> Figure 118: phpMyAdmin Login Page

A quick Internet search suggests that the default login credentials for phpMyAdmin include “root” with a blank password. Let’s try that against our Windows 10 target:

![](img/ec25e59d75726b7041242a56d3376832_278_0.png)

> Figure 119. phpMyAdmin Error Message

If we try those credentials, we get an error message that “Login without a password is forbidden by configuration”. This is because “AllowNoPassword” is set to False within the phpMyAdmin configuration file (`C:\xampp\phpMyAdmin\config.inc.php`). Under this configuration, we need to include a password to log in so we can reasonably assume the password is not blank. We will have to try something else if we want to gain access.

### 9.4.1.2 Burp Suite Intruder

Since the default credentials didn’t seem to work and blank passwords aren’t allowed, let’s try to automate some basic username and password combinations with Burp Suite’s Intruder[^252] tool. Please keep in mind that this feature is time-throttled in the Burp Community Edition. Nevertheless, we can still use it in order to explain some important concepts.

[^252]: (PortSwigger, 2019), https://portswigger.net/burp/documentation/desktop/tools/intruder/using

Let's send a few manual login attempts from our browser and look at the responses in Burp Suite. We have combined three requests together in the following screenshot:

```
POST /phpmyadmin/index.php HTTP/1.1
Host: 10.11.0.22
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Length: 134
Content-Type: application/x-www-form-urlencoded
Cookie: phpMyAdmin=d092dd6dd2c235b7nosq180te265n; pma_lang=en
Connection: close
Upgrade-Insecure-Requests: 1

set_session=d092bq94db2c235b7nosq180te265npma_username=root&pm
a_password=test&server=1&target=index.php&token=65dcrJ0MfT0To7sZ2SB

POST /phpmyadmin/index.php HTTP/1.1
Host: 10.11.0.22
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 146
Cookie: phpMyAdmin=494hu2djjn8d8esc5cpl6o1gnsjn6bdu; pma_lang=en
Connection: close
Upgrade-Insecure-Requests: 1

set_session=494hu2djjn8d8esc5cpl6o1gnsjn6bdu&pm
a_username=root&pm
a_password=test2&server=1&target=index.php&token=42J3jP9N%C6%25C2%5D%7EC2%B5%7C2CU8D

POST /phpmyadmin/index.php HTTP/1.1
Host: 10.11.0.22
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Length: 138
Content-Type: application/x-www-form-urlencoded
Cookie: phpMyAdmin=9kr0nsla35tu12d7i5rg80d0w4nghq; pma_lang=en
Connection: close
Upgrade-Insecure-Requests: 1

set_session=9kr0nsla35tu12d7i5rg80d0w4nghqpma_username=root&pm
a_password=test3&server=1&target=index.php&token=%0k46Tt28F40Z18jD_CVX2VJ8
```

![](img/ec25e59d75726b7041242a56d3376832_279_0.png)

Based on the output, this test may not be straightforward as it seems since we have several factors to contend with. As we can see from the requests, the login form includes a token[^253] to prevent brute forcing and other attacks. In addition, we can see that the form sets a set_session parameter which is unique for each request.

[^253]: (Wikipedia, 2019). https://en.wikipedia.org/wiki/Cross-site_request_forgery#Synchronizer_token_pattern

If we change the set_session parameter and it doesn't match the value of the phpMyAdmin cookie, the site will return an error:

![](img/ec25e59d75726b7041242a56d3376832_280_0.png)

> *Figure 121: phpMyAdmin Error Message for Mismatching Session Values*

We need to avoid this error if we want a successful login. If we look at the HTML source for the login form, we will find the new _set_session and token values are included in the response:

### **Response**

![](img/ec25e59d75726b7041242a56d3376832_281_0.png)

In order to overcome this protective measure, and ensure the values match, we can automate the request with Intruder.

However, we must first submit a login request for Intruder to analyze. We can do this by navigating to Proxy > HTTP History, right-clicking on the POST request to `/phpmyadmin/index.php`, and then selecting Send to Intruder.

![](img/ec25e59d75726b7041242a56d3376832_282_0.png)

> *Figure 123: Send to Intruder*

Now, when we click on the *Intruder* tab, we discover that it contains multiple request sub-tabs. Under these, we will find four additional sub-tabs: *Target, Positions, Payloads, and Options*. Let's inspect these beginning with *Target*.

![](img/ec25e59d75726b7041242a56d3376832_282_1.png)

> *Figure 124: Intruder Target*

The information on this tab is prepopulated based on the request so we will leave the values as-is.

Next, let's review the contents of the **Positions** tab:

![](img/ec25e59d75726b7041242a56d3376832_283_0.png)

> *Figure 125: Intruder Positions*

We use this tab to mark which fields we want Burp Suite to inject payloads into when an attack is run. Burp Suite will automatically mark cookie values and POST body values as payload positions using a section sign (§) as a delimiter. However, we do not want to use all these default positions so we will clear them with **Clear §**.

We will leave *pma_username* set to "root" since this is our target user account. There are four other values we will modify in order to submit login attempts. We will insert the actual attempted password into *pma_password* by selecting the value and clicking **Add §**. The *phpMyAdmin* cookie value and *set_session* post body value change on each request, so we need to add them as payload positions as well. Finally, the *token* value also changes on each request to prevent brute forcing so we will need to select its value and click **Add §** as well.

We'll set the **Attack type** to "Pitchfork", allowing us to set a unique payload list for each position. This is necessary to account for the differences in the payload values we want to send. The pitchfork attack will place the first value from each list into their respective positions and then send the request. The next request will use the second value from each list, and so on. There are several other attack types in Intruder but we will not be reviewing them here.

![](img/ec25e59d75726b7041242a56d3376832_284_0.png)

Configuring a "Pitchfork" attack with the payloads we need here can be a bit confusing. Be sure to read through this entire section before trying to follow along.

We need to configure some of our payloads on the *Options* tab before we can use them so we will be skipping over the *Payloads* tab for now. We need something that can extract values from a response and inject them into the next request. Burp Suite includes a "Recursive grep" payload that searches a response with `grep` for a predefined value and makes the results available for the next request. This is exactly what we need to set the `phpMyAdmin` cookie value, `set_session` post body value, and the `token` field.

[^1]: (PortSwigger, 2019), https://portswigger.net/burp/documentation/desktop/tools/intruder/positions#attack-type

[^2]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Grep
