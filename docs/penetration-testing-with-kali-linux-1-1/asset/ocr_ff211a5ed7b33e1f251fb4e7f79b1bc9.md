![](bbox=[0.12, 0.03, 0.27, 0.09])

```
+ http://10.5.5.25:8080/error (CODE:400|SIZE:6082)
+ http://10.5.5.25:8080/favicon.ico (CODE:200|SIZE:17542)
(!) WARNING: All responses for this directory seem to be CODE = 403.
   (Use mode '-w' if you want to scan it anyway)
...
+ http://10.5.5.25:8080/login (CODE:200|SIZE:1942)
+ http://10.5.5.25:8080/logout (CODE:500|SIZE:14235)
(!) WARNING: All responses for this directory seem to be CODE = 403.
   (Use mode '-w' if you want to scan it anyway)
...
+ http://10.5.5.25:8080/robots.txt (CODE:200|SIZE:71)
...

---- Entering directory: http://10.5.5.25:8080/assets/ ----

------------------
END_TIME: Thu Dec 12 10:16:39 2019
DOWNLOADED: 9224 - FOUND: 5
Listing 985 - Dirb scan of Jenkins
```

Our scan found some endpoints, but nothing of value.

Next, let’s do something that our hacker intuition has been whispering for us to try. Let’s enter the credentials admin:password and admin:admin. Weak password configurations are very common within internal networks as only “trusted” users are expected to be able to access the server.

In addition, attempting a couple of password combinations will very rarely set off any alarms as it’s typical for a regular user to occasionally type in a password incorrectly.