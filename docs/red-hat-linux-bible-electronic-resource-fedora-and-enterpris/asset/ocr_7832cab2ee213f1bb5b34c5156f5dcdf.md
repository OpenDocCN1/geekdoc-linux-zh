however, sendmail will try to determine your computer's domain name on its own. It is recommended that you let sendmail determine the canonical name. The next line configures smart relay and other options:

```
```
CP.
DS
CO @ % !
C..
C[[
```
```

The preceding DS line (set to nothing) indicates that no smart relay host is defined. Although it is more commonly used with UUCP as a transport mechanism, smart relay hosts can also be useful if the machine doesn't have a reliable connection to the entire network (perhaps it's only on a local network). The relay accepts mail from this machine and handles delivering the mail to the appropriate recipients.

The other lines define class macros that become important within the rewriting rules. The CP. and C.. lines define the classes P and ., each of which consists of only a period (.). The CO @ % ! line defines the class O, which lists three characters that are invalid within user names (@, %, and !). The C[[ line defines the class [, which consists of a left bracket.

Next, the FR-o line identifies a file that can be configured to allow mail relaying.

```
```
FR-o /etc/mail/relay-domains
```
```

The preceding line declares file class R, which is a list of hosts to which mail can relayed, stored in the file /etc/mail/relay-domains. The next line has to do with dequoting:

```
```
Kdequote dequote
```
```

The Kdequote line declares the dequote database of class dequote. This is used to remove quotation marks from addresses within the rewriting rules. The next line relates to the way user names and domain names are exposed to the outside world:

```
```
C(E)root
```
```

The preceding class E line (CE root) indicates that mail from the user root should always have the appropriate full host name and domain name, even if other directives indicate that the host name should be masquerading as some other name. Besides class E, class L could be used to list those user names that should receive mail on the local host, even if other directives indicate that all mail should be relayed elsewhere. The class M could be used to indicate which domains should have their host names masqueraded (as set in the following M macro). The class N could be used to indicate host names that should not be masqueraded.

The next lines shown identify sendmail databases:

```
```
Kmailertable hash -o /etc/mail/mailertable.db
Kvirtuser hash -o /etc/mail/virtustertable.db
Kaccess hash -Tc<TMPF> -o /etc/mail/access.db
```
```