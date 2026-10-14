Total equivalent gate count for design: 813  
Additional JTAG gate count for IOBs: 1680

Why does the VHDL version of GNOME consume fewer gates than the ABEL version? The typical answers are: (1) The language constructs used to describe the operations of the circuitry are lead to more efficient circuitry in VHDL than ABEL; and (2) The VHDL synthesis algorithms are more sophisticated than those in ABEL. In this case, the organization and method of description for the GNOME microprocessor has been kept very similar between the VHDL and ABEL versions. Therefore, most of the difference in device utilization may lie with the synthesis algorithms themselves.

# Projects

+   1. Hand assemble the following instructions:
+   
+   ```text
+   start: load #0
+   start1: add R5
+           skip_c
+           jump #start
+           add R0
+           skip_z
+           jump #start
+           jump #start1
+   ```
+   
+   Load the opcodes into the program memory. Download the code to your XS40 or XS95 Board and verify its operation.
+   
+   2. You have seen the multiplication flowchart and the associated instructions. Compute the number of instructions that must be executed to multiply 1111 by 1111. Compute the number of instructions that must be executed to multiply 0000 by 0000.
+   
+   3. Create a multiplication program that executes fewer instructions than the program listed in this chapter. Write the complete sequence of instructions and then generate the machine code that meets the following requirements:
+      a. The program must accept two 4-bit numbers from which it will compute their 8-bit product and store it in RAM.
+      b. You can use only 16 or fewer RAM locations in your program: R0, R1, ..., Re, Rf.
+      c. The RAM locations will contain random numbers at the start of the program. You must initialize whatever RAM locations you are using to the correct values. This includes the two numbers you will be multiplying. The multiplicand for this problem is 5 and the multiplier is 14.