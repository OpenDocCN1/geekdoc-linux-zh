
interchangeably on the vast majority of scripts that you write. Both your HTML and PHP code will reside in any files that end in .php.

To begin, you'll create a simple page that contains some HTML. Create a new file, and call it 1.php. Add the following code in the file:

```html
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

In this example, you are writing some HTML to construct a simple Web page. This HTML first selects a suitable DOCTYPE (the dialect of HTML to use) and then goes on to set the title of the page (the text in the window border) with the `<title>` tag. Next, a large heading with the `<h1>` tag is added before then supplying the memorable words "This is the first script!" inside a paragraph (indicated by the `<p>` and `</p>` tags). If you have a burning ambition to change the memorable words to something else, so be it.

### NOTE

### Running Your Code

When you create the files that store your code, make sure to place them in the directory that your Web server reads for files. This directory is typically called htdocs. If you are using XAMPP, this directory is called /opt/lampp/htdocs on Linux, and in Windows it is the htdocs directory inside the directory where you installed it.

To run your code, remember that `http://localhost` points to this htdocs directory. As such, if you want to access `1.php`, go to `http://localhost/1.php` in your Web browser.

You may have noticed that this code has been stored in a file that has a .php extension instead of the .htm or .html extension. This is because all PHP scripts that you will use are ultimately converted into text that the Web browser can understand. You should always remember that the Web browser has no idea what PHP is. The Web browser understands text, HTML, and CSS only. It is the Web server that runs PHP that does the job of processing the PHP before sending the text, HTML, or CSS back to the browser.

Add a PHP block into your code:

```html
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
<p>
<?php

echo "This is PHP code";

?>
</p>
</body>
</html>
```

In this example, you created another paragraph block and added a PHP block inside it. If you run the script again, you will see another line of text that displays in your Web browser.

![](img/c75d0c4fa51711b62f211459ae794f3f_33_0.png)

### QUICK TIP

In this book, the code shown in bold represents new code that is added to your script.

When you want to use PHP code, encase the PHP commands within the `<?php` and `?>` tags. These two tags indicate the start and end points of a PHP block, and anything between these tags will be fed to the PHP interpreter and digested. You can think of these tags behaving in a similar way as the HTML `<!--` and `-->` comment tags, where everything inside those tags is considered a comment.

Remember how the Web browser doesn't understand PHP? To demonstrate this, look at the source code in your Web browser (usually by clicking **View > Source Code**). As you can see, there is no PHP in there. What happens is that the PHP interpreter on the server reads any PHP commands, executes them, and spits out HTML as the final output. In this example, the PHP **echo** command was used to send the contents within the double quotes to the Web browser. Each command in PHP ends in a semi-colon (;), and you can see it at the end of the **echo** command.

### NOTE
**Using HTML Within PHP**

You can use HTML tags within the PHP echo statement. The purpose of an echo statement is to send information to the browser, and if you want to embed HTML tags or other content (such as CSS or JavaScript) that is readable by Web browsers, you are free to do so. For example, change the preceding echo line to this:

```php
echo "This is <strong>PHP</strong> code";
```

In this line, you are using the HTML **`<strong>`** tag to make a part of the echo statement bold. This is an incredibly useful and often used feature in PHP.

Remember that you can only put HTML tags inside legitimate PHP commands. You can’t just dump HTML inside a PHP block like this:

```php
<?php
<strong>Boogaloo with my didgeridoo</strong>
?>
```

Everything inside the `<?php` and `?>` tags is expected to be PHP, and the `<strong>` tags are HTML (not PHP).

## Using Variables

Variables are the bread and butter of any programming language. A **variable** is a small portion of memory that stores a particular piece of information. Imagine for a second that you have a cardboard box and a pen in your hand. You now decide to store your favorite CD in the box. To better remember what is in it later, you write ‘favealbum’ on the front of the box. You now know that if you look at the box and see ‘favealbum,’ you will remember that you have your slightly embarrassing Leprechaun Hits Volume 1 CD in there.

This is exactly how variables work, except that a variable stores information. In your program, you can create a variable to store some information and then reference what is in that variable by the name of the variable itself. This is best explained with an example.

Create a new file called `simplevariable.php` and add the following code:

```php
<?php
  $monkeys = 10;

  echo "Number of monkeys: " . $monkeys;
?>
```

All variables in PHP begin with a dollar sign ($). In the preceding example, you first create a variable called $monkeys and then used the = sign to set this to the value 10. This is the common way to create a variable in PHP; you simply pick a variable name out of thin air (in this example, my love of monkeys has been indulged) and then set the variable to store a particular value. With $monkeys created, you can now read the code and mentally replace $monkeys for the value 10 when you see it.

One important note at this point, particularly for those of you with prior experience in other programming languages, is that you do not need to indicate what type a variable will be in PHP. In other languages (such as C/C++), you would need to indicate that a variable containing a number is an integer variable. PHP is different and figures out what the type is when you use the variable.

With the variable set, it is then used in the next line in which the echo command is used to first display "Number of monkeys:" and then the value of $monkeys is displayed next to it. When you run the script, you should see the following output: "Number of monkeys: 10"

This echo line uses a technique called concatenation. This bizarre-sounding act provides a simple method of stringing together bits of text (called strings) with the contents of variables. To do this, you use the . symbol (called the concatenation operator) to glue together whatever is on the left and right sides of the dot, or period. In the preceding code, the part on the left side is the text "Number of monkeys:" and the part on the right is the contents of the $monkeys variable.

Concatenation is an important but often slightly confusing topic. It does take a little while to get used to, particularly when using more complex examples. As an example of this, change the echo line above to the following line:

```php
echo "You have " . $monkeys . " monkeys!";
```

In this line, you used the concatenation operator twice to glue an additional part onto the line. If you read the line from left to right, you can see how "You have" is then glued to the value of $monkeys (10), which is then glued to "monkeys!".

## PHP as a Simple Calculator

When you have the ability to create variables, you also have the ability to perform some simple mathematical calculations on them. For those of you who shudder at the thought of math, fear not; you will explore some of the common mathematical uses you will need in PHP.

To begin, create a new file called simplmath.php and add the following code:

```php
$cds = 50;
$tapes = 60;

$total = $cds + $tapes;

echo "You have " . $cds . " cds and " . $tapes . " tapes with " . $total . " items!";
```

In this example, you first created two variables, called $cds and $tapes, that have numbers stored in them. (If you are reading this book in 2020, tapes were items that stored music on them, a bit like your AstroDisks.) The sixth line of code then uses the + sign to add the $cds and $tapes variables together and stores the result in the $total variable. The final echo line then concatenates all of the variables into a single line that explains how many CDs and tapes there are and the total number of items available.

A number of symbols can be used when performing math. Some of the most common are covered in Table 2-1.

**TABLE 2-1 Math Operators in PHP**

| OPERATOR | DESCRIPTION | EXAMPLE |
| :--- | :--- | :--- |
| + | Addition | $total = $cds + $tapes; |
| - | Subtraction | $total = $cds - $tapes; |
| * | Multiplication | $total = $cds * $tapes; |
| / | Division | $total = $cds / $tapes; |

One of the great benefits of PHP has been its batteries-included approach to functionality. To help solve a range of problems, a number of facilities and functions are built right into PHP. For example, some numbers don’t divide easily. Imagine that you need to split a range of news stories across a number of different pages. To
