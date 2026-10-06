# Advanced Bash-Scripting Guide

```
# Will encrypt quotes in a simple monoalphabetic substitution.
# The result is similar to the "Crypto Quote" puzzles
# seen in the Op Ed Pages of the Sunday paper.
```

```
key=ETAOINSHRDULBCFGJMPVW2XYK
# The "key" is nothing more than a scrambled alphabet.
# Changing the "key" changes the encryption.

# The 'cat "$S@" construction gets input from stdin or from files.
# If using stdin, terminate input with a Control-D.
# Otherwise, specify filename as command-parameter.
```

```
cat "$S@"    tr "a-z"      tr "A-Z" "$key"
             |       to uppercase             encrypt
# Will work on lowercase, uppercase, or mixed-case quotes.
# Passes non-alphabetic characters through unchanged.
```

> # Try this script with something like
# "Nothing needs reforming as other people's habits."
# Mark Twain

```
# Output is:
# "CPHFRCS QF CIIQ MINFERCS EQ FPHIM GIFGUI'Q HETPQ."
# BEEML PZERC
```

```
# To reverse the encryption:
# cat "$S@" | tr "A-Z"
```

This simple-minded cipher can be broken by an average 12nd-year-old
++ using only pencil and paper.

```
exit 0
```

# tr variants

The tr utility has two historic variants. The BSD version does not use brackets (tr a-z A-Z), but the SysV one does tr '[a-z]' '\[A-Z]\'. The GNU version of tr resembles the BSD one, so quoting ranges within brackets is mandatory.

A filter that wraps lines to a specified width. This is especially useful with the -s option, which breaks lines at word spaces (see Example 12–19 and Example A–2).

Simple-minded filter formatter, used as a filter in a pipe to "wrap" long lines of text output.

Example 12–19. Formatted list listing.

```
#!/bin/bash
WIDTH=40                # 40 columns wide.
```

12.4. Text Processing Commands