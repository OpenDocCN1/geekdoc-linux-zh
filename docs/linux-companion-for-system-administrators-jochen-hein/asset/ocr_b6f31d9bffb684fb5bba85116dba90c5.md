```
/var/log/messages \\
 postrotate
 /usr/bin/killall -HUP /sbin/syslogd
endscript
\n/var/log/secure \
 monthly
 rotate 6
 create 640 root admin
 postrotate
 /usr/bin/killall -HUP /sbin/syslogd
endscript
```

**Figure 4.32** An example for single files and logrotate.

Logrotate.d defines two log files in logrotate. An entry starts with the name of the log file, and in brackets holds the configuration for that file. The first example consists of a script that will be executed after rotating the file. In this case syslog gets a signal and opens the newly log file.

The second example is the file /var/log/secure. This file contains security relevant data, so logrotate creates it with special permissions. Only the superuser root has write access, the group admin has read access, everyone else has no access to the file. logrotate keeps six versions and only rotates this file monthly. If you have security problems you may find some information here.

# # 4.8 Shared libraries

The shared libraries used under LINUX are loaded into memory once, even if several programs use them. Thus, the available memory can be used for other things, as additional processes or disk cache. This is why it is still possible to work reasonably even with a LINUX system with as little as 8 Mbytes of RAM. Shared libraries are upwardly compatible as the first digit of the version number (the main or major version) does not change. This makes using a new, improved library relatively easy.

However, the use of shared libraries also has its disadvantages. For example, the required libraries must always be available on the system. If a system administrator has deleted these libraries or if they have been damaged during a system crash, it may become necessary to boot the system with an