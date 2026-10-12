![](bbox=[0.12, 0.14, 0.6, 0.55])

# **FIGURE 20.1**  
*A sample Big Brother Web page displaying the available servers and their current status.*

that page. This discourages others outside your system from gleaning information about your system. The standard Apache version that comes with the Red Hat Linux distribution offers password-protection capability. Using the htpasswd executable, you can create a flat text file that holds usernames and the encrypted passwords. In the page you wish to password-protect, simply place a .htaccess executable with the correct syntax.

The following is an example from my own Big Brother page. You should customize it to fit your own setup.

```
AuthName "Big Brother"
AuthType Basic
AuthUserFile /usr/local/apache/htdocs/passwords/bb
AuthGroupFile /dev/null
require valid-user
```

You will also want to make sure the htpasswd executable is in your PATH. The .htaccess file ensures that unauthorized users do not gather more information than necessary from your Web page.