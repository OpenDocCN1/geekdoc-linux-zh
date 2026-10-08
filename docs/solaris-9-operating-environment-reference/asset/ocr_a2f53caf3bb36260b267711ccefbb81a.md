# 154

# comb, sccs-

```
[ offset_string ]
```

```
/usr/bin/od [-bcCDdFfOoSvXx ] [-A address_base ]
```

```
 [-N count ] [ -t type_string ]
```

```
 [- ] file
```

```
/usr/xpg4/bin/od [-bcCDdFfOoSvXx ] [ - ] file
 [ offset_string ]
```

```
/usr/xpg4/bin/od [-bcCDdFfOoSvXx ] [-A address_base ]
```

```
 [- skip ] [-N count ] [ -t type_string ]
```

```
 [- ]
```

The nroff formatter produces outputs for line printers and CRT displays. To bold characters, it prints the character followed by a backspace and then prints the same character again. Underlining is done by printing an underscore, a backspace, and then the character to be underlined. At times you may need to strip these special effects, such as when you want to use the grep command to search formatted manual pages for a particular string. The following example uses col to get rid of these special effects.

```
castle$% col -b nroff-stripped-output
```

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of col: LC_CTYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type Attribute Value
Availability SUNMesu
CSI Enabled

# See Also

nroff(1), tbl(1), ascii(5), attributes(5), environ(5)

# comb, sccs-comb — Combine SCCS Deltas

# Synopsis

```
/usr.ccs/bin/comb [-os] [-csid-list] [-psid] s.filename.
```