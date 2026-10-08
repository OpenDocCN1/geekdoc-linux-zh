# 878

# mpss.so.1

```
/usr/lib/lp/locale/C/mp/mp.pro.fp.ps
/usr/lib/lp/locale/C/mp/mp.pro.fp.xpr
```

Default prologue files for Franklin Planner format.

```
/usr/lib/lp/locale/C/mp/mp.pro.tm.ps
/usr/lib/lp/locale/C/mp/mp.pro.tm.xpr
```

Default prologue files for Time Manager format.

```
/usr/lib/lp/locale/C/mp/mp.pro.ts.ps
/usr/lib/lp/locale/C/mp/mp.pro.ts.xpr
```

Default prologue files for Time/System International format.

```
/usr/openwin/lib/locale/classname/print/prolog
/usr/lib/lp/locale/classname/mp/prolog.ps
```

Default locale-specific prologue file as an alternative to the mp.conf file. See "Environment Variables" on page 876 for more detail on the relationship. The structure and format for mp.conf and .xpr files are documented in the International Language Environments Guide. Refer this document if you need to use alternative fonts, including Printer Resident Fonts, or if you want to make changes to output format.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| Availability | SUNwmp |

# See Also

csh(1), mail(1), attributes(5)
International Language Environments Guide

# mpss.so.1 — Shared Object for Setting Preferred Page Size

# Synopsis

```
/usr/lib/lp/mpss.so.1
```

# Description

Use the mpss.so.1 shared object, new in the Solaris 9 Operating Environment, to selectively configure the preferred stack and/or heap page size for launched processes and their descendants. For mpss.so.1 to be enabled, the following string must be present in the environment (ld.so.1(1)) along with one or more MPSS (Multiple Page Size Support) environment variables.

```
LD_PRELOAD=$LD_PRELOAD:mpss.so.1
```