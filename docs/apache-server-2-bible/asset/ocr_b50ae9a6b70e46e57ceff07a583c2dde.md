Now lets make a little more useful script, as shown in Listing 15-3, which shows information about PHP as it is installed on your Web server.

# **Listing 15-3: info.php**

```
```html
<html>
  <head><title>Hello World Script</title>
  <body>
    <?php
      phpinfo();
    ?>
  </body>
</html>
```
```

This page calls a PHP function called `phpinfo()` to display a great deal of PHP options as they are currently configured using `php.ini`.

# # Using a PHP script as a Server-Side Include

If you wish to use PHP scripts in Server-Side Include (SSI) calls, you can call your PHP script using the following SSI tag:

```
```
<!-#include virtual="/path/script_name.php"->
```
```

For example:

```
```
<!-#include virtual="/phppssi/test.php"->
```
```

Here the PHP script called `/phppssi/test.php` script will be loaded from the page that uses the above SSI calls. For the PHP scripts to work with SSI, you must do the following:

+   1.  Enable the **ExecCGI** option in the directory containing the PHP scripts that need to be run via SSI calls.
+   2.  Make sure the **IncludesNoExec** option is disabled for the same directory. For example:

```
```apache
DocumentRoot  "/www/mysite/htdocs"
<Directory  "/www/mysite/htdocs/parsed">
```