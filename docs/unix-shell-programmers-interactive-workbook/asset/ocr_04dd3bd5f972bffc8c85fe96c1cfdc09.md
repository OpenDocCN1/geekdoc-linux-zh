# Chapter 10: Patterns, Expansions, and Substitutions 433

common problems in very natural way. Subpatterns are patterns that you-round with parentheses and precede with one of five character codes:

+   - !(...) The subpattern must occur zero times. (Must not occur).
- ?(...) The subpattern must occur exactly zero or once.
- (...) The subpattern may occur zero or more times.
- @(...) The subpattern must occur exactly once.
- +(...) The subpattern must occur once or more times.

You will see that patterns are used with variables as well as with file names later in this chapter, but for now we'll continue to work with file names. However, you will need some longer file names than the ones used above to get an idea of how subpatterns work.

So remove all the files in your Lab10.1 directory and run the following commands to create a set of file names to work with:

```
for prefix in re un"
  do for root in read reread
    do for suffix in ed ing
      do > $prefix$root$suffix
    done
done
```

![](bbox=[0.028, 0.638, 0.118, 0.715])

The third do command could have used the touch command instead of output redirection to accomplish the same thing, as follows:

touch $prefix$root$suffix

The touch command is slower to run and takes more characters to but will not destroy the contents of a file if it already exists.

# a) How many files did these commands create?