changes (-i) options. See those options for more information on what is output and when.

This option was added to 3.1.0, so an older rsync on the server side might reject your attempts at fine-grained control (if one or more flags needed to be sent to the server and the server was too old to understand them). See also the “max verbosity” caveat above when dealing with a daemon.

# —debug=FLAGS

This option lets you have fine-grained control over the debug output you want to see. An individual flag na may be followed by a higher nuer, with 0 aning to silence that output, 1 being the default output level, and higher nuerws increasing the output of that flag (for those that support higher levels). Use —debug=help to see all the available flag nas, what they output, and what flag nas are added for each increase in the verbose level. So examples:

```
rsync -avvV --debug=none src/ dest/
rsync -avA --del --debug=del2,acl
src/ dest/
```

Note that so debug sages will only be output when —msgs2stderr is specified, especially those pertaining to I/O and buffer debugging.

This option was added to 3.1.0, so an older rsync on the server side might reject your attempts at fine-grained control (if one or more flags needed to be sent to the server and the server was too old to understand them). See also the “max verbosity” caveat above when dealing with a daemon.

# —msgs2stderr

This option changes rsync to send all its output directly to stderr rather than to send sages to the client side via the protoco (which normally outputs info sages via stdout). This is mainly intended for debugging in order to avoid changing the data sent via the protoco, since the extra protoco data can change what is being tested. Keep in mind that a daemon connection does not have a stderr channel to send sages back to the client side, so if you are doing any daemon-transfer debugging using this option, you should start up a daemon using —no-detach so that you can see the stderr output on the daemon side.

This option has the side-effect of making stderr output get line-buffered so that the rnging of the output of 3 programs happens in a more readable manner.

# -q, —quiet

This option decreases the amount of information you are given during the transfer, notably suppressing information sages from the remote server. This option is useful when invoking rsync from cron.

# —no-motd

This option affects the information that is output by the client at the start of a daemon transfer. This suppresses the sassage-of-the-day (MOTD) text, but it also affects the list of modules that the daemon sends in response to the “rsync host:” request (due to a limitation in the rsync protoco), so omit this option if you want to request the list of modules from the daemon.

# -I, —ignore-tis

Normally rsync will skip any files that are already the sa size and have the sa