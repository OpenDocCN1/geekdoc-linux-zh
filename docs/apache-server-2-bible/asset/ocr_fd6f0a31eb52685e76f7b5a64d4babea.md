Now you need to decide which directory you want to load balance (that is, redirect) between all your Web servers. Typically, this is the CgI directory. For example, the following configuration shows that `/www/mysite/cgi-bin` is to be placed under `mod_backhand`'s control:

```
<Directory "/www/mysite/cgi-bin">
 Backhand byAge
 Backhand byRandom
 Backhand byLoginWindow
 Backhand byLoad
</Directory>
```

+   6. Restart the Apache Web server using `/usr/local/apache/bin/apachectl` restart command.

+   7. Repeat all of the above steps for each Web server.

The `mod_backhand` module creates a daemon process that facilitates gathering and transmission of resource statistics within the Web server cluster. To ensure that this daemon gets a fair share of the system resources, run it with a high priority. For example you can use the `renice` utility found in most Unix and Unix-like systems to set its priority to `-20`.

> **Note** There are other `mod_backhand`-specific tuning issues that you need to consider when using this module. Visit www.backhand.org/mod_backhand for more information.

# # Tuning Web Applications

Web applications are usually the primary performance culprits. Ill-configured or ill-written applications can take servers down to their knees quite easily. It is very important to ensure that your Web applications are not causing problems. This section discusses several tricks that you can use to minimize Web application-related problems. However, because Web applications can be written in many languages using many types of architecture, it is impossible to cover all types of Web applications. So, the discussion here is limited to Perl-based Web application issues.

# ## Speeding up `mod_perl` scripts

The `mod_perl` scripts speed up your Web application performance because they are loaded once and can be run any time without reloading. The following tricks might make your `mod_perl` scripts run even faster or be more performance-friendly.

# Preloading your `mod_perl` modules

If you use a lot of `mod_perl` modules for your Web sites, consider preloading the modules by using the `PerlRequire` directive in `httpd.conf`. Simply, create a Perl script that loads your common modules. For example, following is a simple Perl script called `startup.pl` that loads a few modules that I often use.