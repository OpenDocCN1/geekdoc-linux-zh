# Advanced Bash-Scripting Guide

```
then
  until (( t += i) > ${UPPER_LIMIT} ));
    do Primes[t]=; done
fi
```

```
# echo \${Primes[*]}
echo  # Change to original script for pretty-printing (80-col. display)
printf "%s\n" \${Primes[@]}
echo; echo

exit $?
```

Compare these array-based prime number generators with alternatives that do not use arrays, Example A-15 and Example 16-46.

Arrays lend themselves, to some extent, emulating data structures for which Bash has no native support.

# 27-15. Emulating a push-down stack

```
#!/bin/bash
# stack.sh: push-down stack simulation

# Similar to the CPU stack, a push-down stack stores data items
# sequentially, but releases them in reverse order, last-in first-out.

BP=100
  # Base Pointer of stack array.
  # Begin at element 100.

SP=$BP
  # Stack Pointer.
  # Initialize it to "base" (bottom) of stack.

Data=
  # Contents of stack location.
  # Must use global variable,
  # because of limitation on function return range.

  # 100              -- Base Pointer
  # 99               First data item
  # 98               Second data item
  # ...
  # More data
  # Last data item -- Stack pointer
```

```
declare -a stack

push() {
  if [ -z "$1" ]
  then
    return
  fi

  let "SP" -- "$1"  # Bump stack pointer.
}
```

Chapter 27. Arrays