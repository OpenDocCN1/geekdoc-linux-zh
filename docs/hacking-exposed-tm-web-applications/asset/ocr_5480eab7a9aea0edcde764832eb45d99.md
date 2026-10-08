# Hacking Exposed Web Applications

calculate this number authentically. For example, here's the curl syntax for a POST request to access bank account information:

```
curl -v -d 'authmask=8195' -d 'uid=213987755' -d 'a=viewacct' \
> url https://www.victim.com/
* Connected to www.victim.com (192.168.1.23)
> POST / HTTP/1.1
User-Agent: curl/7.9.5 (x86-pc-cywin) libcurl 7.9.5 (OpenSSL 0.9.6c)
Host: www.victim.com
Pragma: no-cache
Accept: image/gif, image/x-xmap, image/jpeg, image/jpeg, /**
Content-Length: 38
Content-Type: application/x-www-form-urlencoded
```

authmask=8195&uid=213987755&a=viewacct

Thus, you see how curl makes it easy to calculate the Content-Length header.

# Hidden Tags

Hidden tags are so-called "hidden" values used in forms to pass data to the server. They are often used to track a session, a necessary inclusion since HTTP is a stateless protocol. Some sites use hidden tags to track product pricing or sales tax. Although hidden tags are hidden from the user viewing a Web site through a browser, tags are still visible in the HTML source of the page. In the case where an application passes sales tax through hidden tags, you could modify the value from a positive value to a negative one—suddenly sales tax works like a rebate!Hidden tags are part of HTTP forms, so you will see their values being passed in GET or POST requests. You should still look for the actual tags, where the field name or HTML comments may provide additional clues to the tag's function.

# URI

The Universal Resource Identifier (URI) is the string in the Location of the browser. The URI will be composed of the hostname of the Web server, along with the file to be retrieved. By simply modifying the filename and the URI, a hacker can sometimes retrieve files that would not normally be toable. For example, a site may have a link to http://www.victim.com/data/report12345.txt after you pay for access to report. Looking at the URI from a hacker's point of view, you would attempt to access http://www.victim.com/data/report12346.txt.

Another example of bypassing authorization is the Cisco IOS Authorization vulnerability. The URL of the Web-based administration interface contains a two-digit number between 16 and 99.

```
http://www.victim.com/level/NN/exec/...
```

By guessing of NN (the two-digit number), it is possible to bypass authorization and access the device's administration interface at the highest privilege.