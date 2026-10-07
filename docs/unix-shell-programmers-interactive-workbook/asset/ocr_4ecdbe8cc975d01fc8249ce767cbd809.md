# Chapter 6: ADVANCED VARIABLE USAGE 307

+   f) What happens if you use 3.7 as a subscript?
Answer:Your interaction should look like the following:
`[6085]: print ${days[3.7]}`
Wednesday
`[6086]:`

It's all right to use the noninteger as the value of a subscript, but the shell silently converts it to an integer by truncating the number. The fraction part is dropped without any rounding. In the present case, the result is the same as if you printed ${days[3 ]} as your reference.

+   g) What happens if you print a reference to days without using any subscript?
Answer:Your interaction should look like the following:
`[6086]: print ${days}`
Sunday
`[6087]:`

If you reference an array without any subscript, you get the value of the first element of the array. This flexibility works the other way around, too: If you already have a scalar variable (that's the name for a variable that isn't an array), you can turn it into an array just by using subscripts to give values to other elements of the array. The value you assigned to the scalar will remain as the value of element zero.

> You can treat the same variable as either a scalar or as an array. This can be convenient, but doing so makes programs hard to understand. Don't use the same variable name as both a scalar and as an array in the function or script.

![](bbox=[0.08, 0.695, 0.145, 0.76])

+   h) What happens if you use the string, hello, as a subscript?
Answer:You could find using an interaction like the following:
`[6087]: print ${days[hello]}`
Sunday
`[6088]:`

You could also have enclosed hello in quotes (either single or double) with the same effect: If you try to use a string where the shell expects you to put a number and the string is not the name of a variable that has been assigned a numeric value, the shell treats the string as the number zero.

# 6.2