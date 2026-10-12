value cannot be changed by the variable c, which is what c is set pointing to. It means, however, that it won’t be changed with a subsequent statement like this:

Click here to view code image

```
*
```

which causes the GNU C compiler to issue a message like this:

Click here to view code image

```
f
```

In the case in which both the pointer variable and the location it points to will not be changed through the pointer, the following declaration can be used:

Click here to view code image

```
c
```

The first use of c says the contents of the location the pointer references will not be changed. The second use says that the pointer itself will not be changed. Admittedly, this looks a little confusing, but it’s worth noting at this point in the text.3

> 3. The keyword c is not used in every program example where it can be employed; only in selected examples. Until you are familiar with reading expressions such as previously shown, it can make understanding the examples more difficult.

# Pointers and Functions

Pointers and functions get along quite well together. That is, you can pass a pointer as an argument to a function in the normal fashion, and you can also have a function return a pointer as its result.

The first case cited previously, passing pointer arguments, is straightforward enough: The pointer is simply included in the list of arguments to the function in the normal fashion. So, to pass the pointer p from the previous program to a function called p, you can write

```
p
```

```
p
```

Inside the p routine, the formal parameter must be declared to be a pointer to the appropriate type:

```
p
```

Click here to view code image

```
v { }
```

The formal parameter p can then be used in the same way as a normal pointer variable. One thing worth remembering when dealing with pointers that are sent to functions as arguments: The value of the pointer is copied into the formal parameter when the function is called. Therefore, any change made to the formal parameter by the function does not affect the pointer that was passed to the function. But here’s the catch: Although the pointer cannot be changed by the function, the data elements that the pointer references can be changed! Program 10.8 helps clarify this point.

```
p
```

Program 10.8 Using Pointers and Functions

Click here to view code image

/