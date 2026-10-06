```
#!/bin/bash
# random2. Returns a pseudorandom number in the range 0 - 1.
# Uses the awk rand() function.

AWKSCRIPT=' srand(); print rand() '
# Command(s) / parameters passed to awk
# Note that srand reseed awk's random generator.

echo -n "Random number between 0 and 1 = ""
echo | awk "$AWKSCRIPT"

exit 0
```

# # Exercises:

+   # 1) Using a loop construct, print out 10 different random numbers.
# (Hint: you must reseed the "srand() function with a different seed
 in each pass through the loop. What happens if you fail to do this?

+   # 2) Using an integer multiplier as a scaling factor, generate random numbers
 in the range 10 and 100.

+   # 3) Same as exercise #2, above, but generate random integers this time.

# # 9.7. The Double Parentheses Construct

Similar to the let command, the ((...)) construct arithmetic expansion and evaluation. In its simplest form, a=$(( 5 + 3 )) would set "a" to "5 + 3", or 8. However, this double parentheses construct is a mechanism for allowing C-type manipulation of variables in Bash.

Example 9–25. C-type manipulation of variables

```
#!/bin/bash
# Manipulating a variable, C-style, using the ((...)) construct.

echo
(( a = 23 )) # Setting a value, C-style, with spaces on both sides of the ""
echo "a (initial value) = $a"

(( a++ )) # Post-increment 'a', C-style.
echo "a (after a++) = $a"

(( a-- )) # Post-decrement 'a', C-style.
echo "a (after --) = $a"

(( ++a )) # Pre-increment 'a', C-style.
echo "a (after ++a) = $a"

(( --a )) # Pre-decrement 'a', C-style.
echo "a (after --a) = $a"
```

# # 9.7. The Double Parentheses Construct