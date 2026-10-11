```
```
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://10.11.0.22/feedback.php
...
```
```

![](bbox=[0.11, 0.18, 0.88, 0.19])

As demonstrated above, the browser redirection worked, sending the victim browser to our attack machine through the iframe. Again, the victim would not see the zero-size iframe in their browser.

We could take this farther and redirect the victim browser to a client-side attack or to an information gathering script.

To do this, we would want to first capture the victim’s User-Agent header to help identify the kind of browser they are using. In the above example, we used Netcat because it shows us the full request sent from the browser, including the User-Agent header. The Apache HTTP Server will also capture the User-Agent header by default in `/var/log/apache2/access.log`.

We will not be executing any client-side attacks here. Instead, we will attempt to gain access to the web application as an administrative user.

# 9.4.2.4 Stealing Cookies and Session Information

We can also use XSS to steal cookies[^269] and session information if the application uses an insecure session management configuration. If we can steal an authenticated user’s cookie, we could masquerade as that user within the target web site.

To provide some background, websites use cookies to track state[^270] and information about users. Cookies can be set with several optional flags, including two that are particularly interesting to us as penetration testers: `Secure` and `HttpOnly`.

The `Secure`[^271] flag instructs the browser to only send the cookie over encrypted connections, such as HTTPS. This protects the cookie from being sent in cleartext and captured over the network.

The `HttpOnly`[^272] flag instructs the browser to deny JavaScript access to the cookie. If this flag is not set, we can use an XSS payload to steal the cookie.

However, even if this flag is not set, we must work around some other browser controls because browser security dictates that cookies set by one domain cannot be sent directly to another domain. As an aside, this can be relaxed for subdomains in the `Set-Cookie` directive via the `Domain` and `Path` flags. As a workaround, if JavaScript can access the cookie value, we can use it as part of a link and send the link, which we could deconstruct to retrieve the cookie value.

Let’s try an example to demonstrate how this works. Our example application sets a `PHPSESSID` cookie when an admin user logs in. The application uses the cookie to determine if the user has

[^269] (Wikipedia, 2019), https://en.wikipedia.org/wiki/HTTP_cookie

[^270] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Session_(computer_science)

[^271] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Secure_cookie

[^272] (Mozilla, 2019), https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Secure_and_HttpOnly_cookies