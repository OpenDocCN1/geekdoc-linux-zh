The asterisk defines to the C system that the variable `i` is of type `pointer to` `i` . This means that `i` is used in the program to indirectly access the value of one or more integer values.

You have seen how the `&` operator was used in the `&` calls of previous programs. This unary operator, known as the *address operator*, is used to make a pointer to an object in C. So, if `x` is a variable of a particlular type, the expression `&` is a pointer to that variable. The expression `&` can be assigned to any pointer variable, if desired, that has been declared to be a pointer to the same type as `x`.

Therefore, with the definitions of `c` and `i` as given, you can write a statement such as `i` to set up the indirect reference between `i` and `c` . The address operator has the effect of assigning to the variable `i` , not the value of `c` , but a *pointer* to the variable `c` . The link that has been made between `i` and `c` is conceptualized in Figure 10.1 . The directed line illustrates the idea that `i` does not directly contain the value of `c` , but a pointer to the variable `c` .

![](bbox=[0.28, 0.41, 0.72, 0.55])

To reference the contents of `c` through the pointer variable `i` , you use the *indirection operator*, which is the asterisk \*. So, if `x` is defined as type `i` , the statement `*` assigns the value that is indirectly referenced through `i` to the variable `x` . Because `i` was previously set pointing to `c` , this statement has the effect of assigning the value contained in the variable `c` \u2014which is 1 \u2014to the variable `x`.

The previous statements have been incorporated into Program 10.1 , which illustrates the two fundamental pointer operators: the address operator, `&`, and the indirection operator, `*`.

# **Program 10.1 Illustrating Pointers**

Click here to view code image

```
```
#  
i
{
```

```