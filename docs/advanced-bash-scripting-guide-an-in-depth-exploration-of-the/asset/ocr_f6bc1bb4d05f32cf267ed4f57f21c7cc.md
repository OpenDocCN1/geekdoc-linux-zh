# Advanced Bash-Scripting Guide

```
top=$(echo "scale=9; $principal$interest_rate$term" | bc)
#---------------------------------------
# Standard formula for figuring interest.

echo; echo "Please be patient. This may take a while."

let months=$term - 1
#---------------------------------------
for ((x=$months; x > 0; x--)); do
  bot=$(echo "scale=9; $interest_rate$x" | bc)
  bottom=$(echo "scale=9; $bottom+$bot" | bc)
  bottom=$((bottom + $bot))
done
#---------------------------------------
# Rick Boblique pointed out a more efficient implementation
+# of the above loop, decreases computation time by 2/3.

for ((x=1; x <= $months; x++)); do
  bottom=$(echo "scale=9; $bottom $interest_rate + 1" | bc)
done
```

And then we can use with an even more efficient alternative,
+# one cuts down the run time by 95%!

```
bottom={
  echo "scale=9; $bottom=$interest_rate"
  for ((x=1; x <= $months; x++)); do
    echo 'bottom = $bottom * interest_rate + 1'
  done
  echo 'bottom'
}\ | bc
```

On the other hand, Frank Wang suggests:
bottom=$(echo "scale=9; ($interest_rate$term-1)/($interest_rate-1)\ | bc)

```
# Because
+# algorithm behind the loop
+# is actually a sum of geometric progression series.
+# The sum formula is a(1-q^n)/(1-q),
+# where a is the first element and q= (n+1)/e(n)
+# and n is the number of elements.
```

```
# let payment = $top/$bottom
payment=$(echo "scale=2; $top/$bottom" | bc)
# Use two decimal places for dollars and cents.
```

echo
echo "monthly payment = \$payment" # Echo a dollar sign in front of amount.
echo

```
exit 0
```