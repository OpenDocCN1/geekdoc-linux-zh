```
i
{
...
}
```

# Program 10.12 Output

```
T
```

The program is fairly self-explanatory. The first expression inside the f loop was omitted because no value had to be initialized before the loop was started. One point worth repeating is that when the a function is called, a pointer to the v array is passed, where it is called a inside the function. Changes to the value of a (as opposed to the values referenced by a ) do not in any way affect the contents of the v array. So, the increment operator that is applied to a is just incrementing a pointer to the array v , and not affecting its contents. (Of course, you know that you can change values in the array if you want to, simply by assigning values to the elements referenced by the pointer.)

# Pointers to Character Strings

One of the most common applications of using a pointer to an array is as a pointer to a character string. The reasons are ones of notational convenience and efficiency. To show how easily pointers to character strings can be used, write a function called c to copy one string into another. If you write this function using normal array indexing methods, the function might be coded as follows:

![](bbox=[0.01, 0.56, 0.3, 0.58])

```
v
{
...
}
```

The f loop is exited before the null character is copied into the t array, thus explaining the need for the last statement in the function.

If you write c using pointers, you no longer need the index variable i. A pointer version is shown in Program 10.13.

# Program 10.13 Pointer Version of c

![](bbox=[0.01, 0.85, 0.3, 0.87])

```
#
v
{
...
```