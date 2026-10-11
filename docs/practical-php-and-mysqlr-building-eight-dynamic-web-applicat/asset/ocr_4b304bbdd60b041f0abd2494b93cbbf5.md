interchangeably on the vast majority of scripts that you write. Both your HTML and PHP code will reside in any files that end in .php.

To begin, you'll create a simple page that contains some HTML. Create a new file, and call it 1.php. Add the following code in the file:

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<title>Tough first script</title>
</head>
<body>
<h1>The very first script</h1>
<p>
This is the first script!
</p>
</body>
</html>
```

In this example, you are writing some HTML to construct a simple Web page. This HTML first selects a suitable DOCTYPE (the dialect of HTML to use) and then goes on to set the title of the page (the text in the window border) with the <title> tag. Next, a large heading with the <h1> tag is added before then supplying the memorable words This is the first script! inside a paragraph (indicated by the <p> and </p> tags). If you have a burning ambition to change the memorable words to something else, so be it.

# NOTE

# Running Your Code

When you create the files that store your code, make sure to place them in the directory that your Web server reads for files. This directory is typically called htdocs. If you are using XAMPP, this directory is called /opt/lampp/htdocs on Linux, and in Windows it is the htdocs directory inside the directory where you installed it.

To run your code, remember that http://localhost points to this htdocs directory. As such, if you want to access 1.php, go to http://localhost/1.php in your Web browser.

You may have noticed that this code has been stored in a file that has a .php extension instead of the .htm or .html extension. This is because all PHP scripts that you will use are ultimately converted into text that the Web browser can