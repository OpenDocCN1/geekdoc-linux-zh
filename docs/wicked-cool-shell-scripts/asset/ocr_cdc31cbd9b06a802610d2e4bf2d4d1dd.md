calculate that value once and use the calculated value for each subsequent iteration, saving the need to spawn a subshell and invoking expr to find out that the value hasn't changed one iota since the last iteration.

There are also some far smarter algorithms to test for prime numbers, and these are worth exploring, including the delightfully named sieve of Eratosthenes, along with more modern formulas such as the sieve of Sundaram and the rather more complicated sieve of Atkin. Check them out online and test whether your phone number (without dashes!) is a prime or not.

# #87 Let’s Roll Some Dice

This is a handy script for anyone who enjoys tabletop games, especially role-playing games like Dungeons & Dragons.

The common perception of these games is that they’re just a lot of dice rolling, and that’s actually accurate. It’s all about probabilities, so sometimes you’re rolling a 20-sided die and other times you’re rolling six 6-sided dice. Dice are such an easy random number generator that a huge number of games use them, whether it’s one die, two (think Monopoly or Trouble), or more.

They all turn out to be easy to model, and that’s what the script in Listing 12-10 does, letting the user specify how many of what kind of dice are needed, then "rolling" them all, and offering a sum.

# The Code

```
#!/bin/bash
# rolldice--Parse requested dice to roll and simulate those rolls.
#  Examples: d6 = one 6-sided die
#            2d12 = two 12-sided dice
#            d4 3d8 2d20 = one 4-side die, three 8-sided, and two 20-sided dice

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
        quantity=$(echo $dice | @cut -dd -f1)
        if [ -z "$quantity" ] ; then      # User specified dN, not just N.
            quantity=1
        fi
        sides=$(echo $dice | cut -dd -f2)
    fi
```