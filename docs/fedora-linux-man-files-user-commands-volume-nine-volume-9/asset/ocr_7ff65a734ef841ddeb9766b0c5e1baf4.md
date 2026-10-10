—log-target=

Set log target. argument st be one of **console**, **journal**, **kmsg**, **journal-or-kmsg**, **null**.

—log-level=

Set log level. As argument this accepts a nirical log level or the well-known (3) syolic nas (lowercase): **erg**, **alert**, **crit**, **err**, **warning**, **notice**, **info**, **debug**.

—log-color=

Highlight important log ssgaes. argument is a boolean value. If the argument is omitted, it defaults to **true**.

—log-location=

Include code location in log ssgaes. This is mostly relevant for debugging purposes. argument is a boolean value. If the argument is omitted it defaults to **true**.

—default-standard-output=, —default-standard-error=

Sets the default output or error output for all services and sockets, respectively. That is, controls the default for **StandardOutput**= and **StandardError**= (see (5) for details). Takes one of **inherit**, **null**, **tty**, **journal**, **journal**+**console**, **syslog**, **syslog**+**console**, **kmsg**, **kmsg**+**console**. If the argument is omitted —default-standard-output= defaults to **journal** and —default-standard-error= to **inherit**.

-h, —help

Print a short help text and exit.

—version

Print a short version string and exit.