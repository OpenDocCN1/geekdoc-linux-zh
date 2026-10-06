```
$ echo "bat" | awk '/b[ae]+t/(print $0)'
bat
$ echo "bet" | awk '/b[ae]+t/(print $0)'
bet
$ echo "beat" | awk '/b[ae]+t/(print $0)'
beat
$ echo "beet" | awk '/b[ae]+t/(print $0)'
beet
$ echo "beat" | awk '/b[ae]+t/(print $0)'
be
```

This time if either defined in the character class appears, the text matches the pattern.

# Using braces

Curly braces in ERE to allow you to specify a limit on a repeatable regular expression. This is often referred to as an interval. You can express the interval in two formats:

+   - m: The regular expression appears exactly m times.
- n: The regular expression appears at least m times, but no more than n times.

This feature allows you to fine-tune how many times you allow a character (or class) to appear in a pattern.

> CAUTION By default, the gawk program doesn't recognize regular expression intervals. You must specify the --re-interval command line option for the gawk program to recognize regular expression intervals.

Here's an example of using a simple interval of one value:

```
$ echo "bt" | awk --re-interval '/be[1]t/(print $0)'
$
$ echo "bet" | awk --re-interval '/be[1]t/(print $0)'
bet
$ echo "beet" | awk --re-interval '/be[1]t/(print $0)'
$
```

By specifying an interval, you restrict the number of times the character can be present for the string to match the pattern. If the character appears more times, the pattern match fails.

There are lots of times when specifying the lower and upper limit comes in handy:

```
$ echo "bt" | awk --re-interval '/be[1,2]t/(print $0)'
$
$ echo "bet" | awk --re-interval '/be[1,2]t/(print $0)'
bet
```