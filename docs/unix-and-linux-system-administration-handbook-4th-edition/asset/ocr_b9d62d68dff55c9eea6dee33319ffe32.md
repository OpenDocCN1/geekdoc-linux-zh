Excerpts from configuration files and terminal sessions are shown in a fixed-width font.6 Sometimes, we annotate sessions with italic text. For example:

```
$ grep Bob /pub/phonelist      # Look up Bob's phone number
Bob Knowles 555-2834
Bob Smith 555-2311
```

Outside of these specific cases, we have tried to keep special fonts and formatting conventions to a minimum as long as we could do so without compromising intelligibility. For example, we often talk about entities such as the daemon group or the printer anchor-lw with no special formatting at all.

We use the same conventions as the manual pages for command syntax:

+   - Anything between square brackets ("[" and "]") is optional.
+   - Anything followed by an ellipsis (...) can be repeated.
+   - Curly braces ("{" and "}") mean that you should select one of the items separated by vertical bars ("|").

For example, the specification

```
bork [-x] | [on | off] filename ...
```

would match any of the following commands:

```
bork /etc/passwd
bork -x off /etc/passwd /etc/smartd.conf
bork off /usr/lib/tmac
```

We use shell-style globbing characters for pattern matching:

+   - A star (*) matches zero or more characters.
+   - A question mark (?) matches one character.
+   - A tilde or "twiddle" (~) means the home directory of the current user.
+   - ~user means the home directory of user.

For example, we might refer to the startup script directories /etc/rc0.d, /etc/rc1.d, and so on with the shorthand pattern /etc/rc*.d.

Text within quotation marks often has a precise technical meaning. In these cases, we ignore the normal rules of U.S. English and put punctuation outside the quotes so that there can be no confusion about what's included and what's not.

# 1.8 UNITS

Metric prefixes such as kilo-, mega-, and giga- are defined as powers of 10: one megabuck is 1,000,000 dollars. However, computer types have long poached these prefixes and used them to refer to powers of 2. For example, one "megabyte" of

> 6. It's not really a fixed-width font, but it looks like one. We liked it better than the real fixed-width fonts that we tried. That's why the columns in some examples may not all line up perfectly.

> 7. Solaris 10's default shell for root is the original Bourne shell, which (rather surprisingly) does not understand ~ or ~user notation.