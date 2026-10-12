rule is turned off by default. If you want to enable it, set this to `yes` using the `--enable-rule=PARANOID` option in the command line of the configure script.

The `WANTHSREGEX` option is automatically set to default. This specifies that you want to use the regular expression package included with Apache. If you'd rather use your own system's regular expression package, however, set this option to `no` using the `--disable-rule=WANTHSREGEX` option in the command line of the configure script.

# ## Modules configuration options

The default set of modules is added to the standard Apache by using the AddModule lines. The modules are listed in reverse priority order. If you plan to add other modules, do not manually modify this file. Use the configure script to add, remove, enable, or disable modules.

To enable a module that is not already enabled by default, use the `--enable-module=NAME` option. To disable a module, use the `--disable-module=NAME` option. For example, to disable the CGI module, use the following:

```
`./configure --prefix=/usr/local/apache --disable-module=cgi`
```

Or, to enable the user-tracking module, run `configure` as follows:

```
`./configure --prefix=/usr/local/apache --enable-module=usertrack`
```

After you run the configure script successfully using one or more of the options discussed previously, you are ready to compile and install Apache.

# ## Compiling and installing Apache

Compiling and installing Apache is very simple after you have run the configure script. Simply run the `make` command from the top-level directory of your Apache source distribution. If everything goes well, you will not see any error messages. In such a case, you can install Apache by running the `make install` command. If you get error(s) when running `make`, write down the error message(s) and go through the configuration steps again. If you are still having problems, go to the Apache Web site and read the FAQ to find out whether you need to do something else to get Apache