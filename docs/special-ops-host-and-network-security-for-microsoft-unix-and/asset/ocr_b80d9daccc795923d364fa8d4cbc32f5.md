# 576 Chapter 11 : Hacking Custom Web Applications

Accept: image/gif, text/html, /*
Accept-Language: en-us
User-Agent: Mozilla/4.0 (compatible; MSIE 5.0; Windows NT 5.0; .NET CLR 1.0.3705)
Host: www.sensepost.com

The GET method is normally frowned upon, because form information may be truncated (there is a limitation on the permissible length of a URL) and because it presents such obvious tampering capabilities.

```
POST /special_ops/login.asp HTTP/1.0
Accept: image/gif, text/html, /*
Accept-Language: en-us
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0; .NET CLR 1.0.3705)
Host: www.sensepost.com
Content-Length: 31
USERNAME=Haroon&PASSWORD=secret
```

In the form above, we made use of three types of input, the TEXT, PASSWORD, and SUBMIT types. Other types of input can be CHECKBOX, RADIO, TEXTAREA, OPTION, and HIDDEN.

The interactivity that an attacker is searching for be contained within a form, but using the GET request could be nested within a normal-looking, clickable link on a Web page, such as the innocent-looking link that reads Next. It could be as follows:

```
<A href="http://www.sensepost.com/special_ops/login.asp?USERNAME=Haroon&PASSWORD=secret">Next</A>
```

Finding areas of interactivity reinforces the previous step of the methodology, viewing the source for revealing information. The next step involves pinpointing the weaknesses in how the application was designed.

# Pinpointing Attack Vectors

In order to determine how an attacker could exploit the application, you first need to have a complete understanding of the application itself. You need to fully understand what the application does, what it was designed to do, and with this

![](bbox=[0.068, 0.943, 0.293, 0.973])