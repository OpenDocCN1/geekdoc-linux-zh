The elif statement combines the else statement and the if statement and allows you to construct a nested set of if...then...else structures (Figure 13-3). The difference between the else statement and the elif statement is that each else statement must be paired with a fi statement, whereas multiple nested elif statements require only a single fi statement.

The following example shows an if...then...elif control structure. This shell script compares three words that the user enters. The first if statement uses the AND operator (-a) as an argument to test. The builtin returns a true status if the first and second logical comparisons are true (that is, if word1 matches word2 and word2 matches word3). If test returns a true status, the program executes the command following the next then statement and passes control to the fi statement, and script terminates:

```
$ cat if3
echo -n "word 1: "
read word1
echo -n "word 2: "
read word2
echo -n "word 3: "
read word3
if [ "$word1" = "$word2" -a "$word2" = "$word3" ]
then
    echo "Match: words 1, 2, & 3"
elif [ "$word1" = "$word2" ]
then
    echo "Match: words 1 & 2"
elif [ "$word1" = "$word3" ]
then
    echo "Match: words 1 & 3"
elif [ "$word2" = "$word3" ]
then
    echo "Match: words 2 & 3"
elelse
    echo "No match"
fi

$ if3
word 1: apple
word 2: orange
word 3: pear
No match
$ if3
word 1: apple
word 2: orange
word 3: apple
Match: words 1 & 3
$ if3
word 1: apple
word 2: apple
word 3: apple
Match: words 1, 2, & 3
```