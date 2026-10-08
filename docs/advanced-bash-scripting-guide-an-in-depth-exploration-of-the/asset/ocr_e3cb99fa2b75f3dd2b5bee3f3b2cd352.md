# Advanced Bash-Scripting Guide

```
local ${!TEST2} # Indirect reference (as above).
echo "Array element VAR1_1: $VAR1_1 from ARRAY21"
nprint
echo
exit 0
```

# As the author of the script notes,
+# "you can easily expand it to create code named-hashes in bash."
# (Difficult) exercise for the reader: implement this.

Arrays implementing a shell script version of the Sieve of Eratosthenes. Of course, a resource-intensive application of this nature should really be written in a compiled language, such as C. It runs excruciatingly slowly as a script.

# Example 27-13. The Sieve of Eratosthenes

```
#!/bin/bash
# sieve.sh (ex68.sh)

# Sieve of Eratosthenes
# Ancient algorithm for finding prime numbers.

# This runs a couple of orders of magnitude slower
+# than the equivalent program written in C.

LOWER_LIMIT=1 # Starting with 1.
UPPER_LIMIT=1000 # Up to 1000.
# (You may set this higher . . if you have time on your hands).

PRIME=1
NON_PRIME=0

let SPLIT=UPPER_LIMIT/2
# Optimization:
# Need to test numbers only halfway to upper limit. Why?

declare -a Primes
# Primes[] is an array.

initialize() {
# Initialize the array.

i=$LOWER_LIMIT
until [ $i -gt $UPPER_LIMIT ];
do
  Primes[$i]=$PRIME
  let i += 1
done
# Assume all array members guilty (prime)
# until proven innocent.\}
```

# Chapter 27. Arrays