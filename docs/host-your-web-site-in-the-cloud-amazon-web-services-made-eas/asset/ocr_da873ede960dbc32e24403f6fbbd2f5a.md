```
<?php
: php script
?>
```

# PHP 5.3.0 and Time Zones

If you’re using PHP 5.3.0, there is an important change from previous versions. PHP 5.3.0 will now issue a warning-level log message whenever you use a date-related function without specifying a time zone. PHP has always defaulted to the time zone of the machine it’s running on, but that behavior is now deemed to be unreliable and so the warning is emitted.

To avoid seeing the warning messages you must specify a time zone when using date functions, or else set a default time zone. $ ^{36} $ The easiest way to set a default time zone is to edit your **php.ini** file, specifically the following line:

```
; Defines the default timezone used by the date functions
date.timezone =
```

Uncomment the line and add a valid time zone value. You can find a list of time zone values on the PHP web site. $ ^{37} $ Here’s an example:

```
; Defines the default timezone used by the date functions
date.timezone = America/Los_Angeles
```

# Installing CloudFusion

Many of the examples in this book can be run locally—that is, from your PHP-equipped desktop machine running Windows, Mac OS, or Linux—or remotely on a server or an EC2 instance. Wherever you plan to run them from, that’s where you’ll need to install CloudFusion. Here are the steps involved:

+   1. As at the time of writing, the latest version of CloudFusion was 2.5. You can download it from the project’s web site at http://getcloudfusion.com. Unzip

$ ^{36} $ http://www.php.net/manual/en/migration52.datetime.php

$ ^{37} $ http://www.php.net/manual/en/timezones.php