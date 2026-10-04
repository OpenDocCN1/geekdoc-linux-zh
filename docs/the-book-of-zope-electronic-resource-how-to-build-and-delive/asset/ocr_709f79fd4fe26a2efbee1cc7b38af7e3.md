```
SERVER_URL http://dev4.dmz.beehive.de
name Egon
URL0 http://localhost:8080/My_Homepage/index_html
URL1 http://localhost:8080/My_Homepage
URL2 http://localhost:8080
BASE0 http://localhost:8080
BASE1 http://localhost:8080
BASE2 http://localhost:8080/My_Homepage/index_html
BASE3 http://localhost:8080/My_Homepage/index_html
```

environ

```
HTTP_ACCEPT_ENCODING gzip
GATEWAY_INTERFACE CGI/1.1
SERVER_PORT 8080
PATH_TRANSLATED /My_Homepage/index_html
HTTP_VIA 1.0 (Squid/2.2.STABLES)
HTTP_COOKIE tree-s=eJITf3ZHPANV/VYHUDALI1EYELA
HTTP_ACCEPT_LANGUAGE en
PROFILE_PUBLISHER /usr/local/zone 2.2.2/var/profile.txt
HTTP_X_FORWARDED_FOR unknown
REMOTE_ADDR 192.168.1.1
SERVER_NAME localhost
HTTP_USER_AGENT Mozilla/4.7 [en] (WinNT);
HTTP_ACCEPT_CHARSET iso-8859-1,utf-8
HTTP_ACCEPT image/gif,image/x-bitmap,image/jpeg,image/jpeg,image/png,*"
channel_creation_time 971686366
SERVER_PROTOCOL 1.0
PATH_INFO /My_Homepage/index_html
HTTP_HOST localhost:8080
REQUEST_METHOD GET
SCRIPT_NAME
SERVER_SOFTWARE Zope/2.2.2 (source release, python 1.5.2, linux2) ZServer/1.1b1
HTTP_CACHE_CONTROL max-age=359200
CONNECTION_TYPE keep-alive
HTTP_REFERER http://localhost:8080/My_Homepage/index_html/manager_edit
```

The variables name and roles (or other) were previously set as follows using REQUEST.set:

```
<html-call-expr="REQUEST.set('name', 'Egon')">
<html-call-expr="REQUEST.set('roles', ['Manager', 'Owner'])">
```

As you can, the REQUEST is divided into four sections: form, cookies, other, and environ, and each section contains variables. This sample REQUEST

356 Appendix B