# PHP Output

For a web page to be dynamic, the PHP code must create HTML code for the client to interpret. The example in the previous section used the PHP `echo` command to send text to the client web browser. The browser interprets the text as if it were part of the normal HTML code page.

Let’s do an exercise to see how this works. Follow these steps to create a dynamic web page:

+   1. Create a text document in the `/var/www` folder called `phptest.php`. You can use either the standard gedit program or the vim editor from the command prompt, but you must have administrative privileges to create the file. You can do that by running the command:
+   
+      `sudo gedit /var/www/phptest.php`

+   2. Copy the following sample code (which we looked at in the previous section) and paste it into your text file:

```
```html
<html>
<body>
<h2>This is the first PHP coding section</h2>
<?php
echo "This is <i>PHP code</i>\n";
?>
<h2>This is the second PHP coding section</h2>
<?php
echo "This is <b>more</b> PHP code\n";
?>
</body>
</html>
```
```

If you use the gedit editor, it’ll automatically highlight your code for you. The code creates a web page and displays two text lines within the page using PHP code.

+   3. Save the file and exit the editor.

+   4. Test the code by opening your browser and using the URL `http://localhost/phptest.php`.

Any web page file that contains PHP code must use a `.php` file extension. This extension notifies the Apache web server that it must run the web page through the PHP preprocessor to execute the embedded PHP code. If you use the standard `.htm` or `.html` file extension, the web server won’t process your PHP code, and your clients will see just the raw PHP code on their screens (ouch).

Figure 30-3 shows what you should see when you view the web page from a browser.

If you view the web page HTML code from your browser, you’ll see the exact code that the server sent. In Microsoft Internet Explorer, you can do this by clicking View ➔ Source, or in Firefox by selecting View ➔ Page Source. Notice that the HTML code shown doesn’t include the embedded PHP code, just the HTML code that the PHP `echo` commands generated, as shown in Figure 30-4.