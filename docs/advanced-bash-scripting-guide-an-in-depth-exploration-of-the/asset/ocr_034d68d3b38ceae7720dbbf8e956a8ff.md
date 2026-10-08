# Appendix T. ASCII Table

Traditionally, a book of this sorts has an ASCII Table appendix. This book does not. Instead, here are several short scripts, each of which generates a complete ASCII table.

Example T-1. A script that generates an ASCII table

```
#!/bin/bash
# ascii.sh
# ver. 0.2, reldate 26 Aug 2008
# Patched by ABS Guide author.

# Original script by Sebastian Arming.
# Used with permission (thanks!).

exec >ASCII.txt          # Save stdout to file,
# + as in the example scripts
# reassignment-stdout.sh and upperconv.sh.

MAXNUM=256
COLUMNS=5
OCT=64
OCTSUQ=4
LITTLESPACE=-3
BIGSPACE=-5

i=1 # Decimal counter
o=1 # Octal counter

while [ "$i -lt "$MAXNUM" ]; do # We don't have to count past 400 octal.
  paddi="$i"
  echo -n "$paddi: $BIGSPACE"    # Column spacing.
  padddo="000$"
  echo -ne "\$paddo: $LITTLESPACE"    # Original.
  echo -ne "\$paddo: $LITTLESPACE"    # Fixup.

  echo -n ""
  if (( i % $COLUMNS == 0 )); then # New line.
    echo
  fi
  ((i++,o++))
  # The octal notation for 8 is 10, and 64 decimal is 100.
  (( i % $OCT == 0 )) && ((o+=2))
  (( i % $OCTSUQ == 0 )) && ((o+=20))
done

exit $
# Compare this script with the "pr-asc.sh" example.
# This one handles "unprintable" characters.

Exercise:
# Rewrite this script to use decimal numbers, rather than octal.
```

Example T-2. Another ASCII table script

```
#!/bin/bash
```

Appendix T. ASCII Table