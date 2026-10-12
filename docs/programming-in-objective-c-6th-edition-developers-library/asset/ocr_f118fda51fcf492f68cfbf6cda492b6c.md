```
}
```

# **Program 12.2 Output**

Click here to view code image

```
r
r
```

The symbolic name `π` is defined as the value 3.141592654 at the beginning of the program. Subsequent use of the name `π` inside the `a` , `c` , and `v` functions has the effect of causing its defined value to be automatically substituted at the appropriate point.

Assignment of a constant to a symbolic name frees you from having to remember the particular constant value every time you want to use it in a program. Furthermore, if you ever need to change the value of the constant (if, perhaps, you find out that you are using the wrong value, for example), you only have to change the value in one place in the program: in the `#` statement. Without this approach, you would have to otherwise search throughout the program and explicitly change the value of the constant whenever it was used.

You might have realized that all the `#` statements you have seen so far (`Y` , `N` , `N` , and `π` ) have been written in capital letters. The reason this is done is to visually distinguish a defined value from a variable. Some programmers adopt the convention that all defined names be capitalized, so that it becomes easy to determine when a name represents a variable and when it represents a defined name. Another common convention is to prefix the defined value with the letter `k`. In that case, the following characters of the name are not capitalized. `k` and `k` are two examples of defined names that adhere to this convention.

# **Program Extendability**

Using a defined name for a constant value helps to make programs more readily extendable. For example, when you define an array, you must specify the number of elements in the array—either explicitly or implicitly (by specifying a list of initializers). Subsequent program statements will likely use the knowledge of the number of elements contained inside the array. For example, if the array `d` is defined in a program as follows:

```
f
```

there is a good chance that you will see statements in the program that use the fact that `d` contains 1,000 elements. For instance, in a `f` loop

```
f
```

you would use the value `1` as an upper bound for sequencing through the elements of the array. A