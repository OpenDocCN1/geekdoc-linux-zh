```
(gdb) p xtime  
\u2192  **Test the waters by printing a kernel variable** 
$0 = 1113137355
```

Repeated access to the same variable will not yield refreshed values due to gdb’s cached access. You can force a fresh access by rereading the core file using gdb’s core-file command. Let’s now look at the disassembly of trojan_function():

```
(gdb) x/2i trojan_function 
\u2192  **Disassemble trojan_function** 
0xc019d710 <trojan_function>:
 mov  0xab, %eax
0xc019d715 <trojan_function+5>:
 ret
```

trojan_function() looks laconic when seen in assembly due to compiler optimizations. It’s effectively copying the contents of address 0xab to the EAX register, which holds the return value from functions on x86-based systems. But 0xab does not look like a valid kernel address! Fix the bug by allocating valid memory space to my_variable, recompile, and continue your testing.

# ## JTAG Debuggers

JTAG debuggers use hardware-assist to debug code. You need specialized monitor hardware[^1] and a front-end user interface (some JTAG debuggers use gdb as the front-end) to step through code. JTAG can also be used for purposes other than debugging, such as burning code onto on-board flash memory, as discussed in Chapter 18, “Embedding Linux.” JTAG connectors are common on development boards but are usually not part of production units.

[^1] Some JTAG debuggers work with several processor architectures if you suitably replace the probe that connects the debugger to the target board.

JTAG debuggers usually connect to target hardware via serial port, USB, or Ethernet. With Ethernet, you can remotely access the JTAG debugger, and hence the target board, even if the board itself does not possess a network interface.

Figure 21.2 shows a JTAG-based remote debugging session in action. The JTAG debugger used in this scenario supports a gdb front end. The development host and the JTAG hardware are connected to an Ethernet LAN. The debug serial port on the target hardware is connected to the serial port on the JTAG box. Figure 21.2 achieves remote debugging on the Linux development host using five terminal sessions. Terminal 1 runs gdb, which connects to the JTAG box over the network using telnet:

```
(gdb) target remote 10.1.1.2:1001 \u2192 10.1.1.2 is the IP address of
the JTAG hardware. 1001 is the
JTAG TCP port that listens to
incoming gdb connections
```

![](bbox=[0.25, 0.75, 0.73, 0.77])

[View full size image]