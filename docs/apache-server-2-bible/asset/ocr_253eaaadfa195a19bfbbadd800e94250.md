space character). A good thing about a CGI module is that it takes cares of decoding this and gives the script `Carol Godsave` as the name. The script displays a page as shown in Figure 12-4.

```
Hello Carol Godsave.
Thanks for coming to our Web site.
```

![](bbox=[0.18, 0.28, 0.55, 0.31])

The p() method creates an HTML paragraph tag pair, which is used to sandwich the parameter it receives. For example, the first p() call:

```
print $query->p( 'Hello ' . $formattedName . ',');
```

translates into:

```
<p>Hello Carol Godsave,</p>
```

The entire output document that is sent to the Web browser looks like this:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
      PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
      "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">

<html xmlns="http://www.w3.org/1999/xhtml"
      lang="en-US">

<head>
   <title>Greetings</title>
</head>
<body>

<p>Hello Carol Godsave,</p>
<p>Thanks for coming to our Web site.</p>

</body></html>
```

The start_html() method produces the following contents:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
      PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
      "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">

<html xmlns="http://www.w3.org/1999/xhtml"
      lang="en-US">

<head>
```