# OffSec

301 shows a WordPress instance (indicated by the URL and title of the page) on INTERNALSR1 Let's browse to the dashboard login page for WordPress at http://127.0.0.1/wordpress/wp-admin and join to it with credentials we discovered so far.

Once we entered the URL, Firefox displays an error:

![](bbox=[0.125, 0.196, 0.875, 0.423])

Figure 302: Failed Redirect to the Administrator Login

The navigation bar in Firefox shows that we were redirected to internalsrv1.beyond.com. We can assume that the WordPress instance has the DNS name set as this address instead of the IP address. Because our machine doesn't have information about this DNS name, we cannot connect to the page.

To be able to use the web application, we'll add internalsrv1.beyond.com via 127.0.0.1 to /etc/hosts.

```
kali@kali:~beyond1 cat /etc/hosts
127.0.0.1       localhost
127.0.0.1       kali
...
127.0.0.1       internalsrv1.beyond.com
...
```

Now, let's open the /wp-admin page again.