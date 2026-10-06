# Chapter 21: Setting Up a Web Server

```
$ chmod 711 /home/cjb/public_html
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```

For UserDir to work, the mod_userdir module must also be loaded (which it is by default).

There are two ways in which the UserDir directive can handle an incoming request that includes a username (for example, ~cjb). One possible format identifies the physical path of the individual users' accessible directories. The other can redirect a URL to which the request is redirected. A few examples are presented in Table 21-4, using the URL http://www.box.com/~cjb/proj/c004.html as a sample request.

# Table 21-4: UserDir Path Name and URL Examples

| UserDir Directive | Referenced Path or URL |
| --- | --- |
| UserDir public_html | ~cjb/public_html/proj/c004.html |
| UserDir/*/WWW | /cjb/WWW/proj/c004.html |
| UserDir/*/local/web | /usr/local/web/proj/c004.html |
| UserDir http://www.box.com/users | http://www.box.com/users/~cjb/proj/c004.html |
| UserDir http://www.box.com/~* | http://www.box.com/~cjb/proj/c004.html |
| UserDir http://www.box.com*/html | http://www.box.com/cjb/html/c004.html |

The UserDir directive can also be used to explicitly allow or deny URL-to-path name translation for particular users. For example, it is a good idea to include the following line to avoid publishing data that shouldn't be made public:

```
UserDir root
```

Alternatively, use the following lines to disable the translations for all a few users:

```
UserDir disable
UserDir enable wilhelm cjb jsmith
```

> NOTE: You should always be careful about content you publish about yourself on the Internet (names, addresses, personal information,and so on) and keep in mind that you could be accountable for the content you publish on your Web server. When you allow others to publish on your Web server, your liability can extend to those users publish as well. Be sure to have a clear policy about what is acceptable (and legal) to publish on your Web server and give that information to those you allow to use the server.