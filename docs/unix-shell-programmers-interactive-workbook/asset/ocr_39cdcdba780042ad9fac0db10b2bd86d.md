# LAB 5.2 ANSWERS

This section gives you some suggested answers to the questions in Lab 5.2, with discussion related to those answers. Your answers may vary, but the most important thing is whether or not your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and discuss them at the companion web site for this book, located at:

```
http://www.phptr.com/phptrinteractive/
```

# 5.2.1 ANSWERS

+   * What is the purpose of the double dash (--) on line 5051?
  Answer: It marks the end of the options to the set command, and the beginning of the parameters for it.

If the double dash were missing, set would interpret -vu and -do as its own options, and you would get an error message because -d is not a valid option for set.

+   * What would be output if you printed a reference to the special variables # and between lines 5051 and 5052?
  Answer:You would see the number 3 and the values of the three parameters, like the following interaction:
  [5051a] print $#: $@
  3: -vu -do hello
[5052]:

There are four options, but the user chose to write them as two parameters. The third parameter doesn't start with a dash, so it does not contain any options.