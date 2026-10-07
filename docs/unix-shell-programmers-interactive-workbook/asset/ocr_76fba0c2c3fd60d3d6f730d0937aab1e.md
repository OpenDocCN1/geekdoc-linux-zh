# LAB 8.2 ANSWERS

This section gives you some suggested answers to the questions in Lab 8.2, with discussion related to those answers. Your answers may vary, but the most important thing is whether or not your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and discuss them at the companion web site for this book, located at:

```
http://www.phtpr.com/phtprinterinteractive/
```

# 8.2.1 ANSWERS

+   **What is the name of the control variable of this *for loop***
Answer:The control variable is named *param*.

You can use any simple variable name you like for the control variable. This name is an abbreviation for parameter. Each time through the loop, this variable will be assigned the value of the next element in the list being iterated over.

+   **What does the *loop* test part of this *for loop***
Answer:The loop test part is in "$@".

The loop test part of this type of for loop consists of the keyword followed by the list of values to be iterated over. When there are no more values in the list, the test fails, and the shell skips to the next statement after the done.

+   **What is the word in after the control variable name?**
Answer:It is a keyword, a piece of syntax that tells which type of for loop this is is.

The next token after *for* must be either *in*, the start of an arithmetic expression (see next exercise), or the keyword do.