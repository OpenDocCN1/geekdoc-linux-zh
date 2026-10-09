For example, when a user enters makesite as the keywords field value and chooses the dontcare case option from the drop-down list, the script (modified_form.php) displays the following:

You entered:
Keywords: makesite
Case: upper

# ## Creating sessions with PHP

PHP 4 introduced native session management, which makes creating user sessions simple. This means that you can track a user as the user moves from one page to another. There are two ways to maintain sessions with PHP.

# ### Using HTTP cookies to create user sessions

This is the default method. To create a session you need to call the session_start() function in your PHP page. For example, look at simple PHP page called start.php, which is shown in Listing 15-8.

# Listing 15-8: start.php

```
```PHP
<?php
session_start();
session_register('count');
$count++;
?>
<html>
<head><title>Start Session</title>
</head>
<body bgcolor="Red">

<?php echo "You have visited this page $count time(s)."; ?>

<p>
<a href="/next_page.php">Next</a>
</p>
</body>
</html>
```
```

In the listing you can see two PHP scripts. The first script creates a session by calling the session_start() function. It also registers a session variable called count by using the session_register() function and increments the variable by one. Notice that this script is kept outside the <html> tag. This is required because the script sets the session cookie, which is an HTTP header that must come before any contents. The above PHP page assumes that you have output_buffering set