```
`-]
telnet> c
Connection closed.
$
:`
```

The session showed how to compute the following:
3 * (4 + 7)

The steps performed in Listing 11.1 are as follows:

+   1. The three values 3, 4, and 7 are first pushed onto the stack.
+   2. The stack is dumped with the dump operation.
+   3. The + operation is performed, which causes 4 + 7 to be evaluated and its result 11 to be placed on the stack in place of the inputs.
+   4. The stack is dumped again using dump. From this, you can see that the values 3 and 11 remain on the stack.
+   5. The multiplication of 3 * 11 is evaluated when * is entered. The result of 33 replaces the input values on the stack.
+   6. The dump operation is performed again to show the stack contents. It shows the single result of 33 on the stack.
+   7. The = operation pops this last value off the stack.
+   8. The dump operation now shows an empty stack.
+   9. The telnet session is closed using CTRL+1 and then the c character followed by a RETURN.

Unary functions supported by the server are shown in Table 11.2.

| Function | Argument | Description |
|---|---|---|
| abs | N/A | The top stack value is replaced with the absolute value of that number. |
| neg | N/A | The top stack value is replaced with the negated value of that number. |
| sqrt | N/A | The top stack value is replaced with the integer square root of that number. |

Note that the unary functions only require one number to exist on the stack. Table 11.3 lists some more advanced functions that the RPN server supports.