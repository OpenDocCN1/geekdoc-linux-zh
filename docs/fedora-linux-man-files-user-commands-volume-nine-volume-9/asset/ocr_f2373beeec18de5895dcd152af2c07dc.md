# FILES

*`/etc/sane.d`*  
This directory holds various configuration files. For details, please refer to the manual pages listed below.

*`~/.sane/pass`*  
This file contains lines of the form
user:password:resource
scanimoge uses this information to answer user authorization requests automatically. The file st have `0600` permissions or stricter. You should use this file in conjunction with the `—accept-md5-only` option to avoid server-side attacks. The resource may contain any character but is limited to 127 characters.