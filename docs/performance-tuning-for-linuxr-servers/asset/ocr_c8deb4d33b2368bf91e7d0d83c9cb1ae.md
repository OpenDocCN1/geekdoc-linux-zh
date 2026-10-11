```
# run.ithrace
-----------------------------
ss: 0x8049a5c 1 push ebp
ss: 0x8049a5d 2 mov ebp, esp
ss: 0x8049a5f 3 sub esp, 0x8
ss: 0x8049a62 5 call 0x420628d8
0 1 4 @ 0 func1:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
ss: 0x8049a64 1 push ebp
ss: 0x8049a6b 2 mov ebp, esp
ss: 0x8049a6d 3 sub esp, 0x8
ss: 0x8049a70 5 call 0x420628d8
0 1 4 @ 0 func2:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
ss: 0x8049a78 1 push ebp
ss: 0x8049a79 2 mov ebp, esp
ss: 0x8049a7b 3 sub esp, 0x8
ss: 0x8049a7e 5 call 0x420628d8
0 1 4 @ 0 func3:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
ss: 0x8049a86 1 push ebp
ss: 0x8049a87 2 mov ebp, esp
ss: 0x8049a89 3 sub esp, 0x8
ss: 0x8049a8c 5 call 0x420628d8
0 1 4 @ 0 func4:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
ss: 0x8049a94 1 push ebp
ss: 0x8049a95 2 mov ebp, esp
ss: 0x8049a97 3 sub esp, 0x8
ss: 0x8049a9a 5 call 0x420628d8
0 1 4 @ 0 func5:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
-----------------------------
```

This report shows the assembler instructions that were executed between the entry and the branch instruction. The report provides a detailed view of what is going on in the system. To relate this back to the actual C code, you would have to compile the C code with the assembler option and calculate the offsets to the assembler instructions to find them in the listing.

If you add the -- option to the post-processing report generator, the output would look similar to the following.

```
# run.ithrace -c
cpu ring instruction_count offset symbolname modulename pid tid_pname To_instruction
0 1 2 @ 0 32 printf:/lib/i686/libc-2.2.93.so 8a1_0_/piperf/bin/ithrace_ RETURN
0 1 5 @ 0 54 main:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 4 @ 0 0 func1:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 4 @ 0 0 func2:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 4 @ 0 0 func3:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 4 @ 0 0 func4:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 4 @ 0 0 func5:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 6 @ 0 0 func6:/piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ CALL
0 1 3 @ 0 50 <pl:>://piperf/bin/ithrace 8a1_0_/piperf/bin/ithrace_ JUMP
0 1 6 @ 0 0 print:/lib/i686/libc-2.2.93.so 8a1_0_/piperf/bin/ithrace_ CALL
0 1 2 2 @ 0 .i686.get_pc_thunk.bx:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ RETURN
0 1 8 @ 11 printf:/lib/i686/libc-2.2.93.so 8a1_0_/piperf/bin/ithrace_ CALL
0 1 7 @ 0 10 vfprintf_internal:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ CALL
0 1 2 2 @ 0 .i686.get_pc_thunk.bx:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ RETURN
0 1 6 @ 0 d_IO_vfprintf_internal:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ CALL
0 1 3 1 @ 470 <pl>:>/lib/i686/libc-2.2.93.so 8a1_0_/piperf/bin/ithrace_ JUMP
0 1 4 @ 0 errno_location:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ CALL
0 1 2 2 @ 0 .i686.get_pc_thunk.bx:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ RETURN
0 1 2 5 @ 9 errno_location:/lib/i686/libc-2.2.93.so
8a1_0_/piperf/bin/ithrace_ RETURN
-----------------------------
```