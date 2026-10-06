The LoadModule directive points the Apache server to the actual PHP module that will be loaded by the web server for processing PHP scripts. The AddType directive maps the given filename extension, .php, onto the specified content type.

To test the module, create the following file, example.php, and try to access it through the web server. If all works, a test message that includes the welcome message "Hi, I'm a PHP script! and the current date is displayed within the browser window. If the script fails, you'll see an error message, either from the web server or the PHP module, depending on what the issue is.

```
<html>
<title>Example</title>
<body>

<?php
echo "Hi, I'm a PHP script!";
echo "Today is";
echo date("d S of F Y h:i:s A");
?>

</body>
</html>
```

For more information on using PHP, you can turn to PHP and MySQL Bible by Tim Converse, Joyce Park, and Clark Morgan (Wiley, 2004).

For SUSE users there are a number of resources for finding and installing the web server, including the Apache Software Foundation and SUSE.

While configuration of the web server is a snap, a number of tools such as graphical interface (GUI) tools are designed to change the configuration of the web server by providing configuration options in a basic point-and-click interface. And, of course, don't forget about YaST!

In fact, all of this shows that the Apache server is a powerful tool. However, this chapter hasn't even begun to cover the tip of the iceberg. A number of resources exist to provide details of all what can be done with the Apache server and its corresponding source license. These web sites include:

+   * The ASF main site (www.apache.org)

+   * Apache Week (www.apacheweek.com), a newsletter dedicated to covering news of the web server and related projects

+   * Planet Apache (www.planetapache.org), a web site dedicated to collecting the latest blog posts from Apache developers worldwide