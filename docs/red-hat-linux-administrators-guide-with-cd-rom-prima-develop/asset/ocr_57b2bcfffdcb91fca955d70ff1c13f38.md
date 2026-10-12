color-codes your logs on the fly. Based on the color scheme, you can tell whether your box is all right from across the room. Depending on which log file you wish to view, you can continuously pipe the tail portion of your `/var/log/messages` file to a terminal window or console display.

To view new messages as they arrive in a certain log file, use the `-t` option with the tail command:

```
# tail -t /var/log/messages
```

You can quickly determine whether your system is logging too much or not enough.

For checking your FTP or Web daemon log files, you can try some Apache log filters of xferlog analyzers, which produce useful information for evaluation. You can customize any sort of log scanner program to suit your particular situation. A wide range of log filters and parsers are available on Linux software pages such as Freshmeat or IceWalkers. I am reluctant to recommend a specific log filter since tastes vary. However, one of the more highly recommended and used log- watching programs is swatch. You can always consult the GNUware CD that came with this book and look up the Administration portion for a variety of dif- ferent tools.

Red Hat is designed to periodically rotate all log files. If you wish to do this yourself, disable the configuration files or edit them to your taste. Keep the files for longer periods of time indefinitely, or clear them out more often than before. If you do insist on periodically cleaning out your log directories, it is better to restart the daemons if any modifications are executed on the logs. For example, if the `/var/log/messages` file is removed or simply deleted altogether, it is prudent to invoke the touch command to re-create an empty messages file and restart the inetd daemon process. The touch command creates an empty file with the same name. Linux will sometimes work if the file is empty, but it is prudent to enter some text if only to let yourself know that the file was created by hand. Under Red Hat this file cannot be empty, as some text must first be entered or piped into the file. After creating the new file, you must edit it by entering a single line of text.