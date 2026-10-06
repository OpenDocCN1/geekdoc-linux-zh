
# Advanced Bash–Scripting Guide

```bash
initialize ()
{
# Initialize the array.

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do
  Primes[i]=$PRIME
  let i += 1
done
  # Assume all array members guilty (prime)
  # until proven innocent.
}

print_primes ()
{
# Print out the members of the Primes[] array tagged as prime.

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
then
    printf "%8d" "$i"
    # 8 spaces per number gives nice, even columns.
  fi
done

let i += 1
}

sift ()
{
# Sift out the non-primes.

let i=$LOWER_LIMIT+1
# We know 1 is prime, so let's start with 2.

until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
# Don't bother sieving numbers already sieved (tagged as non-prime).
then

    t=$i
    while [ "$t" -le "$UPPER_LIMIT" ]
do
      let t += $i
      Primes[t]=$NON_PRIME
      # Tag as non-prime all multiples.
done
  fi
done
}

let "i += 1"
)

# Invoke the functions sequentially.
initialize
sift
print_primes
# This is what they call structured programming.

echo

exit 0

#------------------------------------
# Code below line will not execute.

# This improved version of the Sieve, by Stephanie Chazelas
# executes somewhat faster.

# Must invoke with command-line argument (limit of primes).
UPPER_LIMIT=$1    # From command line.
let SPLIT=UPPER_LIMIT/2    # Halfway to max number.

Primes=(' $(seq $UPPER_LIMIT) )

i=1
until [[ ((i += 1) > SPLIT ]]; # Need check only halfway.
do
  if [[ -n ${Primes[$i]} ]]];
  then
    t=$i
    until (( ((t += i) > UPPER_LIMIT ))
    do
      Primes[t]=
    done
  fi
done
echo ${Primes[*]}
exit 0
```

Compare this array–based prime number generator with an alternative that does not use arrays. Example A-14.

--- Arrays lend themselves, to some extent, emulating data structures for which Bash has no native support.

## Example 26–6. Emulating a push–down stack

```bash
#!/bin/bash
# stack.sh: push-down stack simulation
```

```bash
# Similar to the CPU stack, a push-down stack stores data items
# sequentially, but releases them in reverse order, last-in first-out.

BP=100            # Base Pointer of stack array.
                   # Begin at element 100.
SP=$BP           # Stack Pointer.
                   # Initialize it to "base" (bottom) of stack.
Data=             # Contents of stack location.
                   # Must use local variable,
                   # because of limitation on function return range.
declare -a stack

push() {
  if [ -z "$1" ]  # Push item on stack.
  then
    return
  fi

  let SP --= 1      # Bump stack pointer.
  stack[$SP]=$1
  return
}

pop() {           # Pop item off stack.
  Data=            # Empty data item.
  if [ "$SP" -eq "$BP" ]  # Stack empty?
  then
    return
  fi
  # This also keeps SP from getting past 100,
  # + prevents a runaway stack.
  Data=${stack[$SP]}
  let SP += 1       # Bump stack pointer.
  return
}

status_report() {
  # Find out what's happening.
  echo "------------------------------------------------"
  echo "REPORT"
  echo "Stack Pointer = $SP"
  echo "Just popped \"$Data\" off the stack."
  echo "------------------------------------------------"
  echo
}

# ==================================================
# Now, for some fun.
echo

# See if you can pop anything empty stack.
pop
status_report

echo

push garbage
pop
status_report # Garbage in, garbage out.
value1=23; push $value1
value2=skidoo; push $value2
value3=FINAL; push $value3

pop # FINAL
status_report
pop # skidoo
status_report
pop # 23
status_report # Last-in, first-out!
```

# Notice how the stack pointer decrements with each push
# + increments with each pop.

```bash
echo
====================================================
```

# Exercises:

- 1) Modify the "push()" function to permit pushing multiple element on the stack with a single call.
- 2) Modify the "pop()" function to permit popping multiple element from the stack with a single call.
- 3) Using this script as a jumping-off point, write a stack-based calculator.

