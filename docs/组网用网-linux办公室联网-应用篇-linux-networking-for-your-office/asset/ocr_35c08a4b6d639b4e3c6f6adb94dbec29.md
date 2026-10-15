password (you can do this by specifying an asterisk [*] in the password field in /etc/passwd or, if you're using shadow passwords, in /etc/shadow). In fact, you can use an existing non-login account, such as nobody.

Because Netatalk requires no authentication for printing, and because it uses only a single username for all printed jobs, accounting of print jobs through Netatalk is effectively impossible. You also cannot restrict access to a printer to certain groups or individuals. In a mixed-operating system (OS) network, however, you can give Macintosh clients access to a different set of printers than you give to Windows or UNIX/Linux clients.

After you've configured your printers, you can type /etc/rc.d/init.d/atalk restart to restart Netatalk, forcing it to reread its configuration files.

# CAUTION

> If you're already sharing files, be sure nobody is using a Netatalk volume before you restart Netatalk. The restart process disconnects all connected Netatalk users, so if people are doing work on shared files, those people might become annoyed at you for disconnecting them and causing them to lose their work!

You might want to check the last few lines of /var/log/messages after you've restarted Netatalk so that you can see its startup messages. You should see something similar to the following, indicating that papd has configured printers for sharing:

```
Aug 21 19:58:42 speaker papd[27276]: register epson360:LaserWriter@*
Aug 21 19:58:48 speaker papd[27276]: register epson:LaserWriter@*
Aug 21 19:58:54 speaker papd[27276]: register epson720:LaserWriter@*
Aug 21 19:59:00 speaker papd[27276]: register hp4000:LaserWriter@*
Aug 21 19:59:00 speaker papd[27301]: child 27301 for "epson" from 41201.173
Aug 21 19:59:01 speaker papd[27301]: lp_print queued
Aug 21 19:59:01 speaker papd[27276]: child 27301 done
```

If you see error messages from papd, or if you don't see the names of printers you thought you'd created, you should go back and check your configuration again. Lack of error messages doesn't necessarily indicate a lack of problems, though. For instance, papd doesn't report an error at this point if a queue name you specified doesn't exist.