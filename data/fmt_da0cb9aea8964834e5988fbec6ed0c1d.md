
```
$ isprime 77
for counter 2, remainder = 1
for counter 3, remainder = 2
for counter 4, remainder = 1
for counter 5, remainder = 2
for counter 6, remainder = 5
for counter 7, remainder = 0
No, 77 is not a prime
```

Listing 12-9: Running the `isprime` script with debug lines uncommented

### Hacking the Script

There are some inefficiencies in the implementation of the mathematical formula in this script that slow it way down. For example, consider the `while` loop conditional. We keep calculating `$(expr $number / 2)` when we can just

calculate that value once and use the calculated value for each subsequent iteration, saving the need to spawn a subshell and invoking `expr` to find out that the value hasn't changed one iota since the last iteration.

There are also some far smarter algorithms to test for prime numbers, and these are worth exploring, including the delightfully named sieve of Eratosthenes, along with more modern formulas such as the sieve of Sundaram and the rather more complicated sieve of Atkin. Check them out online and test whether your phone number (without dashes!) is a prime or not.

## #87 Let's Roll Some Dice

This is a handy script for anyone who enjoys tabletop games, especially role-playing games like Dungeons & Dragons.

The common perception of these games is that they're just a lot of dice rolling, and that's actually accurate. It's all about probabilities, so sometimes you're rolling a 20-sided die and other times you're rolling six 6-sided dice. Dice are such an easy random number generator that a huge number of games use them, whether it's one die, two (think Monopoly or Trouble), or more.

They all turn out to be easy to model, and that's what the script in Listing 12-10 does, letting the user specify how many of what kind of dice are needed, then "rolling" them all, and offering a sum.

### The Code

```
#!/bin/bash
# rolldice--Parse requested dice to roll and simulate those rolls.
#  Examples: d6 = one 6-sided die
#            2d12 = two 12-sided dice
#            d4 3d8 2d20 = one 4-sided die, three 8-sided, and two 20-sided dice

rolldie()
{
    dice=$1
    dicecount=1
    sum=0

    # First step: break down arg into MdN.
    if [ -z "$(echo $dice | grep 'd')" ] ; then
        quantity=1
        sides=$dice
    else
        quantity=$(echo $dice | cut -dd -f1)
        if [ -z "$quantity" ] ; then      # User specified dN, not just N.
            quantity=1
        fi
        sides=$(echo $dice | cut -dd -f2)
    fi

    echo "" ; echo "rolling $quantity $sides-sided die"
    # Now roll the dice...
    while [ $dicecount -le $quantity ] ; do
        roll=$(( ( $RANDOM % $sides ) + 1 ))
        sum=$(( $sum + $roll ))
        echo "  roll #$dicecount = $roll"
        dicecount=$(( $dicecount + 1 ))
    done
    echo I rolled $dice and it added up to $sum
}
while [ $# -gt 0 ] ; do
    rolldie $1
    sumtotal=$(( $sumtotal + $sum ))
    shift
done
echo ""
echo "In total, all of those dice add up to $sumtotal"
echo ""
exit 0
```

Listing 12-10: The `rolldice` script

### How It Works

This script revolves around a simple line of code that invokes the bash random number generator through the expedient shortcut of referencing `$RANDOM` ①. That's the key line: everything else is just window dressing.

The other interesting segment is where the dice description is broken down ②, because the script supports all three of these notations: `3d8`, `d6`, and `20`. This is a standard gaming notation, for convenience: number of dice + d + sides the die should have. For example, `2d6` means two 6-sided dice. See if you can figure out how each is processed.

There's a fair bit of output for such a simple script. You'll probably want to adjust this to your own preferences, but here you can see that the statement is just a handy way to verify that it parsed the die or dice request properly.
