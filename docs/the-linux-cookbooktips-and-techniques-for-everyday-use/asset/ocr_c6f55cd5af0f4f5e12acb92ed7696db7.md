# 29.2 Outputting a Random Number

@sf (WWW): http://dsl.org/comp/tinvutils/

To output a random number, use random. Give as an argument an integer denoting the range of numbers to be output; random then outputs a random number from 0 to the number you give, minus one.

+   - To output a random number from 0 to 9, type:

```
$ random 10 RET
```

# 29.3 Listing a Sequence of Numbers

Use seq to print a sequence of numbers. This is very useful for getting a listing of numbers to use as arguments, or otherwise passing sequences of numbers to other commands.

To output the sequence from 1 to any number, give that number as an argument.

+   - To output the sequence of numbers from one to seven, type:

```
$ seq 7 RET
```

+   - To output the sequence of numbers from one to negative seven, type:

```
$ seq -7 RET
```

To output the sequence from any one number to another, give those numbers as arguments.

+   - To output the sequence of numbers from nine to zero, type:

```
$ seq 9 0 RET
```

+   - To output the sequence of numbers from negative one to negative twenty, type: