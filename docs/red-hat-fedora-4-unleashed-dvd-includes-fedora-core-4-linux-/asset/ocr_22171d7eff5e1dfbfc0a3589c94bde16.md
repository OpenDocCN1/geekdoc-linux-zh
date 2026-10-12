# # Variable Substitution

PHP allows you to define strings using three methods: single quotation marks, double quotation marks, or heredoc notation. Heredoc is discussed in the next section because it really does need to be covered by itself, but single quotation marks and double quotation marks work identically, with one minor exception—variable substitution.

Consider the following code:

```
```php
<?php
  $age = 25
  echo "You are ";
  echo $age;
?>
```
```

That is a particularly clumsy way to print a variable as part of a string. Fortunately, if you put a variable inside a string, PHP performs *variable substitution*, replacing the variable with its value. That means we can rewrite the code like so:

```
```php
<?php
  $age = 25
  echo "You are $age";
?>
```
```

The output is the same. The difference between single quotation marks and double quotation marks is that single-quoted strings do not have their variables substituted. Here’s an example:

```
```php
<?php
  $age = 25
  echo "You are $age";
  echo 'You are $age';
?>
```
```

The first echo prints "You are 25", but the second one prints "You are $age".

# # Heredoc Syntax

The third method for setting string variables is called *heredoc*, and it enables you to use anything you want to signify the start and end of your string. Heredoc uses `<<<` (three left angle brackets) followed by your string terminator. You can then enclose all the text you want in your string, including variables you want PHP to substitute. When you are done, simply print your terminator at column 0 on a line, followed by a semicolon.

That last part is important: You need to have your heredoc terminator as the first thing on a line by itself. You cannot even have any spaces before the terminator, so be extra careful.

Like many things, this becomes most apparent when you see it in code (see Listing 31.4).