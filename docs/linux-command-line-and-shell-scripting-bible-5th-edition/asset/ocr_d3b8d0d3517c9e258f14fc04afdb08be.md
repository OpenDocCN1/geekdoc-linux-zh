This time, if either character defined in the character class appears, the text matches the specified pattern.

# ## Using braces

Curly braces are available in ERE to allow you to specify a limit on a repeatable regular expression. This is often referred to as an *interval*. You can express the interval in two formats:

+   m\—The regular expression appears exactly m times.
+   m, n\—The regular expression appears at least m times, but no more than n times.

This feature allows you to fine-tune exactly how many times you allow a character (or character class) to appear in a pattern.

> **CAUTION**
> By default, gawk doesn’t recognize regular expression intervals. You must specify the `--re-interval` command-line option for gawk to recognize regular expression intervals.

Here’s an example of using a simple interval of one value:

```
$ echo "bt" | gawk --re-interval '/be{1}t/{print $0}'
$
$ echo "bet" | gawk --re-interval '/be{1}t/{print $0}'
bet
$ echo "beet" | gawk --re-interval '/be{1}t/{print $0}'
$
```

By specifying an interval of 1, you restrict the number of times the character can be present for the string to match the pattern. If the character appears more times, the pattern match fails.

Often, specifying the lower and upper limits comes in handy:

```
$ echo "bt" | gawk --re-interval '/be{1,2}t/{print $0}'
$
$ echo "bet" | gawk --re-interval '/be{1,2}t/{print $0}'
bet
$ echo "beet" | gawk --re-interval '/be{1,2}t/{print $0}'
beet
$ echo "beet" | gawk --re-interval '/be{1,2}t/{print $0}'
$
```

In this example, the e character can appear once or twice for the pattern match to pass; otherwise, the pattern match fails.