+   15. Now, you need to create a similar statement for each of your own virtual hosts. Follow the same pattern as you did with the localhost statement. Make these <VirtualHost> directives as complex or as simple as you need them to be.

+   16. If you are finished configuring your /etc/httpd.conf file, press the Esc key, and type "ZZ" to save and close it.

# ## Configuring What Web Browsers See

To set up what Web clients can see when looking through your Web information, do the following:

+   1. Log in as root on the machine you want to use for your Web server.

+   2. Type “vi /etc/httpd/conf/httpd.conf”.

> **NOTE:** *If you are using the original Red Hat 6.1 or later, you may find that this information is instead in smb.conf.*

+   3. Use the cursor to move down to the following statement:

```
DocumentRoot /home/httpd/html
```

+   4. If you want to keep your Web files elsewhere, type “i” to enter Insert mode, and edit /home/httpd/html to indicate your preferred document base.

+   5. Cursor down to:

```
UserDir public_html
```

+   6. If you want user Web space to go into a different directory inside a user's home directory, change this value.

+   7. Move the cursor down to this line:

```
DirectoryIndex index.html .shtml index.cgi
```

+   8. If you want to add other default base page items to this list, add them in the order that they should be sough.

+   9. Move down to:

```
FancyIndexing on
```