# Tip:

If your version of grep supports the -w option, take advantage of it! It's an option to match whole words only. You could, for example, look for all instances of "good" that were used as a whole word by using the regular expression "good", but this has a problem. What about a sentence that ends with the word "good"? It wouldn't match. We can't use the ".*" trick, since that would match "goody", and even "goodness". But if your version of grep will support the -w option, you can use

```
grep -iw "good" files
```

which will find all instances of the word "good" but not other words that have "good" buried within them. If your version of grep doesn't support this option, by the way, it gets much harder. The following should catch virtually all instances, but we suspect that we will have missed something:

```
grep -i "[\'\"\(\[\{good\] \'\,\.\?\!\]\}"

```

Whew. That seems like just a bit too much work for the result. If your version of grep doesn't support the -w option, you might want to ask your system administrator to get a copy of the GNU version of grep that does include this useful option.

# What is a "regular expression"?

We've tossed around the term "regular expression" fairly often throughout this book, and you will continue to see it in any additional reading you do about UNIX, including in the man pages. A regular expression is a string of characters, which may include wildcards and metacharacters, used by one of the text utilities as a search pattern. It looks much like the wildcards used by file utilities, and includes many of the same special characters, but is not quite the same.

A regular expression describes the pattern you are looking for. It can include sets of characters like [aA], which would match both upper and lowercase instances of "A", or wildcards like "*", which matches any number of characters (including zero) but not special characters; or ".", which matches any single character. Two other useful metacharacters are ^ and $, which match the beginning and