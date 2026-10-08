
## Paulo Marcel Coelho Aragoja suggests for-loops as a simpler alternative.
```bash
# for (( last = $number_of_elements - 1 ; last > 0 ; last-- ))
#    By C.Y. Hunt (Thanks!)
# do
#   for (( i = 0; i < last; i++ ))
#     do
#       echo "${Countries[$i]}" "${Countries[$((i+1))]}" \ \
#       exchange $i ($((i+1)))
#     do
# done
```
Since "heaviest" element bubbles to bottom,
we need to do one less comparison each pass.

```bash
echo $count: ${Countries[@]}" Print result array at end of each pass.
let count += 1

done
# End of outer loop
# All done.
```

```bash
exit 0
```

## Is it possible to nest arrays within arrays?

```bash
#!/bin/bash
# "Nested" array.
# Michael Zick provided this example,
# with corrections and clarifications by William Park.
AnArray=($is --inode --ignore-backups --almost-all \ \
--directory --full-time --color=none --time=status \ \
--sort-time -1 ${PWD}) # Commands options.
# Spaces are significant ... and do not quote anything about the above.
```

```bash
SubArray=${AnArray[0]:11:1} ${AnArray[6]:5}
# This array has six elements:
# SubArray=${AnArray[1]} [1]=${AnArray[6]} [2]=${AnArray[7]}
# [3]=${AnArray[8]} [4]=${AnArray[9]} [5]=${AnArray[10]}
```

```bash
# Arrays in Bash are (circularly) linked lists
# of type string (char).
# So, this isn't actually a nested array,
# but it's functionally similar.
```

```bash
echo "Current directory and date last status:"
echo "${SubArray[@]}"
```

```bash
exit 0
```

## Chapter 27. Arrays

# Advanced Bash-Scripting Guide

Embedded arrays in combination with indirect references create some fascinating possibilities

### Example 27-12. Embedded arrays and indirect references

```bash
#!/bin/bash
# embedded-arrays.sh
# Embedded arrays and indirect references.

# This script by Dennis Leeuw.
# Used with permission.
# Modified by document author.

ARRAY1=(
VAR_1=value1
VAR_2=value2
VAR_3=value3
)

ARRAY2=(
VARIABLE="test"
STRING="${VAR1}=value1VAR2=value2VAR3=value3"
ARRAY21=${ARRAY1[*]}
) # Embedded ARRAY1 within this array.

function print () {
OLD_IFS="$IFS" # To print each array element
IFS=$'\n' # on a separate line.
TEST1="ARRAY2[*]"
local ${!TEST1} # See what happens if you delete this line.
# Indirect reference.
# This makes the components of $TEST1
# accessible to this function.

# Let's see what we've got so far.
echo
echo "$TEST1 = ${!TEST1}" # Just the name of the variable.
echo;
echo "${!TEST1} = ${${!TEST1}}" # Contents of the variable.
# That's an indirect
# reference does.

echo
echo ""
echo

# Print variable
echo "Variable VARIABLE: $VARIABLE"

# Print a string element
IFS="$OLD_IFS"
TEST2="${!2}"
local ${!TEST2} # Indirect reference (as above).
echo "String element VAR2: $VAR2 from STRING"

# Print an array element
TEST2="ARRAY21[*]"
```

27: Arrays

# Advanced Bash-Scripting Guide

```bash
local ${!TEST2} # Indirect reference (as above).
echo "Array element VAR1: $VAR1 from ARRAY21"
print
echo
exit 0
```
# As the author of the script notes,
# "you can easily expand it to create hashes in bash."
# (Difficult) exercise for the reader: implement this.
# Arrays implementing a script version of Sieve of Erathenes. Of course, a resource-intensive application of this nature should be written in a compiled language, such as C. It runs excruciatingly slowly as a script.

### Example 27-13. Sieve of Eratosthenes

