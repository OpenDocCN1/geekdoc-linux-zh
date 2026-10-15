```
echo "" ; echo "rolling $quantity $sides-sided die"
# Now roll the dice...
while [ $dicecount -le $quantity ] ; do
  roll=$( ( $RANDOM % $sides ) + 1 )
  sum=$( $sum + $roll )
  echo "  roll #$dicecount = $roll"
  dicecount=$( $dicecount + 1 )
done
echo I rolled $dice and it added up to $sum
}
while [ $# -gt 0 ] ; do
  rolldie $1
  sumtotal=$( $sumtotal + $sum )
  shift
done
echo ""
echo "In total, all of those dice add up to $sumtotal"
echo ""
exit 0
```

Listing 12-10: The rolldice script

# How It Works

This script revolves around a simple line of code that invokes the bash random number generator through the expedient shortcut of referencing $RANDOM ①. That’s the key line: everything else is just window dressing.

The other interesting segment is where the dice description is broken down ②, because the script supports all three of these notations: 3d8, d6, and 20. This is a standard gaming notation, for convenience: number of dice + d + sides the die should have. For example, 2d6 means two 6-sided dice. See if you can figure out how each is processed.

There’s a fair bit of output for such a simple script. You’ll probably want to adjust this to your own preferences, but here you can see that the statement is just a handy way to verify that it parsed the die or dice request properly.

Oh, and the cut invocation ③? Remember that -d indicates the field delimiter, so -dd simply says to use the letter d as that delimiter, as needed for this particular dice notation.

# Running the Script

Let’s start easy: in Listing 12-11, we’ll use two 6-sided dice, as if we were playing Monopoly.