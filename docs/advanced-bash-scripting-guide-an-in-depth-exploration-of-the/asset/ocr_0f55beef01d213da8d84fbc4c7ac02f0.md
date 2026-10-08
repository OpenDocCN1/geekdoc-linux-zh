# Advanced Bash-Scripting Guide

A new, generalized {a..z} brace expansion operator.

```
#!/bin/bash

for i in {1..10}
# Simpler and more straightforward than
+# for i in $(seq 10)
do
    echo -n "$i"
done
echo

# 1 2 3 4 5 6 7 8 9 10
```

```
# Or just .
echo (a..z)      # a b c d e f g h i j k l m n o p q r s t u v w x y z
echo (e..m)      # e f g h i j k l m
echo (z..a)      # z y w v u t s r q p o n l k j i h g f e c b a
# Works backwards, too.
echo (25..30)    # 25 26 27 28 29 30
echo (3..1)       # 3 2 1
echo (X..d)       # X Y Z [ ] a b c d
# Shows (some) of) the ASCII characters between Z and a,
+# but don't rely on this type of behavior because .
echo {1..a}      # 1..a
# Why?
```

# You can tack on prefixes and suffixes.
echo "Number#{1..4}" "..."
# Number #1, Number #2, Number #3, Number #4, ...

```
# You can concatenate brace-expansion sets.
echo {1..3}{x..z} "-..."
# 1x1 + 1y2 + 1z2 + 2x1 + 2y2 + 2z2 + 3x3 + 3y3 + 3z + +
# Generates an algebraic expression.
# This could be used to find permutations.
```

```
# You can nest brace-expansion sets.
echo {a..c},{1..3}
# a b c 1 2 3
# The "comma" operator splices strings together.
```

```
#############################################################################
# (unfortunately, brace expansion does not lend itself to parameterization.
var1=
var2=
echo "${var1}\${var2}" # (1..5)
```

```
# Yet, as Emiliano G. points out, using "eval" overcomes this limitation.
start=0
end=10
for index in \$(eval "\$start..\$end"); do
    echo -n "\$index" # 0 1 2 3 4 5 6 7 8 9 10
```

Chapter 37. Bash, versions 2, 3, and 4

549