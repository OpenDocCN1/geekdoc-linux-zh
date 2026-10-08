# Advanced Bash-Scripting Guide

```
echo
# But, note that in a classic for-loop: for n in [list]
#+ a terminal semicolon is required.

for n in 1 2 3
{
  echo -n "$n"
}

# Thank you, YongYe, for pointing this out.
```

This constructs a test for a condition at the top of a loop, and keeps looping as long as that condition is true (returns a 0 exit status). In contrast to a for loop, a while loop finds use in situations where the number of repetitions is not known beforehand.

```
while [ condition ]
do
  command(s)...
done
```

The bracket construct in a while loop is nothing more than our friend, the test brackets used in an if/then test. In fact, a while loop can legally use the more versatile double-brackets construct (while (( condition ))).

As is the case with for loops, placing the do on the same line as the condition test requires a semicolon.

Note that the test brackets are not mandatory in a while loop. See, for example, the getopts command.

# Example 11-15. Simple while loop

```
#!/bin/bash
var0=0
LIMIT=10
while [ "$var0" -lt "$LIMIT" ];
  # Spaces, because these are "test-brackets" . .
  echo -n "$var0"      # -n suppresses newline.
                        Space, to separate printed out numbers.
  var0=$(expr $var0 + 1) # var0=$((var0+1)) also works.
                        var0=$((var0 + 1)) also works.
                        let "var0 += 1" # other methods also work.
done
echo
```

Chapter 11. Loops and Branches

148