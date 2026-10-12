To check the version and see the compile time options, use `mutt -v` like this:

```
$ mutt -v
Mutt 1.4.2.11 (2004-02-12)
Copyright (C) 1996-2002 Michael R. Elkins and others.
Mutt comes with ABSOLUTELY NO WARRANTY; for details type `mutt -vv' .
Mutt is free software, and you are welcome to redistribute it
under certain conditions; type `mutt -vv' for details.
System: Linux 2.6.11.1177_F04 (1686) (using ncursew 5.4)
Compile options:
 -DOMAIN
 -DEBUG
 -HOMEPOOL -USE_SETGID -USE_DOTLOCK -DL_STANDALONE
 +USE_FCNTL -USE_FLOCK
 +USE_POP +USE_IMAP +USE_GSS +USE_SSL +USE_SASL
 +HAVE_REGCOMP -USE_GNU_REGEX
 +HAVE_COLOR +HAVE_START_COLOR +HAVE_TYPEHEAD +HAVE_BKGDDSET
 +HAVE_CURS_SET +HAVE_META +HAVE_RESIZETERM
 +HAVE_PGP -BUFFY_SIZE -EXACT_ADDRESS -SUN_ATTACHMENT
 +ENABLE_NLS -LOCALES_HACK +HAVE_WC_FUNCS +HAVE_LANGINFO_CODESET
 +HAVE_LANGINFO_YESEXPR
 +HAVE_ICONV -ICONV_NONTRANS +HAVE_GETSID +HAVE_GETADDRINFO
 ISPALL="/usr/bin/ispell"
 SENDMAIL="/usr/sbin/sendmail"
 MAILPATH="/var/mail"
 PKGDATADIR="/usr/share/mutt"
 SYSCONFDIR="/etc"
 EXEOSHELL="/bin/sh"
 -MIXMASTER
```

To contact the developers, please mail to `<mutt-dev@mutt.org>`.
To report a bug, please use the flea(1) utility.

If you want to change the options (such as any paths) you will need to recompile mutt from the source code.

The latest versions of mutt, as well as news and information about it, are available at http://www.mutt.org/. mutt is proud to be a bug-free program, but its authors believe it might have a few “fleas”—thankfully, these are few.

The systemwide configuration file is kept at `/etc/Muttrc`, and each user can have his own `~/.muttrc` files. mutt configuration is often an evolving process, as each user attempts to configure this feature-rich mail client.