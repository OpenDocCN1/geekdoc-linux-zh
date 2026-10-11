```
% mysql --set-variable=connect_timeout=10
% mysql -O connect_timeout=10
```

--set-variable and -O are deprecated.

Each program's variables are listed in the program's description in this appendix, and are also displayed in the program's help message (see Section F.1, “Displaying a Program's Help Message”).

# F.2.2 Option Files

Most MySQL programs support option files. These provide a means for storing program options so that you don't have to type them on the command line each time you invoke a program. For binary distributions, you can find sample option files under the MySQL installation directory. If you have a source distribution, look in the support-files directory for the sample files. They have names such as my-huge.cnf, my-large.cnf, and so forth. (The filename suffix is .ini on Windows.)

Any option specified in an option file can be overridden by explicitly specifying the option on the command line with a different value.

MySQL programs that support option files look for them in several locations. However, it is not an error for an option file to be missing. This means you normally must create option files yourself. Option files must be text files, so if you create an option file in a word processor, be sure to save it in plain text format, not in the word processor's native document format.

Under Unix, the option files shown in the following table are read in order if they exist.

| Filename | Contents |
| :--- | :--- |
| /etc/my.cnf | Global options |
| /etc/mysql/my.cnf | Global options (as of MySQL 5.1.15) |
| SYSCONFDIR/my.cnf | Global options |
| MYSQL_HOST/my.cnf | Server-specific options |
| ~/.my.cnf | User-specific options |

In addition, if a file is named with the --defaults-extra-file option, it is read just before ~/.my.cnf. ~ represents the pathname to your home directory. SYSCONFDIR comes from the --sysconfdir option given to configure at MySQL build time. Its default value is the /etc directory under the installation directory compiled in to the distribution. This option file location is used as of MySQL 5.0.21/5.1.10, although until 5.0.53/5.1.22, the file named by this location is read last.