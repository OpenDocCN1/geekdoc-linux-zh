
## PHP Forms Authentication

If PHP Basic Authentication isn’t a viable solution for you, or the look of the browser’s login panel isn’t your cup of tea, have no fear; you’ve yet another option. Instead of relying on the standard built-in login window from your browser, you can easily craft your own login form, and you can even use most of the previous PHP authentication code. Enter the following as `phpauthforms.php`. Note that most of it is pulled directly from the `phpauthbasic.php` file you used earlier:

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB',   'WebAuth');

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
              mysql_query('SELECT COUNT(username) AS ucount
                           FROM Users
                           WHERE username="' . addslashes($username) . '"'
                           '  AND passwmd5="'   . md5($password)     . '"'
                           '  AND passwd_sha1="' . sha1($password)    . '"',
                           $conn);

         // Check if a match was found
         if (($row = mysql_fetch_array($result)) && $row['ucount'])
         {
            $ret = true;
            $_SESSION['username'] = $username;
         }
      }

      // Close connection
      mysql_close($conn);
   }

   return $ret;
}

session_start();
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
}
```

What has changed? Not much actually. The key modifications were made at the end of the file:

```php
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
    exit;
}
```

Instead of checking for the server variables `PHP_AUTH_USER` and `PHP_AUTH_PW`, you check the login credentials passed via HTTP POST, named `username` and `passwd`. Then, like the basic authentication example, if the login is invalid or not provided, a login prompt is presented to the user. In this case, the `attempt_auth()` function has been removed, and in the place where it once was called, sits a simple HTML form:

```php
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
exit;
}
```

## Chapter 7

To use this authentication method, you can simply include this script at the top of any page you want to protect. Call this one *testforms.php* (it has to match the target of the form used previously):

```php
<?php
require_once 'phpauthforms.php';
echo "Authentication Successful";
?>
```

So what are the advantages to this method? Compatibility, for starters. Using simple form-based authentication with PHP works in nearly any situation, regardless if *safe_mode* is enabled, or Apache is using `.htaccess` authentication of its own. The only real downside to a solution like this is that you must code your own login form, and style it how you want, instead of relying on the browser/OS to do that for you.

### Other Access Restrictions

In addition to restricting access by username and password, you can also use PHP to check other user parameters. One common variable to check is the source IP of the user. By referencing the server variable `$_SERVER['REMOTE_ADDR']`, you can make sure that only certain ranges of IPs are allowed to view a resource, or conversely, you can block specific IPs. If you're creating a website for a corporate intranet, you can restrict access to internal IPs (assuming your network uses them). For example, you could decide that only members of the 10.0.1.x network can view a special area of your website. Another example would be BBS sites or web forums. Often times they have the need to ban a specific user by IP, if the person is spamming the boards, for example.

Another server variable worth checking is the `$_SERVER['HTTP_REFERER']` variable. This variable holds the name of the previous page viewed, and can help you eliminate a certain class of web attacks. Suppose you create a simple form that saves data to a database, emails people, or anything that relies on valid user input. You might have even gone to great lengths to perform client-side input validation, and specified maximum lengths on your forms. Unfortunately, anything you might expect as input from a web client can easily be corrupted using an external form. Any site attacker can easily copy your form’s HTML markup, and then modify it to suit their needs—whether it be for information-gathering, cross-site scripting, SQL injection, or anything really.

All they need to do is make a copy of the form that can submit improper data to your site, host it on their own machine, but have it post to your form, using an absolute URL as the method. This kind of attack can be especially harmful when hidden form variables are used, and when *register_globals* is enabled in `php.ini`.

By checking the `HTTP_REFERER` value, you can eliminate a majority of spoofed form attacks, as long as you ensure the input is coming from a page actually on your website.

To see an example of `HTTP_REFERER` checking and `REMOTE_ADDR` verification in action, take a look at the following code:

```php
<?php
// Check the referer
if (!preg_match('/http:\/\/localhost|
' (www\.example\.com/i/',
$_SERVER['HTTP_REFERER'] ))
{
    echo 'Invalid referer! ' .
    'We don't take kindly to spoofed forms in these parts.';
}

// Check to see if request came from internal users
if ( !preg_match( '/ (10\.\d(1,3)\.\d(1,3)\.\d(1,3))|
'( 172\.16\.\d(1,3)\.\d(1,3) )|
'( 192\.168\.\d(1,3)\.\d(1,3) ) /i' ,
$_SERVER['REMOTE_ADDR'] })
{
    echo 'Invalid client address! ' .
    'Who let YOU in here?';
}
?>
```

This code simply checks the referring page first, to make sure it came from localhost or the expected domain (assuming you've changed it to match your own domain), and then checks the user's IP address to make sure it comes from an internal/private IP range.

Another thing PHP can do, to help limit certain kinds of access, is to provide CAPTCHA images for use in registration forms. CAPTCHA, which stands for "Completely Automatic Public Turing Test to Tell Computers and Humans Apart," is a kind of test where typically an image is presented with somewhat mangled text printed in the image. The idea is that humans should be able to figure out what the text actually says, despite its distorted appearance, whereas a computer cannot. Many free email and bulletin board sites use such a technology to keep automated robot scripts from registering and abusing the services with spam or the like.

While currently in an alpha stage of development, the `Text_CAPTCHA` package in the PHP Pear repository provides an easy interface to implement CAPTCHA functionality. `Text_CAPTCHA` can be found at http://pear.php.net/package/Text_CAPTCHA.

If you want to try out `Text_CAPTCHA`, you can simply install it using the `pear install` command:

```bash
pear install -f Text_CAPTCHA
```

You need to use the `-f` flag to force the installation because `Text_CAPTCHA` is currently not considered stable by the Pear team, so a normal unforced installation will fail. Also note that `Text_CAPTCHA` is dependent on the `Text_Password` and `Image_Text` (also alpha) Pear packages, so you'll need to install those first if you don't have them already.

Once they're all installed, create the following as `captchatest.php`:

```php
<?php
// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$options = array(
```
