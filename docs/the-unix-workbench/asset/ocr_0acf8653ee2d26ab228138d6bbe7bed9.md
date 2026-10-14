echo $? 

# ## 1

Ah-ha! Obviously 3 is not greater than 4, so this false logical expression resulted in an exit status of 1, which is the same exit status as false! Because they have the same exit status [[ 3 -gt 4 ]] and false are essentially equivalent. To quickly test the logical value of a conditional expression, we can use the AND and OR operators so that an expression will print "t" if it's true and "f" if its false:

```
[[ 4 -gt 3 ]] && echo t || echo f
[[ 3 -gt 4 ]] && echo t || echo f
```

# ## t

# ## f

This is a little trick you can use to quickly look at the resulting value of a logical expression.

These binary logical expressions compare two values, but there are also unary logical expressions that only look at one value. For example, you can test whether or not a file exists using the -e logical flag. Let’s take a look at this flag in action:

```
cd ~/Code
[[ -e math.sh ]] && echo t || echo f
```