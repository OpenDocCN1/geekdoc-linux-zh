# 376 Lab 8.1: Loops: while and until

LAB 8.1

b) If it's not really needed, why is until included?

```
c) What does the following function print?
function u {
until [[ "$1" == "" ]]
do
  print -- "$1"
  shift
done}
```

# LAB 8.1 ANSWERS

![](bbox=[0.179, 0.503, 0.301, 0.563])

This section gives you some suggested answers to the questions in Lab 8.1, with discussion related to those answers. Your answers may vary, but the most important thing is whether or not your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, we are encouraged to post your answers and to discuss them at the companion web site for this book, located at:

```
http://www.phptr.com/phptrinteractive/
```

# 8.1.1 ANSWERS

After entering the given function into your ~/fun directory, run the following commands:

```
f811 -ac
print a is '\$a_opt\', b is '\$b_opt\', c is '\$c_opt\'
```