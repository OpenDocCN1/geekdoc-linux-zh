```
10 (five pennies)
 1 (one nickel)
---
-3
 2
```

One nickel is left:

```
10 (five pennies)
 1 (one nickel)
---
-3
12
```

So we get one nickel and two pennies left.

# ## 2.3 Conversion to Pental

Sometimes conversions are unavoidable. For a computer to be able to store a number in binary which is input in decimal, a conversion is needed. Although conversions can be done by searching for a representation which works, there are more efficient methods. Consider the conversion of 207 into base five. To understand this conversion, it may help to look at the answer before we start:

1312 = 1·5³ + 3·5² + 1·5¹ + 2·5⁰

We can see that 5 can be factored out of this sum, except for the 2 at the end:

1312 = (1·5² + 3·5¹ + 1·5⁰)·5 + 2

But this just says what the quotient and remainder of 207 divided by 5 are. Notice that the remainder is our units digit. Furthermore, we can calculate this quotient and remainder using base ten, which is what we have available when we start this conversion:

```
41
5)207
 205
---
 2 and so our ones digit is 2.
```

We have in base ten that:

207 = 41·5 + 2

where again peeking at the answer shows us that:

41 = 1·5² + 3·5¹ + 1·5⁰

The quotient, 41, contains the information needed to get all the other digits. They can be obtained using more divisions:

```
8
5)41
 40
---
 1 and adjoining this digit gives us 12.
```