# Retrieving Configuration Settings

There might be times when a simple version check isn’t enough information, and you require a little more information about the way PHP is configured, but you don’t have access to php.ini directly. To look up runtime configuration settings, you have three main choices: ini_get(), get_cfg_var(), and ini_get_all().

The first option, ini_get(), checks a given string against the current runtime configuration. If a setting matches, it returns the value of that setting; if no match is found, an empty string is returned:

```
```php
<?php

echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";

?>
```
```

Running this should produce output similar to the following:

Error reporting: 2047
Register globals:
Nonexistant setting:

Note that the value of error reporting is actually the numerical equivalent to the constant E_ALL in this case. But where’s the value for register_globals? When ini_get() returns what php.ini considers Boolean (off or on, 0 or 1, yes or no), it automatically converts them. Any value of “off” or “no” automatically gets converted to “0”; any value of “yes” or “on” automatically becomes “1”.

The second option for retrieving configuration settings, get_cfg_var(), behaves almost identically to ini_get(), except that it pulls its values directly from php.ini and not the current runtime environment. Unless you’ve changed a configuration variable in your code (more on this later), the value should normally match what is returned by ini_get(). Take, for example, the following code:

```
```php
<?php

echo 'Error reporting: ' . get_cfg_var('error_reporting') . "\n" .
     'Register globals: ' . get_cfg_var('register_globals') . "\n" .
     "Nonexistant setting: " . get_cfg_var('nonexistant') . "\n";

?>
```
```

Unless a setting was changed in the active script, this code would produce identical output to the following:

```
```php
<?php

echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";

?>
```
```