# Uploading files

An HTML form can provide a file selection facility, which calls upon the operating system’s “Choose File” dialog, to allow the user to browse their local file system and select a file. To enable this facility the HTML <form> tag must include an enctype attribute specifying the encoding type as “multipart/form-data”.

The full path address of the file selected for upload is a value stored in the FieldStorage object list that can be accessed using its associated key name. Usefully, the file name can be stripped from the path address by the “os” module’s path.basename() method.

A copy of an uploaded file can be written on the web server by reading from the FieldStorage object’s file property.

![](bbox=[0.11, 0.48, 0.22, 0.57])

+   1. Create a new HTML document containing a form with a file selection facility and a submit button

```
<!DOCTYPE HTML>
<html lang="en">
<head> <meta charset="UTF-8">
<title>File Upload Example</title> </head>
<body>
<form method="POST" action="upload.py" enctype="multipart/form-data" >
<input type="file" name="filename" style="width:400px">
<input type="submit" value="Submit">
</form>
</body>
</html>
```

![](bbox=[0.11, 0.84, 0.22, 0.94])