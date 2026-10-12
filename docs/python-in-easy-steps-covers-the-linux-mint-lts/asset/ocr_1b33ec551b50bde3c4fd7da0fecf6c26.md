# ## Handling values

Values can be passed to a Python script on the web server when the browser makes an HTTP request. Those values can be used in the script and echoed in a response returned to the browser.

Python’s “cgi” module can be used to easily handle data passed from the web browser by an HTTP request. This provides a FieldStorage() constructor that creates an object storing the passed data as a dictionary of key:value pairs. Any individual value can then be retrieved by specifying its associated key name within the parentheses of that FieldStorage object’s getvalue() method.

The browser can submit data to the script using a “GET” method that simply appends key=value pairs to the script’s URL address. These follow a ? question mark character after the file name and multiple pairs must be separated by an & ampersand character. For example, script.py?key1=value1&key2=value2.

![](bbox=[0.11, 0.52, 0.2, 0.62])

+   1. Create a new HTML document containing hyperlinks with appended values to pass to a Python script
+   ```html
+   <!DOCTYPE HTML>
+   <html lang="en">
+   <head>
+   <meta charset="UTF-8">
+   <title>Python Appended Values</title>
+   </head>
+   <body>
+   <h1>
+   <a href="get.py?make=Ferrari&model=Dino">Ferrari</a>
+   <a href="get.py?make=Fiat&model=Topolino">Fiat</a>
+   <a href="get.py?make=Ford&model=Mustang">Ford</a>
+   </h1>
+   </body>
+   </html>
+   ```