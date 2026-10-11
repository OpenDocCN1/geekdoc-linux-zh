```
do
echo "$friend"
let counter="$counter + 1"
done
done
echo "Good-bye!"
let flag=0
done
```

Indenting a nested loop doesn't affect how Linux processes the commands that the loop contains. Linux processes the commands in the same manner as it does those in the block of code that you don't indent — indenting a loop simply makes the code easier for you (and other programmers) to read and understand.

# Avoiding Endless Loops

All right. You build your masterpiece of a program and fill it with loops inside other loops (nested loops), but it doesn't work correctly. The program keeps breaking out of an outer loop prematurely. It's a mess! This situation results from a common mistake that you want to avoid. Whenever code contains many nested loops, changes that you make within an inner loop are likely to inadvertently make the condition in an outer loop false — breaking your program out of the loop.

```
let flag=1
while [ "$flag" -eq 1 ]
do
for friend in Bob Mary Sue
do
echo "Hello $friend ."
let counter=1
while [ "$counter" -lt 4 ]
do
echo "$friend"
let counter="$counter + 1"
done
done
echo "Good-bye!"
let flag=1
done
```

Here's what's happening.

let flag=1 creates a variable called flag and assigns the value 1 to the variable.

while [ "$flag" -eq 1 ] uses the value of flag as the condition for entering the loop. As long as the value of flag is 1, all the instructions inside the loop execute.