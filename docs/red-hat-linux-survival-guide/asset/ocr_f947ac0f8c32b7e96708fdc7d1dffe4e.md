For example, in the following example mailer SMTP is being defined:

```
Msmtp,  P=[IPC], F=mDFMuX, S=11/31, R=21/31, E=\r\n, L=990,
        T=DNS/RFC822/SMTP
```

Typically, you do not need to make any changes in standard mailer definitions.

# H: Define header

An “H” line is used to create a header definition. The syntax for such a line is as follows:

```
H[?flags?]<header name>: <header template>
```

For example, each of the following “H” lines defines a mail header:

```
H??Return-Path: <$g>
HReceived: $?sfrom $s $.$?_($??s$|from $.$_)
    $.by $j ($v/$Z)$?r with $r$. id $i$?u
    for $u; $| 
    $. $b
H?D?Resent-Date: $a
H?D?Date: $a
H?F?Resent-From: $?x$x <$g>$|$g$.
H?F?From: $?x$x <$g>$|$g$.
H?x?Full-Name: $x
H?M?Resent-Message-Id: <$t.$i@$j>
H?M?Message-Id: <$t.$i@$j>
```

You should not make any changes in header definitions.

# O: Set option

The “O” lines are used to set global options for sendmail. The syntax for such a line is as follows:

```
O option name = value
```

Table 13-1 shows all the options available in the latest version (8.9.x) of sendmail.