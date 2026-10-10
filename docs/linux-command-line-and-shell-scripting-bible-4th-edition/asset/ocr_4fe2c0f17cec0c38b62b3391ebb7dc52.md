```
This is the line in the Web page.
This should provide some
information to use in our sed script.
```

$

Notice that the title text is missing, along with the text that was bolded and italicized. The sed editor literally interpreted the script to mean any text between the less-than and greater-than sign, including other less-than and greater-than signs! Each time the text was enclosed in HTML tags (such as <b>first</b>), the sed script removed the entire text.

The solution to this problem is to have the sed editor ignore any embedded greater-than signs between the original tags. To do that, you can create a character class that negates the greater-than sign. This changes the script to

```
s/<[^>]*>//g
```

This script now works properly, displaying the data you need to see from the web page HTML code:

```
$ sed 's/<[^>]*>//g' data11.txt
```

```
This is the page title
```

```
This is the first line in the web page.
This should provide some useful
information to use in our sed script.
```

$

That's a little better. To clean things up some, we can add a delete