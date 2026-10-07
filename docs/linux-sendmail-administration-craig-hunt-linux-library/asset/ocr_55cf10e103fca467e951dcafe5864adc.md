included in the other two levels plus the operating system definitions that were used during the compile, and the default pathnames for the configuration file and the PID file. For me, debug level 0.1 is the most useful because it provides the Sendmail compiler options and the system identity, which are the pieces of information from this display that I find most helpful.

Debug level 35.9 is interesting because it shows you all of the sendmail.cf variables and the values they have been assigned. Listing 10.16 shows the information displayed by debug level 35.9.

# Listing 10.16 The Output of Debug Level 35.9

```
[root]# sendmail -bt -d35.9
define(deliveryMode as b)
define(* as $=)
define(+ as $=+)
... Many lines deleted ...
define(8 as $8)
define(9 as $9)
define(n as MAILER-DAEMON)
define(v as 8.11.0)
define(w as wren.foobirds.org)
define(j as wren.foobirds.org)
define(m as foobirds.org)
define(k as wren.foobirds.org)
define(b as Sat, 4 Nov 2000 09:33:49-0500)
define(load_avg as 0)
define(opMode as t)
redefine(w as wren)
define(S as )
define(R as )
define(H as )
define(M as )
redefine(n as MAILER-DAEMON)
define(Z as 8.11.0)
redefine(deliveryMode as b)
define(_ as root@localhost)
define(deliveryMode as i)
redefine(deliveryMode as i)
define(i as eA4Exni100755)
```