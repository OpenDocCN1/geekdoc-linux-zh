![](bbox=[0.24, 0.09, 0.81, 0.43])

**FIGURE 21-2:** The phpinfo() function output in Ubuntu.

As you can imagine, lots of settings are available in the php.ini configuration file. You may need to tweak some of these php.ini settings on your PHP server:

+   ❓ date.timezone: Defines the time zone of the PHP server. This must use a time zone value defined at https://php.net/manual/en/timezones.php.

+   ❓ display_errors: Defines whether PHP error messages appear on the web page. This feature is extremely handy for development work, but should be disabled for production servers.

+   ❓ error_reporting: Sets the level of error reporting from the PHP server. PHP uses a complicated bit pattern to set what errors to display. It uses labels to indicate the error level, and Boolean bitwise operators to combine the levels; the tilde (¬) indicates the NOT operator. The error levels are:

+   ○ E_ERROR: Fatal run-time errors

+   ○ E_WARNING: Run-time warnings that won't halt the script

+   ○ E_PARSE: Parsing syntax errors

+   ○ E_NOTICE: Script encountered something that could be an error and affect the results

+   ○ E_CORE_ERROR: Fatal error that prevents PHP from starting

+   ○ E_CORE_WARNING: Non-fatal errors during startup

+   ○ E_COMPILE_ERROR: Fatal error while compiling the PHP code