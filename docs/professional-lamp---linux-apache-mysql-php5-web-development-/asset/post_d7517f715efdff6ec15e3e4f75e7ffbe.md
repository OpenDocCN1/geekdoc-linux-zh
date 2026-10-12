
## Chapter 5

### session.hash_function

In the past, when PHP created a new session and session ID for a user, you had no control over what algorithm was used to create the session ID. With `session.hash_function`, you have the ability to choose between two hash algorithms used to create the session ID.

Setting this option to `0` tells PHP to use `MD5` to hash the session ID (128 bits). If you wanted to use `SHA-1` (160 bits), you would set the value to `1`.

### session.hash_bits_per_character

To further configure the session ID, you can use `session.hash_bits_per_character` to specify how many bits are stored in each character of the session ID when converting to a readable value. The options are as follows:

- `4`: 0-9, a-f
- `5`: 0-9, a-v
- `6`: 0-9, a-z, A-Z, "-", "/"

### zend.zl1_compatibility_mode

The last new configuration setting, `zend.zl1_compatibility_mode`, simply specifies whether or not you want to enable compatibility with Zend Engine 1 (PHP 4).

## PHP Configuration during Runtime

Checking and changing the settings of directives in `php.ini` directly is often a quick and easy solution to monitoring and modifying your installation, but many times you can't bring the server down to make a change, or you need to know a setting while a script is running. The techniques in this part of the chapter will help you make modifications while the server is still running.

## Obtaining Current Runtime Settings

If you need to know the exact version of PHP installed, PHP provides the `phpversion()` function, which returns a `string` listing the full installed version. For example:

```php
<?php

echo "The current version of PHP installed is: " . phpversion();

?>
```

This would output something like the following:

```
The current version of PHP installed is: 5.0.4
```

## Retrieving Configuration Settings

There might be times when a simple version check isn’t enough information, and you require a little more information about the way PHP is configured, but you don’t have access to php.ini directly. To look up runtime configuration settings, you have three main choices: `ini_get()`, `get_cfg_var()`, and `ini_get_all()`.

The first option, `ini_get()`, checks a given string against the current runtime configuration. If a setting matches, it returns the value of that setting; if no match is found, an empty string is returned:

```php
<?php

echo "Error reporting: " . ini_get('error_reporting') . "\n" .
      "Register globals: " . ini_get('register_globals') . "\n" .
      "Nonexistant setting: " . ini_get('nonexistant') . "\n";

?>
```

Running this should produce output similar to the following:

```
Error reporting: 2047
Register globals:
Nonexistant setting:
```

Note that the value of error reporting is actually the numerical equivalent to the constant `E_ALL` in this case. But where’s the value for `register_globals`? When `ini_get()` returns what PHP.ini considers Boolean (off or on, 0 or 1, yes or no), it automatically converts them. Any value of "off" or "no" automatically gets converted to "0"; any value of "yes" or "on" automatically becomes "1".

The second option for retrieving configuration settings, `get_cfg_var()`, behaves almost identically to `ini_get()`, except that it pulls its values directly from php.ini and not the current runtime environment. Unless you’ve changed a configuration variable in your code (more on this later), the value should normally match what is returned by `ini_get()`. Take, for example, the following code:

```php
<?php

echo "Error reporting: " . get_cfg_var('error_reporting') . "\n" .
      "Register globals: " . get_cfg_var('register_globals') . "\n" .
      "Nonexistant setting: " . get_cfg_var('nonexistant') . "\n";

?>
```

Unless a setting was changed in the active script, this code would produce identical output to the following:

```php
<?php

echo "Error reporting: " . ini_get('error_reporting') . "\n" .
      "Register globals: " . ini_get('register_globals') . "\n" .
      "Nonexistant setting: " . ini_get('nonexistant') . "\n";

?>
```

The third way to get configuration information, `ini_get_all()`, acts like `ini_get()` magnified. Instead of specifying a single value to lookup, `ini_get_all()` returns an array containing all the registered configuration options. Its returned values aren't just limited to the current setting either - `ini_get_all()` returns the global value set in php.ini, the current local value as it exists at the moment, and the access level required to change the setting.

Look at this simple example:

```php
<?php
print_r(ini_get_all());
?>
```

You execute this code, and you get something similar to the following:

```
Array
(
  [allow_call_time_pass_reference] => Array
  (
    [global_value] =>
    [local_value] =>
    [access] => 6
  )

  [allow_url_fopen] => Array
  (
    [global_value] => 1
    [local_value] => 1
    [access] => 4
  )

  [always_populate_raw_post_data] => Array
  (
    [global_value] => 0
    [local_value] => 0
    [access] => 6
  )

  [arg_separator.input] => Array
  (
    [global_value] => &
    [local_value] => &
    [access] => 6
  )

...
```

Note this output has been greatly abbreviated - the actual returned array has over 150 different items. Also note that some of the values are empty strings, like the global and local values for `allow_call_time_pass_reference`. When `ini_get_all()` returns each setting, it uses the same value transformation that `ini_get()` performs, in regards to off/on values.

## Extension Information

Now that you can gather information about the runtime settings, it’s time to learn how to check extensions and their properties. PHP provides you with three built-in functions to look up information about loaded extensions.

The first, `extension_loaded()`, simply checks to see if a given extension is loaded. All you need to do is provide the name of the extension, and it will return a Boolean indicating whether or not it is available, like so:

```php
<?php
if (extension_loaded('mysql'))
{
    echo "MySQL is available.\n";
}
else
{
    echo "MySQL is NOT available.\n";
}
if (extension_loaded('fakesql'))
{
    echo "Fake SQL is available.\n";
}
else
{
    echo "Fake SQL is NOT available.\n";
}
?>
```

When you run this, you should see the following:

> MySQL is available.
> Fake SQL is NOT available.

If you need to know the status of more than one extension at a time, PHP gives you `get_loaded_extensions()`. Like `ini_get_all()`, `get_loaded_extensions()` returns an array of all the extensions loaded. Consider the following code:

```php
<?php
print_r(get_loaded_extensions());
?>
```

This should produce output similar to the following, give or take a few extensions, based on your current setup:

```
Array
(
    [0] => xml
    [1] => tokenizer
    [2] => standard
    [3] => SQLite
    [4] => SPL
    [5] => sockets
    [6] => SimpleXML
    [7] => session
    [8] => posix
    [9] => pgsql
    [10] => pcre
    [11] => mysqli
    [12] => mysql
    [13] => iconv
    [14] => gd
    [15] => exif
    [16] => dom
    [17] => ctype
    [18] => calendar
    [19] => bz2
    [20] => bccmath
    [21] => zlib
    [22] => openssl
    [23] => ibxm
)
```

Once you know an extension is available, you might want to know a little more about that particular module. To get a listing of all the functions that an extension provides, use `get_extension_funcs()`. Like some of the previous informational commands, it returns an array of available values, but in this case, it provides a list of functions for a given extension. For example:

```php
<?php
print_r(get_extension_funcs('simplexml'));
?>
```

Running this code should give a list of all the functions provided by the SimpleXML extension:

```
Array
(
[0] => simplexml_load_file
[1] => simplexml_load_string
[2] => simplexml_import_dom
)
```

## Magic Quotes

As mentioned earlier in the chapter, PHP allows a special data handling device called “magic quotes.” When magic quotes are enabled, PHP automatically escapes any special characters — single quote, double quote, NULL — by prefixing them with a backslash, to prevent issues when using the strings in a database.

There are actually two places where PHP can automatically escape strings: input data from a web form or request, or automatically from any function that returns any data at all. Each replacement is controlled by
