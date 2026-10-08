# Chapter 5: Authentication 147

In step 2, the client is redirected to the login form at http://login.passport.login.asp. The query string in the Location header contains information which Site partner originated the request (id=) and the URL to return to authentication is successful (return URL, or ru). The WWW-Authenticate header reads Passport version1.4:

```
HTTP/1.1 302 Object Moved
Location: http://login.passport/login.4?id=658&ru=http://my.msn.com/etc.
WWW-Authenticate: http://my.msn.com/etc.
```

The client requests the login page from login.passport.com in step 3:

```
GET /login.asp?id=658&ru=http://my.msn.com/etc. HTTP/1.0
Referer: http://my.msn.com/
Host: login.passport.com
```

The user then enters his or Her Passport password into login.asp, and POSTs the data; note that the credentials are sent via SSL, but appear as cleartext in our trace, which performed on the machine performing the login. Partners are not required to require SSL between the client and Passport's servers.

```
POST /pssecquest/post.srfc1=1033id=658&ru=http://my.msn.com/etc. HTTP/1.0
Referer: http://login.passport/login.asp?id=658&ru=http://my.msn.com/etc.
Host: login.passport.com
```

```
login=johndoe&domain=msn.com&passwd=guessme&msp_shared=
```

In step 4, following successful login, Passport's login servers set a series of cookies on the client. The important cookie is the MSPAuth cookie, which is the Passport authentication ticket.

```
HTTP/1.1 200 OK
Set-Cookie: MSPAuth=4Z9iuseblah;domain=.passport.com;path=/
Set-Cookie: MSPProf=2Z9iuseblah;domain=.passport.com;path=/
etc.
```

Finally, in step 5, the client gets back to the original resource on the Partner site (which Passport's login servers remember from the ru in the original query string), they use the MSPAuth ticket in:

```
GET /my.aspx HTTP/1.0
Host: my.msn.com
Cookie: MSPAuth=2Z9iuseblah; MSPProf=2Z9iuseblah
```

Now that the client presents the ticket, it gets access to the resource. Although this seems like a few round trips, it happens quickly and transparently to the user, depending on the speed of the Internet connection.