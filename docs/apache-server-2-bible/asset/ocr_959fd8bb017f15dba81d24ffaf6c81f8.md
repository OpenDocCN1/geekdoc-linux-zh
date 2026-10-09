# **Listing 16-1 (*continued*)**

```
```perl
    <p>Process ID: $$ </p>
    <p>Request count: $callCounter </p>
    <hr>
  </body>
</html>
HTML_DOC

    $callCounter++;

    return OK;
}

1;
```
```

The module name is `Development::SimpleAPI`. This tells `mod_perl` to load the module from a subdirectory called `Development` under any of the directories pointed to by `@INC`. Because you created `Development` subdirectory in the `/usr/lib/perl5/site_perl` directory, `mod_perl` will load the `SimpleAPI.pm` module from this directory. This module's purpose is to demonstrate `mod_perl` features.

This module works as follows:

+   The `use strict;` line tells Perl to enforce checking of unsafe constructs. This is a very important line for `mod_perl` modules. For example, if a variable is used in the script without properly declaring it by using a `my` statement, then Perl will complain about it and force you to declare it before using it.

+   The `use Apache::Constants qw(:common);` line simply loads the `Constants.pm` module, which defines a set of constants, such as `OK, REDIRECT`, and `DONE`, that can be used readily in the script.

+   The next line defines the `$callCounter` variable and sets it to zero. This variable is global to the entire script and its value is available to all invocations of the script from within the Apache child process. Also, note that the variable is set to zero after when the module is initially loaded.

+   Next, a `handler()` method is defined. This method is given the Apache request object (`$r`) as a parameter, which it uses to write a `Content-Type` header by using the built-in `send_http_header()` method.

![](bbox=[0.12, 0.65, 0.18, 0.72])