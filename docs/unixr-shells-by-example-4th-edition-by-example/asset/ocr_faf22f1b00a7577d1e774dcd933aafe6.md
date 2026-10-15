# EXAMPLE 12.13

(How $* and $0 Differ)

```
1  $ set 'apple pie' pears peaches
2  $ for i in $*
> do
> echo $i
> done
apple
pie
pears
peaches
```

```
3  $ set 'apple pie' pears peaches
4  $ for i in "$*"
> do
> echo $i
> done
apple pie pears peaches
```

```
5  $ set 'apple pie' pears peaches
6  $ for i in $0
> do
> echo $i
> done
apple
pie
pears
peaches
```

```
7  $ set 'apple pie' pears peaches
8  $ for i in "$@"      # At last!!
> do
> echo $i
> done
apple pie
pears
peaches
```

# EXPLANATION

+   1 The positional parameters are set. When the $* is expanded, the quotes are stripped and apple pie becomes two separate words. The for loop assigns each of the words, in turn, to the variable i and then prints the value of i. Each time through the loop, the word on the left is shifted off, and the next word is assigned to i.
+   2 If $* is surrounded by double quotes, all of the words in the list become one single string, and the whole string is assigned to the variable i.
+   3 The positional parameters are set.