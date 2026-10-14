# DO NOT TRUST PRE-COMPILED BINARIES

A system administrator must check the integrity and authenticity of the pre-compiled binaries installed. Pre-installed binaries are software programs and packages that come ready to run on your system. Such precautions must be taken to avoid the installation of binaries that have and may contain Trojan horses. This applies equally to UNIX and Windows, especially when the binaries are downloaded from the Internet. It is also a good idea to educate Windows users to not execute binaries they receive as attachments. Indeed, most of the time, beyond the immediate risk of viruses, there is a risk of installing Trojan horses and other exploits targeted at weaknesses in the operating system and installed applications.

# LIMIT USER PRIVILEGE

One issue that a system administrator has to face during day-to-day activities is granting users the correct privileges. For example, a common issue is giving users sufficient access to printing resources. It is quite common that a printer queue will become blocked due to a file or printer error. However, it usually takes administrator privilege to clear the problem. If the user had administrator access, they could fix it themselves, but giving them administrator access is not a good idea. So, how can you help the user without compromising your security?

Under UNIX, a happy medium is to install a package called sudo. sudo allows the system administrator to grant a user or group of users the rights to use a specific list of commands as if they were the administrator on a specified host. The sudo package is available for just about every UNIX operating system, and can be found at http://www.courtesan.com/sudo.

A list of platforms under which the sudo package has been tested is available at http://www.courtesan.com/sudo/RUNSON.

The installation of this package is easy, but it is strongly recommended that the system administrator pay some extra attention to the many options available. It is generally a good idea to set up the logging option to use syslog and to configure the syslog facility and priority to specific values to include sudo logs in with your other centralized logs. For example, when using the ./configure script:

```
--with-logging=syslog --with-logging=local4 --with-logging=alert
```

Then the /etc/syslog.conf file can be edited to add the following lines: