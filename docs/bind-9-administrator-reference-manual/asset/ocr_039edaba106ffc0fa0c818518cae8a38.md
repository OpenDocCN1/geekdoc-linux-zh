# Chapter 6. BIND 9 Configuration Reference

For security reasons, when the "-u" command line option is used, the named.run file is created only after named has changed to the new UID, and any debug output generated while named is starting up and still running as root. If you need to capture this output, you must run the server with the "-g" option and redirect standard error to a file.

Once a channel is defined, it cannot be redefined. Thus you can alter the built-in channels directly, but you can modify the default logging by pointing channels at channels you have defined.

# 6.2.10.2. The category Phrase

There are many categories, so you can send the logs wherever you want, without seeing logs you don't want. If you don't specify a list of channels for a category, then log messages in that category will be sent to the default category instead. If you don't specify a default category, the following "default" is used:

```
category "default" { "default_syslog"; "default_debug"; };
```

As an example, if you want to log security events to a file, but you also want to keep the default behavior. You specify the following:

```
channel "my_security_channel" {
    file "my_security_file";n    severity info;
}
category "security" {
    my_security_channel;
    default_syslog;
    default_debug;
}

```

To discard all messages in a category, specify the null channel:

```
category "xfer-out" { "null"; }
category "notify" { "null"; };
```

Following are the available categories and brief descriptions of the types of log information they contain. More categories may be added in future BIND releases.

| default | The default category defines the logging options for those categories where no specific configuration has been defined. |