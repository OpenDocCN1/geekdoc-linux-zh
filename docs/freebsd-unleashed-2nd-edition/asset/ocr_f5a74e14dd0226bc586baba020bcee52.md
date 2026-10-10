# **LISTING 12.3**  Breaking Out of a Loop

```
```
#!/bin/sh
# The following program loops indefinitely.
while true
do
    echo "This line will print forever... But..."
    break
done
echo
echo "The break statement in the loop causes the loop"
echo "to terminate immediately and go the first statement"
echo "after the loop."
```
```

Here's the output of this program:

```
```
This line will print forever... But...
```

The break statement in the loop causes the loop
to terminate immediately and go to the first statement
after the loop.
bash$
```

In a more complex implementation, you could have a loop that waits for some kind of input to be entered from the user's console or from the network; the loop could test continuously for the existence of a file or the value of a variable, and if that condition becomes true, a break could end the loop. Usually it is considered more elegant to write loops whose exit conditions are constructed to react properly on the right kind of input and to avoid a break when possible. In sufficiently complex programs, however, a break can be just what you need to get out of a jam.

# **The continue Statement**

The continue statement causes the loop to immediately jump back to the top and re-evaluate the test condition. Any remaining statements in the loop are not executed. Listing 12.4 is another example that uses the "endless loop" program with a slight modification.

# **LISTING 12.4**  Restarting a Loop Before It Has Ended

```
```
#!/bin/sh
# The following program loops indefinitely.
while true
do
    echo "This line will print forever."
    continue
```
```