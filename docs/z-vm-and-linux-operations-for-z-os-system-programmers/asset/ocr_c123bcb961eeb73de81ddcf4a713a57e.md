For more details about VM dump tools, please refer to z/VM V5r3.0 Diagnosis Guide, GC24-6092, located at: http://publib.boulder.ibm.com/infocenter/zvm/v5r3/index.jsp?topic=/com.ibm.zvm.v53.hcpcl1/getdump.htm

> z/OS analogy: in z/OS, a dedicated dump address space is used to capture dump onto DASD. User-initiated dumps are also saved in the dump address space.

# Traces

The virtual machine tracing facility allows you to follow, or trace, the execution of almost anything that takes place while you are using your virtual machine. For example, you can trace instructions, I/O interrupts, branches, and changes to storage.

Tracing the execution of programs inside a virtual machine can help system operators and support teams to identify the step in a program where execution fails. Example 8-13 shows the output of the TRACE I/O command run in a Linux guest.

# Example 8-13 Tracing I/O in a Linux guest running cat /root/viminfo command

```
00: EXTENT 80C00000 00000000 00080000 00080000
00: EXTENT 1F209FC0 47400010 1F209FF0 0008 47400010 ........
00: LOCATE RECORD 01800001 00080000 00070000 01061000
00: CCW 1F209FC8 85001000 1DE19000 0010 85041000 ........
00: IDAL 0000000000DAAE0000
00: -> 00000000208C790E* SIGA B2740000 0000000000000000 CC 0
00: SCH 0006 DEV 0602
00: FC 00000001 MASK 80000000 00010006
00: -> 0000000000332258* SSCH MASK3300 0000000001F4844 CC 0
00: SCH 0001 DEV 0100
00: CPA 1F209FB8 PRM 010F4800 KEY 0 FPI C2 LPM F0
00: VDEV 0100 CCW 63600020 1F209FD0 000 63600020 ........
00: EXTENT 80C00000 00000000 00080000 00080000
00: CCW 1F209FC0 47400010 1F209FF0 0008 47400010 ........
00: LOCATE RECORD 01800001 00080000 00070000 01061000
00: CCW 1F209FC8 85001000 1DE19000 0010 85041000 ........
00: IDAL 0000000005CCB000
00: -> 00000000208CB852* SIGA B2740000 0000000000000000 CC 0
00: SCH 0006 DEV 0602
00: FC 00000000 MASK 20000000 20000000
00: -> 00000000208CB852* SIGA B2740000 0000000000000000 CC 0
```