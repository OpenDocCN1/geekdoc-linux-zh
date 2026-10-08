# mail, rmail

/usr/bin/vax
/usr/bin/u370

# Description

> Note — The machid family of commands is obsolete. Use uname -p and
uname -m instead.

The following commands return a true value (exit code of 0) if you are using an
instruction that set the command name indicates.

+   - sun true if you are on a Sun system.
- dp11 true if you are on a PDP-11/45 or PDP-11/70.
- sparc true if you are on a computer using a SPARC processor.
- u3b true if you are on a 3B20 computer.
- u3b2 true if you are on a 3B2 computer.
- u3b5 true if you are on a 3B5 computer.
- u3b15 true if you are on a 3B15 computer.
- vax true if you are on a VAX-11/750 or VAX11/780.
- u370 true if you are on an IBM (Reg.) System/370 computer.

The commands that do not apply return a false (non-zero) value. These commands
are often used within make files (see make(1)) and shell scripts (see sh(1)) to increase
portability.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNMcsu |

# See Also

sh(1), test(1), true(1), uname(1), make(1S), attributes(5)

# mail, rmail — Read Mail or Send Mail to Users

# Synopsis

Sending Mail
/usr/bin/mail [-tw] [-m message-type] recipient...
/usr/bin/rmail [-tw] [-m message-type] recipient...