```bash
#!/bin/bash
# sieve.sh (ex68.sh)
# Sieve of Eratosthenes Ancient algorithm for finding prime numbers.
# This runs a couple of orders of magnitude slower than the equivalent program written in C.

LOWER_LIMIT=1 # Starting with 1.
UPPER_LIMIT=1000 # Up to 1000 (You may set this higher if you have time on your hands).
PRIME=1
NON_PRIME=0

let SPLIT=UPPER_LIMIT/2 # Optimization: test numbers only halfway to upper limit. Why?

declare -a Primes # Primes[] is an array.

initialize() {
# Initialize the array.
i=$LOWER_LIMIT
until [ $i -gt $UPPER_LIMIT ]; do
  Primes[$i]=$PRIME
  let i += 1
done
# Assume all array members are guilty (prime) until proven innocent.
}

print() {
# Print out the members of the Primes[] array tagged as prime.
i=$LOWER_LIMIT
until [ $i -gt $UPPER_LIMIT ]; do
  if [ ${Primes[$i]} -eq $PRIME ]; then
    printf "%8d" "$i" # 8 spaces per number gives nice even columns
  fi
  let i += 1
done
}

sift () {
# Sift out non-primes.
i=$LOWER_LIMIT+1 # Let's start with 2.
until [ $i -gt $UPPER_LIMIT ]; do
  if [ ${Primes[$i]} -eq $PRIME ]; then # Don't bother sieving already sieved (tagged as non-prime).
    t=$i
    while [ $t -le $UPPER_LIMIT ]; do
      let t += 1
      Primes[$t]=$NON_PRIME # Tag as non-prime multiples.
    done
  fi
  let i += 1
done
}

#===========================================
# main ()
# Invoke the functions sequentially.
initialize
sift
print_primes # This is what they call structured programming.
#============================================

echo
exit 0

```
# Code below will not execute, because of 'exit'.
# This improved version of Sieve, by Stephane Chazelas executes somewhat faster.
# Must invoke with command-line argument (limit of primes).

UPPER_LIMIT=$1 # From command-line.
let SPLIT=UPPER_LIMIT/2 # Halfway to max number.

Primes=$(seq $UPPER_LIMIT)

i=1
until (( i += 1 )); do # Need only halfway.
  if [ -n ${Primes[$i]} ]; then
    t=$i
    until (( t += i ) > UPPER_LIMIT); do
      Primes[$t]=
    done
  fi
done
echo ${Primes[*]}
exit $?
```

##### Example 27-14. The Sieve of Eratosthenes, Optimized

```bash
#!/bin/bash
# Optimized Sieve of Eratosthenes
# Script by Jared Mattin, with minor changes by ABS Guide author.
# Used in ABS Guide with permission (thanks him!).

# Based on script in Advanced Bash Scripting Guide.
# http://tdlp.org/abs/html/arrays.html#PRIMES (ex68.sh).
# http://www.cs.hmc.edu/oneill/papers/Sieve-JFP.pdf (reference)
# Check results against http://primes.utm.edu/lists/small/1000.txt

# Necessary but not sufficient would be, e.g., (( $(seq 7919 | wc -l) == 1000 )) && echo 7919 is the thousand prime

UPPER_LIMIT=$1 # Need an upper limit of primes to search.

Primes=$(seq $UPPER_LIMIT)

typeset -i t
Primes[$i-1]=$i # 1 is not a prime.
until (( i += 1 )) > $((UPPER_LIMIT)/i); do # Need only it-way.
  if [ ${Primes[t*(i-1)]} -eq $i ]; then # Why? Obscure, but instructive, use of arithmetic expansion in subscript.
    until (( t += i) > ${UPPER_LIMIT} )); do
      Primes[t]=;
    done
  fi
done
# echo ${Primes[*]}
echo # Change to original script for pretty-printing (80-col. display)
printf "%s\n" "${Primes[@]}"
echo; echo

exit $?
```
Compare these array-based prime number generators with alternatives that do not use arrays, Example A-15 and Example 16-46.

Arrays lend themselves, to some extent, emulating data structures for which Bash has no native support.

## 27-15. Emulating a push-down stack

```bash
#!/bin/bash
# stack.sh: push-down stack simulation

# Similar to the CPU stack, a push-down stack stores data items
# sequentially, but releases them in reverse order, last-in first-out.

BP=100 # Base Pointer of stack.
# Begin at 100.

SP=$BP

declare -a stack # Stack array.

push() {
  if [ -z "$1" ]; then
    return
  fi

  let SP -- "$1" # Bump stack pointer.
  stack[$SP]=$1
}

pop() { # Pop item off stack.
  if [ $SP -eq $BP ]; then # Stack empty?
    return
  fi

  Data=${stack[$SP]}
  let SP += 1 # Bump stack pointer.
  return
}

status_report() { # Find what's happening.
echo "--------------------------------"
echo "--------------------------------"
echo "REPORT"
echo "Stack Pointer = $SP"
echo "Just popped \"\$Data\" off the stack."
echo "--------------------------------"
echo
}

#=================================================
# Now, for some fun.
echo

# See if you can pop anything off empty stack.
pop
status_report
echo

push garbage # Garbage in, garbage.
pop
status_report

value1=23; push $value1
value2=skidoo; push $value2
value3=LAST; push $value3

pop # LAST
status_report
pop # skidoo
status_report
pop # 23 # Last-in, first-out!

# Notice the stack pointer decrements with each push,
# and increments with each pop.
echo
```
