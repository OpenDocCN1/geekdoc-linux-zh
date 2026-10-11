To confirm this offset, we will update the `crash` variable in our proof-of-concept to cleanly overwrite EIP with four "B" characters.

```
crash = "\x41" * 4368 + "B" * 4 + "C" * 7
```

Listing 371 - Controlling the EIP register

# 12.3.1.1 Exercises

+   1. Determine the correct buffer offset required to overwrite the return address on the stack.
+   2. Update your stand-alone script to ensure your offset is correct.

# 12.4 Locating Space for Our Shellcode

Next, we must find if there are any registers that point to our buffer at the time of the crash. This step is essential, allowing us to subsequently attempt to identify possible JMP or CALL instructions that can redirect the execution flow to our buffer.

We notice that the ESP register (Figure 227) points to the end of our buffer, leaving only seven bytes of space for shellcode. Furthermore, we cannot increase the overflow buffer size in an attempt to gain more space; even a single byte increase produces a different crash that does not properly overwrite EIP.

![](bbox=[0.35, 0.48, 0.66, 0.86])

Figure 227: ESP points to the end of our buffer leaving only 7 bytes of space for our shellcode