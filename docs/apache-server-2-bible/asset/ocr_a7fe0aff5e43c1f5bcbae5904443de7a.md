Table 9-1: (continued)

|Server Variable|Explanation|
|---|---|
|TIME_HOUR|Current hour|
|TIME_MIN|Current minute|
|TIME_SEC|Current second|
|TIME_WDAY|Current weekday|
|TIME|Current time|
|API_VERSION|Version of API used|
|IS_SUBREQ|Set if request is a subrequest|

# RewriteEngine

This directive provides you with the on/off switch for the URL rewrite engine in the `mod_rewrite` module. By default, all rewriting is turned off. To use the rewrite engine, you must turn the engine on by setting this directive to `on`.

**Syntax:** `RewriteEngine On | Off`

**Default:** `RewriteEngine Off`

**Context:** Server config, virtual host, per-directory access control file (`.htaccess`)

When enabling URL rewriting per-directory configuration (`.htaccess`) files, you must enable (that is, set to `On`) this directive inside the per-directory configuration file and make sure that you have enabled the following directive in the appropriate context for the directory:

`Options FollowSymLinks`

In other words, if the directory belongs to a virtual host site, make sure that this option is enabled inside the appropriate virtual host container. Similarly, if the directory in question is part of the main server's Web document space, make sure that this option is enabled in the main server configuration.

![](bbox=[0.11, 0.76, 0.18, 0.81])

Enabling rewrite rules in per-directory configurations could degrade the performance of your Apache server. This is because `mod_rewrite` employs a trick to support per-directory rewrite rules, and this trick involves increasing the server's processing load. Therefore, you should avoid using rewrite rules in per-directory configuration files whenever possible.