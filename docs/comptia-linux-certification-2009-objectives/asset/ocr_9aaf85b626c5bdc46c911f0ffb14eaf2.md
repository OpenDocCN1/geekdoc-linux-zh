+   a. On the system labeled **srvA**, using the *vi* editor, open the `/etc/squid/squid.conf` file.
b. Locate the text “http_port 3128” and verify that the line is uncommented.
c. Locate the line with content “#http_access allow our_networks.”
d. Press **O** to switch to the insert mode and move to a new line.
e. Enter
```
acl myhosts src
192.168.0.0/255.255.255.0
```
to define the myhosts ACL.
f. Enter
```
acl admin src
192.168.1.0/255.255.255.0
```
to define the admin ACL.
g. Enter
```
acl lunch time MTWTF 12:00-13:00
```
to define an ACL for lunchtime.
h. Enter
```
http_access allow myhosts
```
to grant access to the myhosts ACL.
i. Enter `http_access allow lunch` to grant access to everyone during lunchtime on weekdays.
j. Enter
```
http_access deny admin
```
to deny access to the admin ACL.
k. Enter `visible_hostname srvA.ourglobalcompany.com` to declare **srvA** as a visible_hostname.

See *Code Sample 1*.

```
Code Sample 1
```
acl myhosts src 192.168.0.0/255.255.255.0
```
```