Fancy manipulation of array "scripts" may require intermediate variables. For projects involving this, again consider a more powerful language, such as Perl or C.

## Example 26–7. Complex array application: Exploring a weird series

```bash
#!/bin/bash

# Hofstadter's notorious "Q-series":
# Q(1) = 1
# Q(2) = 1
# Q(n) = Q(n-1) + Q(n-2), for n>2
# This is a "chaotic" series with strange and unpredictable behavior.
# The first 20 terms of the series are:
# 1 2 3 4 5 6 8 8 9 10 11 12

LIMIT=100 # Number of terms to calculate
LINEWIDTH=20 # Number of terms per line

Q[1]=1 # First term of series.
Q[2]=1 # Second term of series.

for ((n=3; n<LIMIT; n++))
do
  Q[n]=$(( Q[n-1] + Q[n-2] ))
  echo -n "${Q[n]} "
  if [ $((n % LINEWIDTH)) -eq 0 ]; # Format output.
  then
    echo # Break lines into neat chunks.
  fi
done
exit 0

# This is an iterative implementation of the Q-series left as an exercise.
# The more intuitive recursive implementation is
Warning: calculating this series recursively takes a very long time.
```

Bash supports only one-dimensional arrays, however a little trickery permits simulating multi-dimensional ones.

## Example 26–8. Simulating a two-dimensional array, then tilting it

```bash
#!/bin/bash
# Simulating a two-dimensional array

# A two-dimensional array stores rows sequentially.
Rows=5
Columns=5

declare -a alpha      # char alpha [Rows][Columns];
                      # Unnecessary declaration.

load_alpha ()
{
    local rc=0
    local index
for i in A B C D E F G H I J K L M N O P Q R S T U W X Y
do
    local row=$(expr rc / Columns)
    local column=$(expr rc % Columns)
    let "index" = $row * Columns + $column
    alpha[$index]=$i      # alpha[row][column]
    let rc += 1
done

# Simpler would be
#     declare -a alpha={A B C D E F G H I J K L M N O P Q R S T U V W X Y}
# but this simpler lacks the "flavor" of a two-dimensional array.
```

```bash
print_alpha ()
{
    local row=0
    local index
}while [ "$row" -lt "$Rows" ];
do
    # Print out in "row order"
    # columns vary
    # while row (outer loop) remains the same
    local column=0
    while [ "$column" -lt "$Columns" ];
    do
        let index=$(expr $row * Rows + column)
        echo -n "${alpha[$index]}"  # alpha[row][column]
        let "column += 1"
    done
    let "row += 1"
done
```

> # The simpler equivalent is
# echo ${alpha[*]} | xargs -n $Columns

filter ()
{
    echo -n ""      # Filter negative array indices.
    #               Provides the tilt.
}

if [[ "$1" -ge 0 && "$1" -lt "$Rows" && "$2" -ge 0 && "$2" -lt "$Columns" ]];
then
let index=$1 * Rows + "$2"
# Now, print rotated.
echo -n "${alpha[$index]}"  # alpha[row][column]
fi
```

```bash
rotate () # Rotate the array "balance" on its lowerthand corner.
local row
local column
for ((row = Rows; row > -Rows; row-- ))  # Step through the array backwards
do
  for ((column = 0; column < Columns; column++))
  do
    if [ "$row" -ge 0 ]
    then
      let t1=$column $row
      let t2=$column
    else
      let t1=$column
      let t2=$column + $row
    fi

    filter $t1 $t2  # Filter out negative array indices.
  done
  echo; echo
done
```

# Array rotation inspired by examples (pp. 143-146) in
# "Gödel, Escher, Bach: An Eternal Braid"
# (see bibliography).


------------------------------------------------------
load_alpha      # Load the array.
print_alpha     # Print it out.
rotate          # Rotate 45 degrees counterclockwise.
------------------------------------------------------
```
