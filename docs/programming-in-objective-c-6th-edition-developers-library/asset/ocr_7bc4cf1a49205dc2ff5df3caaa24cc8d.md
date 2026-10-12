```
} ```
```

# Program 5.7 Output

Click here to view code image

```
```
E
&
I
```
```

# Program 5.7 Output (Rerun)

Click here to view code image

```
```
E
8
I
```
```

# Program 5.7 Output (Second Rerun)

Click here to view code image

```
```
E
B
I
```
```

The first test that is made after the character is read in determines whether the c variable c is an alphabetic character. This is done by testing if the character is either a lowercase letter or an uppercase letter. The former test is made by the expression

```
```
(
)```
```

which is TRUE if c is within the range of characters ' ' through ' ' ; that is, if c is a lowercase letter. The latter test is made by the expression

```
```
(
)```
```

which is TRUE if c is within the range of characters ' ' through ' ' ; that is, if c is an uppercase letter. These tests work on all computer systems that store characters inside the machine in a format known as ASCII format.

1. *It's better to use routines in the standard library called  and  and avoid the internal representation issue entirely. To do that, you need to include the line # in your program. However, we’ve put this here for illustrative purposes only.*

If the variable c is an alphabetic character, the first i test succeeds and the message I a is displayed. If the test fails, the  clause is executed. This clause determines if the character is a digit. Note that this test compares the character c against the characters ' ' and ' ' and not the integers 0 and 9. This is because a character was read in from the terminal, and the characters ' ' to ' ' are not the same as the numbers 0–9. In fact, on a