To determine if two strings are equal, you must explicitly compare the two character strings character by character. If you reach the end of both character strings at the same time, and if all of the characters up to that point are identical, the two strings are equal; otherwise, they are not.
It might be a good idea to develop a function that can be used to compare two character strings, as shown in **Program 9.4**. You can call the function @ and have it take as arguments the two character strings to be compared. Because you are only interested in determining whether the two character strings are equal, you can have the function return a b value of t (or nonzero) if the two strings are identical, and f (or zero) if they are not. In this way, the function can be used directly inside test statements, such as in

Click here to view code image

```
i
```

# Program 9.4 Testing Strings for Equality

Click here to view code image

```
/
#
#b
{


}
i
{


}
```

# Program 9.4 Output

```
0
1
1
```

The @ function uses a w loop to sequence through the character strings $ \backslash and $. The loop is executed so long as the two character strings are equal (@ ) and so long as the end of either string is not reached (@ ).