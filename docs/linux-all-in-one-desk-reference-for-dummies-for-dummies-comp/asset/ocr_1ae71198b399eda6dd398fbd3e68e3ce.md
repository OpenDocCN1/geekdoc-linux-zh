# Installing the Mail Server

MAILER(smtp)dn1
MAILER(procmail)dn1
dn1 MAILER(cyrusv2)dn1

> If you make changes to the `/etc/mail/sendmail.mc` file, you must generate the `/etc/mail/sendmail.cf` file by running the `sendmail.mc` file through the `m4` macro processor with the following command. (You have to log in as **root**.)

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

The comments also tell you that you need the `sendmail-cf` package to process this file.

From the previous section's description of `m4` macros, you can see that the `sendmail.mc` file uses `define` to create new macros. You can also see the liberal use of `dn1` to avoid inserting too many blank lines into the output.

The other uppercase words (such as `OSTYPE`, `FEATURE`, and `MAILER`) are `sendmail` macros. These are defined in the `.m4` files located in the subdirectories of the `/usr/share/sendmail-cf` directory and are incorporated into the `sendmail.mc` file with the following `include` macro:

```
include(¹usr/share/sendmail-cf/m4/cf.m4¹)dn1
```

The `/usr/share/sendmail-cf/m4/cf.m4` file, in turn, includes the `cfeead.m4` file, which includes other `m4` files, and so on. The net effect is that, as the `m4` macro processor processes the `sendmail.mc` file, the macro processor incorporates many `m4` files from various subdirectories of `/usr/share/sendmail-cf`.

Here are some key points to note about the `/etc/mail/sendmail.mc` file:

+   - **VERSIONID**('setup for Red Hat Linux') macro inserts the version information enclosed in quotes into the output.

+   - **OSTYPE**('linux') specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration.
+     Placing this macro right after the **VERSIONID** macro is customary.

+   - **MAILER**(smtp) describes the mailer. According to instructions in the `/usr/share/sendmail-cf/README` file, **MAILER** declarations are always placed at the end of the `sendmail.mc` file, and **MAILER**(smtp) always precedes **MAILER**(procmail). The mailer **smtp** refers to the SMTP mailer.