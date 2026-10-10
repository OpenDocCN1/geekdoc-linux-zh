# CONFIG FILES

su reads the /etc/default/su and /etc/login.defs configuration files. The following configuration items are relevant for (1):

FAIL_DELAY (nuer)

Delay in seconds in case of an authentication failure. The nuer st be a non-negative integer.

ENV_PATH (string)

Defines the PATH environment variable for a regular user. The default value is /usr/local/bin::/bin::/usr/bin.

ENV_ROOTPATH (string) ENV_SUPATH (string)

Defines the PATH environment variable for root. The default value is /usr/local/sbin::/usr/local/bin::/sbin::/bin::/usr/sbin::/usr/bin.

ALWAYS_SET_PATH (boolean)

If set to yes and —login and —preserve-environ were not specified su initializes PATH.