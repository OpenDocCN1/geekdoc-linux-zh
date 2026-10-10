(idx=24) 0 (LW-Call) 25020 0 25000
0 25000 0 25000
(idx=28) 0 (LW-Call) 25030 0 25000
0 25000 0 25000
(Note: Many entries have been truncated for brevity)
0 25000 0 25000
sysvec_end:8000240000

# The gateway64_page from a 64-Bit HP-UX 11.0 Kernel

```
Use q4 to find the address of the gateway64_page:
```
q4 > &gateway64_page
    0450000             151552        0x25000
```
```

```
Next, create the listing using adb:
```
$ adb -k /stand/vmunix /dev/mem > /tmp/gateway64_page
25000,0x4c71a
```
```

Listing 4.3 shows the individual promotion blocks for the 64-bit system calls. Note that there is only one block per specific call type.

```
Listing 4.3 # adb -k /stand/vmunix /dev/mem ; 25000,0x4c71a
```
----------
gateway64_page:
gateway64_page:				MTPD r0, sr2
gateway64_page+4:			GATE
gateway64_page+0x000C, r0
gateway64_page+8:			LDIL L\0x340000, r1
gateway64_page+0xC:			BE, N40(sr2, r1)
lw_getpid_gate64:
lw_getpid_gate64:			MTPD r0, sr2
lw_getpid_gate64+4:			GATE
lw_getpid_gate64+0x000C, r0
lw_getpid_gate64+8:			LDIL L\0x3b2000, r1
lw_getpid_gate64+0xC:			BE, N120(sr2, r1)
lw_getuid_gate64:
lw_getuid_gate64:			MTPD r0, sr2
lw_getuid_gate64+4:			GATE
lw_getuid_gate64+0x000C, r0
lw_getuid_gate64+8:			LDIL L\0x3b2000, r1
lw_getuid_gate64+0xC:			BE, N420(sr2, r1)
cnx_lw_pmon_read_gate64:
cnx_lw_pmon_read_gate64:		MTPD r0, sr2
```
```