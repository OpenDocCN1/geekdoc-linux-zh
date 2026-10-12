
## Chapter 7

### Code Implementation
```php
}

function check_login($username, $password)
{
    $ret = false;

    if ($username && $password)
    {
        // Check if login matches database values
        $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);

        if (mysql_select_db(AUTH_DB, $conn))
        {
            // Search for matches
            $result =
                mysql_query("SELECT COUNT(username) AS ucount
                             FROM Users
                             WHERE username='" . addslashes($username) . "'
                             AND passwd_md5='" . md5($password) . "'
                             AND passwd_sha1='" . sha1($password) . "'",
                             $conn);

            // Check if a match was found
            if (($row = mysql_fetch_array($result)) && $row['ucount'])
            {
                $ret = true;
                $_SESSION['username'] = $username;
            }

            // Close connection
            mysql_close($conn);
        }
    }

    return $ret;
}

session_start();

// Check if using valid credentials
if (!(isset($_SESSION['username']) ||
      (isset($_SERVER['PHP_AUTH_USER']) &&
       check_login($_SERVER['PHP_AUTH_USER'],
                   $_SERVER['PHP_AUTH_PW']))))
{
    // Show login prompt
    attempt_auth();
    echo 'Authorization Required';
    exit();
}
?>
```

What does all this mean? Take a look at what makes this script tick.

The first thing you are going to do is define some constants for the database connection:

```php
<?php

// Define database constants

define('AUTH_HOST', 'localhost');

define('AUTH_USER', 'WebAuth');

define('AUTH_PASS', 'AuthPass');

define('AUTH_DB', 'WebAuth');
```

Next comes the function definition for `attempt_auth()`. This function simply sends response headers to the browser, telling it to attempt a Basic Authentication login, with the given realm displayed as the security zone in the login prompt:

```php
function attempt_auth()
{
  // Send authentication headers
  header('WWW-Authenticate: Basic realm="Protected by PHP"');
  header('HTTP/1.0 401 Unauthorized');
}
```

After `attempt_auth()` is the function definition for `check_login()`. This is where the passed username and password will actually be checked against values stored in the **WebAuth** database created earlier. The first order of business is to make sure a username and password were passed, and to connect to the database and set **WebAuth** as active:

```php
function check_login($username, $password)
{
	$ret = false;
	if ($username && $password)
	{
	  // Check if login matches database values
	  $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);
	  if (mysql_select_db(AUTH_DB, $conn))
	{
```

After a database connection is made, you perform the query that checks for a username/password match:

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS account
FROM users
WHERE username='$username'
AND password=md5('$password')
AND passwd_sha1='$sha1'", $conn);
```

To build this query, the username must first be escaped using `addslashes()`, to help avoid any SQL-injection attacks (discussed later). The PHP functions `md5()` and `sha1()` are used here, but if you wanted, you could easily use the MySQL equivalents — they should produce the exact same result:

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS count
FROM users
WHERE username='" . addslashes($username) . "'
AND passwd_md5=MD5('" . addslashes($password) . "')
AND passwd_sha1=SHA1('" . addslashes($password) . "')",
$conn);
```

You might have noticed that the `addslashes()` function was added as a wrapper for the passwords, where it didn’t exist in the previous case where PHP was doing the password hashing. This is again to prevent any SQL injection attacks or even simple errors where a user’s password might contain an apostrophe. When hashing the passwords first with PHP, there’s no need to escape the result with `addslashes()`, because both the `md5()` and `sha1()` functions produce output consisting solely of hexadecimal values — there’s no way an apostrophe or other dangerous character will slip through.

To finish the `check_login()` function, set the return placeholder to **true**, and create a session variable that you’ll use later in the script to avoid unnecessary repeat queries:

```php
// Check if a match was found
if (($row = mysql_fetch_array($result)) && $row['account'])
{
$ret = true;
$_SESSION['username'] = $username;
}

// Close connection
mysql_close($conn);
}

return $ret;
}
```

On to the actual first-interpreted code in the script, you begin by initializing the session data:

```php
session_start();
```

Then you’ll first check to see if the session variable from `check_login()` is set. If it is not yet set — meaning the person has not yet authenticated — check for the PHP `USER` and `PHP_AUTH_PW` server variables and call the `check_login()` function. The server variables `PHP_AUTH_USER` and `PHP_AUTH_PW` both exist when PHP attempts to get login information using Basic Authentication. If they are not set, the user hasn’t yet been prompted for the login information. In this case, you want to prompt the user for login information if none has been passed and if the credentials previously passed were not valid. If no valid user information is found, `attempt_auth()` is called, and the user gets another chance to login. If, and only if, the user clicks Cancel on the login prompt, the “Authorization Required” message is displayed:

```php
// Check if using valid credentials
if (!(isset($_SESSION['username']) ||
      (isset($_SERVER['PHP_AUTH_USER']) &&
        check_login($_SERVER['PHP_AUTH_USER'],
                    $_SERVER['PHP_AUTH_PW']))))
{
    // Show login prompt
    attempt_auth();
    echo 'Authorization Required';
    exit;
}
?>
```

To test out the PHP authentication, you could simply attempt to load this script in your browser, but it's much better if you include it in any standard PHP page you've created. You can use the following code to test out this authorization as a simple inclusion:

```php
<?php

require_once 'phpauthbasic.php';

echo "Authentication Successful!";
?>
```

When you try to load this script in your browser, use the testuser/testpass combination, or whatever you originally added to the users table. If the username and password are correct, you should see a nice “Authentication Successful!” message; if you click Cancel, you’ll get the dreaded “Authorization Required” message.

Now that you’ve seen it work, you might think there’s no reason not to use this method. But as with many of the choices you’ll make when deciding how to write your applications, this method has some drawbacks.

There are two main requirements that must be fulfilled before this authentication method will work. First, safe_mode must not be enabled in php.ini. When enabled, safe_mode prevents the creation of the PHP_AUTH_USER and PHP_AUTH_PW server variables. If those variables don’t exist, the script will keep redisplaying the login prompt until the user clicked Cancel, regardless if the credentials used were truly valid. A quick way to determine if safe_mode is indeed enabled: the uid of the script is added to the end of the realm information in the login prompt.

Second, this method cannot be used in conjunction with Apache’s Basic Authentication system. This applies to any Apache-controlled access (htaccess) at the same level of the script, or at any parent directories. If both authentication systems are enabled, the Apache system takes initial precedence. What will happen is the user can log in initially using the credentials valid with the Apache Basic authentication, which is followed by the PHP authentication prompt. At this point, however, HTTP has effectively cleared the browser’s authentication state with the Apache controls — a result of the HTTP 401 response. Because the browser is no longer authenticated against Apache, it will re-prompt for the Apache-level credentials, and then go back to the PHP credentials, and so on, until the user clicks Cancel or Stop in their browser.
