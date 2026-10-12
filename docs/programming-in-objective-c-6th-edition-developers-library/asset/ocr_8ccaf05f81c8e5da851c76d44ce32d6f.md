n member of n is then copied into 1 , and because you set this value to point to n , 1 points to n by the end of the second pass through the loop.

When the w loop is executed the third time, the p call displays the value of 3 as contained in n . At that point, 1 (which is actually n ) is copied into 1 , and, because you set this member to the null pointer, the w loop terminates after it has been executed three times.

Trace through the operation of the w loop just discussed, using a pencil and paper, if necessary, to keep track of the values of the various variables. Understanding the operation of this loop is the key to your understanding the operation of pointers in C. Incidentally, it should be noted that this same w loop can be used to sequence through the elements of a list of *any* size, provided the end of the list is marked by the null pointer.

When working with actual linked lists in a program, you will not normally link together list entries that have been explicitly defined like in the program examples in this section. You did that here just to illustrate the mechanics of working with a linked list. In actual practice, you will typically ask the system to give you memory for each new list entry and you will link it into the list while the program is executing. This is done with a mechanism known as *dynamic memory allocation*, and is covered in Chapter 16.

# ## The Keyword const and Pointers

You have seen how a variable or an array can be declared as c to alert the compiler as well as the reader that the contents of a variable or an array will not be changed by the program. With pointers, there are two things to consider: whether the pointer will be changed, and whether the value that the pointer points to will be changed. Think about that for a second. Assume the following declarations:

```
```
c
```
```

The pointer variable c is set pointing to the variable c. If the pointer variable is always set pointing to c, it can be declared as a c pointer as follows:

```
```
c
```
```

(Read this as “c is a constant pointer to a character.”) So, a statement like this:

![](bbox=[0.0, 0.96, 0.4, 0.97])

c causes the GNU C compiler to give a message like this:^2

> 2. Your compiler may give a different warning message, or no message at all.

![](bbox=[0.0, 1.0, 0.4, 1.0])

```
```
f
```
```

Now if, instead, the location pointed to by c will not change *through the pointer variable charPtr*, that can be noted with a declaration as follows:

```
```
c
```
```

(Read this as “c points to a constant character.”) Now of course, that doesn’t mean that the