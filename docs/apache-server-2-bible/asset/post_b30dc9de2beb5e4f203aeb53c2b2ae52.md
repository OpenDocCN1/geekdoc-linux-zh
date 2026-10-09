
Here the variable `$keywords` is assigned the value `makesite` because `keywords=makesite` is the query string passed to the server via the GET method. If the Web form's `<form action="form.php">` line is changed to `<form action="form.php" method="POST">`, then the HTTP POST method will be used and the `keywords=makesite` data will be read by the PHP module and automatically made available to the script as the value of the script variable `$keywords`.

If the Web form has multiple fields, all the fields are turned into script variables that are named accordingly. For example, a modified version of `simple_form.html` is shown in Listing 15-6.

### Listing 15-6: modified_simple_form.html

```html
<html>
    <head>
        <title>Simple HTML Form</title>
    </head>
    <body>
        <form action="modified_form.php" method="POST">

            <input type="text" name="keywords" size=30>

            <select name="case">
                <option value="lower">Lower case</option>
                <option value="upper">Upper case</option>
                <option value="dontcare">Don't Care</option>
            </select>

            <input type=submit>

        </form>
    </body>
</html>
```

Here the form has two input fields (`keywords` and `case`).

When this Web form is submitted via the POST method, the `modified_form.php` shown in Listing 15-7 receives all the data.

### Listing 15-7: modified_form.php

```php
<?php
    print "You entered:<br>Keywords: $keywords <br>Case: $case\n";
?>
```

For example, when a user enters `makesite` as the keywords field value and chooses the `dontcare` case option from the drop-down list, the script (`modified_form.php`) displays the following:

You entered:
Keywords: makesite
Case: upper

## Creating sessions with PHP

PHP 4 introduced native session management, which makes creating user sessions simple. This means that you can track a user as the user moves from one page to another. There are two ways to maintain sessions with PHP.

### Using HTTP cookies to create user sessions

This is the default method. To create a session you need to call the `session_start()` function in your PHP page. For example, look at a simple PHP page called `start.php`, which is shown in Listing 15-8.

### Listing 15-8: start.php

```php
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

In the listing you can see two PHP scripts. The first script creates a session by calling the `session_start()` function. It also registers a session variable called `count` by using the `session_register()` function and increments the variable by one. Notice that this script is kept outside the `<html>` tag. This is required because the script sets the session cookie, which is an HTTP header that must come before any contents. The above PHP page assumes that you have output buffering set to Off in `php.ini`. This is the default setting because output buffering causes PHP pages to be slower. If you turn on output buffering by setting `output_buffering = On` in `php.ini`, you can place the PHP scripts anywhere in the page.

The second script simply prints the value of `$count`. Now if you load this page using a Web browser for the first time, the `session_start()` function will create a new HTTP cookie-based session. The cookie sent to your Web browser will have attributes similar to the following:

Cookie Name: `PHPSESSID`
Domain: `192.168.1.100`
Path: `/`
Expires: `End of session`
Secure: `No`
Data: `3de4aa1f73e33dd8f2c8b8d9f69e442e`

The name of the cookie that is sent to the Web browser is `PHPSESSID`. This is the default name set in `php.ini` by using the following line:

`session.name = PHPSESSID`

You can change this to another name if you wish. By default the cookie is valid for only the Web server itself. The sample cookie above shows the domain field of the cookie is set to the IP address of the Web server. If you wish to allow a session cookie to be valid throughout multiple Web servers within your domain, you can set the `session.cookie_domain` directive in the `php.ini` file to the top-level domain name of your Web sites. For example, if you have three Web sites — `corp.domain.com`, `www.domain.com`, and `extranet.domain.com` — and would like the session cookie to be valid in all three of these sites, you can set the `session.cookie_domain` as follows:

`session.cookie_domain = .domain.com`

Notice the leading period before the top-level domain name (`domain.com`); it enables the cookie to be valid over all hosts under this domain.

The default session cookie expires at the end of a session. In other words, when a Web browser is closed, the session cookie is expired. This default behavior is set using the `session.cookie_lifetime` directive in the `php.ini` file. By default it is set to 0, which makes the cookie expire at the end of a session (that is, when the user closes the browser):

`session.cookie_lifetime = 0`

> **Note** PHP does not store any user data within the cookie. The cookie is simply an identifier that points to user data on the server side.

After the first script in Listing 15-8 creates the session, you can easily access the session variable(s) in other pages. For example, Listing 15-9 shows `next_page.php`, which uses the session variable called `$count` created in `start.php`.

### Listing 15-9: next_page.php

```html
<html>
<head><title>Using Session Variables</title>
</head>
<body bgcolor="Red">
<?php
    session_start();
    $count++;
    echo "You have visited this page $count time(s).";
?>

</body>
</html>
```

Any time you want to make use of a current session in a new page you must use the `session_start()` method. This is a bit confusing because it might cause you to think that you are creating a new session. Actually, `session_start()` detects the existing session and uses it. The session variables become available after you have issued the `session_start()` function call. Notice that in this page, we do not place the script before the contents. In other words, we have not placed the script before `<html>` tag because we are no longer issuing a new session, so no new cookie needs to be set. However, this assumes that you have an existing session. To be able to create a new session if one does not exist, move the script outside the content such as the `start.php` page or enable output_buffering in `php.ini`. Also, if you plan to allow session creation on any page, you have to use the `session_register()` method to register variables as shown in `start.php`.

In any page in which you use `session_start()` to select the current session, you can also use `session_register()` to add new variables to the user session.

### Using URL encoding to create user sessions

If you do not want to rely on cookies for maintaining a session, you can use URL-encoded sessions. Setting the `session.use_cookies` directive to 0 in `php.ini` enables this mode. However, unlike the cookie mode, this mode requires that you pass session ID (set via `session_name` in `php.ini`) by using `<?=SID?>` as part of URLs in a page. For example, Listing 15-10 shows a page called `start_url_encoded_session.php`.

### Listing 15-10: start_url_encoded_session.php

```php
<?php
    session_start();
    session_register('count');
    $count++;
?>

<html>
<head><title>Session Management</title>
</head>
<body bgcolor="Red">

<p>
<?php echo "You have visited this page $count time(s)."; ?>
</p>

<p>
<a href="/next_page.php?<?=SID?>">Next Page</a>
</body>
</html>
```

Notice the link titled "Next Page". When the user clicks on this link, the browser requests `/next_page.php` and a query string called `PHPSESSID=session_identifier` is passed to the Web server. Here’s a sample URL request:

`http://207.183.233.21/next_page.php?PHPSESSID=6b2cee31528316080ff88fe81ef800bF8`

This enables the PHP script (`next_page.php`) to know which session the user belongs to and to avoid the use of HTTP cookies. If you wish to maintain the session by using this method, all the links in the PHP page have to have the `<?=SID?>` tag appended to them; otherwise, the session will not be available on every PHP page.

### Terminating a user session

Ending a session is as simple as creating one. For example, the following PHP script will terminate the current user session:

```php
<?php
    session_start();
    $sessionArray = $HTTP_SESSION_VARS;
    session_destroy();

    foreach ($sessionArray as $session_name => $session_value) {
        unset($$session_name);
    }
    unset($sessionArray);
?>
```

Here the `session_start()` is needed to connect the script page to the current session. Then `$sessionArray` is assigned the session variables stored in global variable `$HTTP_SESSION_VARS`. The `session_destroy()` function is called to remove session data from the server. The `foreach` loop explicitly unsets each session variable. Finally, the `$sessionArray` variable is also unset to completely remove the session.
