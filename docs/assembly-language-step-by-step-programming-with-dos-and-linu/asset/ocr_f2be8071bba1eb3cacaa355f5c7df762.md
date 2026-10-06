This code tells printf to display the value right-justified within a field 5 characters wide. If you don't put a field width there, printf will simply give the value as much room as its digits require.

# Passing Arguments to printf

The real challenge in working with printf, assuming you understand how it works logically, is knowing how to pass all the arguments it needs to pull off any particular display. Like the Writeln function in Pascal, printf has no set of arguments. It can take as few arguments as one base string, or as many arguments as you need, including additional strings, character values, and numeric values of various sorts.

All arguments to C library functions are passed on the stack. This is done either directly, by pushing the argument value itself on the stack, or indirectly, by pushing a 32-bit pointer to it onto the stack. For 32-bit or 64-bit data, you push the values themselves onto the stack.(The big instruction set win with protected mode is that you can push immediate values onto the stack, something that was impossible prior to the introduction of the 386.) For larger data items such as strings and arrays, you push a pointer to the items onto the stack.

When there are multiple arguments passed to printf, they all have to be pushed onto the stack, and in a very particular and nonintuitive order: from right to left as they would appear if you were to call printf() from the C. The base string is considered the leftmost argument and is always pushed onto the stack. A simple example will tell you here:

```
printf('%d + %d = %d ... for large values of %d,.2,2,5,2);
```

This is a C statement that calls printf(). The base string is enclosed in quotes and is the first argument. After the string are numeric arguments. There must be one numeric value for each of the %d formatting codes embedded in the base string. The order that these items go onto the stack is from the right reading to the left: 2,5,2,2, and finally the base string. In assembly, you'd do it this way:

```
push word 2
push word 5
push word 2
push word 2
push word mathmsg
call printf
add esp,20
```