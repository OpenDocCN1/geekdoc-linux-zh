![](bbox=[0.0, 0.012, 0.26, 0.025])

v
v
If w were declared to be a (signed) `⊆`, the same result would be produced on some computers; on others, the result would be FBBBF711 if the operation were performed as an arithmetic right shift.

It should be noted that the C language does not produce a defined result if an attempt is made to shift a value to the left or right by an amount that is greater than or equal to the number of bits in the size of the data item. So, on a machine that represents integers in 32 bits, for example, shifting an integer to the left or right by 32 or more bits is not guaranteed to produce a defined result in your program. You should also note that if you shift a value by a negative amount, the result is also undefined.

# ## A Shift Function

Now, it’s time to put the left and right shift operators to work in an actual program example, as shown in [Program 11.3](#). Some computers have a single machine instruction to shift a value to the left if the shift count is positive and to the right if the shift count is negative. Now, write a function in C to mimic this type of operation. You can have the function take two arguments: the value to be shifted and the shift count. If the shift count is positive, the value is shifted left the designated number of places; otherwise, the value is shifted right the number of places as specified by the absolute value of the shift count.

```
```
Program 11.3 Implementing a Shift Function
```

Click here to view code_image

```

```
```
/
/
#
u
{
}
i
{
}
```

Program 11.3 Output

```
7
1
4
1
```

```