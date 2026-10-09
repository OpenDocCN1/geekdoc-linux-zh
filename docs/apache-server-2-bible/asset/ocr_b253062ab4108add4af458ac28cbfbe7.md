| Apache Programs | Purpose |
| :--- | :--- |
| `htpasswd` | This program is used to create and update user authentication information used in basic HTTP authentication. See Chapter 7 for details. |
| `httpd` | This is the Apache Web server program. |
| `logresolve` | This program converts (resolves) IP addresses from a log file to host names. See Chapter 8 for details. |
| `rotatelogs` | This program rotates Apache logs files when they reach a certain size. See Chapter 8 for details. |

Table 2-5 lists the contents of the `config` directory.

# **Table 2-5**
**Apache config Directory Contents**

| Configuration File | Purpose |
| :--- | :--- |
| `httpd.conf` | This is the Apache configuration file. |
| `httpd-std.conf` | This is the sample copy of the `httpd.conf` file, which is not required by Apache. For new Apache users, this file can act as a means for recovering the default `httpd.conf`. |
| `highperformance.conf` | This is a sample configuration file that shows some pointers for configuring Apache for high performance. |
| `highperformance-std.conf` | This is a sample copy of the `highperformance.conf` file, which is not required by Apache. |
| `magic` | This file stores the magic data for `mod_mime_magic` Apache module. |
| `mime.types` | This file is used to decide which MIME-type headers are sent to the Web client for a given file.

For more information about MIME types, please read RFC 2045, 2046, 2047, 2048, and 2077. The Internet media-type registry is at <ftp://ftp.iana.org/in-notes/iana/assignments/media-types>. |