# Providing text areas

Large amounts of user-input text data can be passed from a web page to a web server using HTML <textarea> tags and the form POST method. This tag has no value attribute so a default value may not be provided. It is, therefore, useful to have the Python script test whether the text area has been left blank and provide a default value when the user has entered no text.

![](bbox=[0.12, 0.32, 0.21, 0.41])

+   1. Create a new HTML document containing a form with a text area field and a submit button
+      ```html
+      <!DOCTYPE HTML>
+      <html lang="en">
+      <head> <meta charset="UTF-8">
+      <title>Text Area Example</title> </head>
+      <body>
+      <form method="POST" action="text.py">
+      <textarea name="Future Web" rows="5" cols="40">
+      </textarea>
+      <input type="submit" value="Submit">
+      </form>
+      </body>
+      </html>
+      ```

![](bbox=[0.12, 0.68, 0.2, 0.78])

+   2. Next, start a new Python script by making CGI handling features available and create a FieldStorage data object
+      ```python
+      import cgi
+      data = cgi.FieldStorage()
+      ```