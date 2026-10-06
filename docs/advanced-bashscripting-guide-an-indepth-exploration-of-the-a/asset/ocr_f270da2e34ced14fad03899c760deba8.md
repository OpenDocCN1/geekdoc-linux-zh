# Advanced Bash–Scripting Guide

```
let "t2 = nr % 7"
if [ "$t2" -ne 4 ]
then
continue
fi

let "t3 = nr % 9"
if [ "$t3" -ne 5 ]
then
continue
fi

break # What happens when you comment out this line? Why?

done
echo "Number = $nr"
```

A reader sent in the following code snippet.

```
while read LINE
do
  echo $LINE
done < "tail -f /var/log/messages"
```

He wished to write a script tracking changes to the system log file, /var/log/messages. Unfortunately, the above code block hangs and does nothing useful. Fix how it works (hint: rather than redirecting the stdin of the loop), try pipe.

Analyze Example A-8, and reorganize it in a simplified and more logical style. See how many of its variables can be eliminated and try to optimize the speed to speed up its execution time.

Alter the script so that accepts any ordinary ASCII text file as input for its initial "generation". The script will first read the $ROW* characters, and set the occurrences of vowels as "living" cells. Hint: be sure to translate the spaces in the input file to underscore characters.

# I.2. Writing Scripts

Write a script to carry out each of the following tasks.

Easy

Home Directory Listing

I.2. Writing Scripts