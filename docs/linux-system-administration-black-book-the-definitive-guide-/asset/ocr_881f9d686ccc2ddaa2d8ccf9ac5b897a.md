**AddModule**, on the other hand, adds a module to Apache without making it active. You use this one differently:

```
AddModule module
```

So, you would not typically uncomment both of these items. Either you would load it, or you would add it. Not both. The module mod_put is available from [http://pwww.ec-lyon.fr/~/vincent/apache/mod_put.tgz](http://pwww.ec-lyon.fr/~/vincent/apache/mod_put.tgz), and is used to implement the **HTTP PUT** and **DELETE** methods described in Table 13.9.

After these items is an HTTP upload area definition:

```
#Alias /upload /tmp
#<Location /upload>
# EnablePut On
# AuthType Basic
# AuthName Temporary
# AuthUserFile /etc/httpd/conf/passwd
# EnableDelete Off
# umask 007
# <Limit PUT>
#	require valid-user
# </Limit>
#</Location>
```

This commented-out section first tells Apache that whenever an HTTP client asks for anything in DocumentRoot/upload, the server should turn to the contents of the /tmp directory. Then, a **<Location>** statement outlines what is allowed for DocumentRoot/upload.

There are a few new directives defined here. The first is **EnablePut**. This directive, as you might have guessed, makes the PUT HTTP method described in Table 13.9 available for use. **AuthType**, although not new, was not defined in context earlier. The **AuthType** directive sets the level of user authentication required to access a directory. This ensures that this section of code does not let random people have access to the DocumentRoot/upload directory. There are two values available for **AuthType**, but only **Basic** is currently implemented. This value requires clients to log in to use this section of your Web space.

Three other directives in this section are needed to fully implement the authentication scheme. The next item in the code, **AuthName**, is one of these. It assigns a distinctive string to this particular authorization rule, so when the user tries to access the protected URL they are given information to put the password request in context. In this case, the text “Temporary” will appear in the authentication