Additional trace information for debugging can be found in the /proc/s390dbf/qeth* files. While reporting a problem to IBM support, the content of these files needs to be provided for diagnosis. Figure 4-30 shows the output of trace information for qeth.

```
```
# cat /proc/s390dbf/qeth_trace/hex_ascii
00 01162707622:358305 6 - 00 0000000010e8c182 71 64 69 6e 70 75 75 74 00 | qd input.
00 01162707622:358305 6 - 00 0000000010e8b834 6e 65 78 74 73 6b 62 00 | nextskb.
00 01162707622:358308 6 - 00 0000000010e8b834 6e 65 78 74 73 6b 62 00 | nextskb.
00 01162707622:358308 6 - 00 0000000010e8bdfc 70 74 62 66 70 70 6c 65 | ptbfplen
00 01162707622:358308 6 - 00 0000000010e8be2c 71 75 65 69 6e 62 75 76 | queinbuf
00 01162707622:360123 6 - 01 0000000010e8c182 71 64 69 6e 70 75 75 74 00 | qd input.
00 01162707622:360126 6 - 01 0000000010e8b834 6e 65 78 74 73 6b 62 00 | nextskb.
:
```
```

Figure 4-30 Using information from /proc/s390dbf/qeth_trace/hex_ascii for diagnosis

# Survey in the QDIO layer

The survey in the QDIO layer is essentially checking the trace information from the debugger. Figure 4-32 on page 136 shows a sample output of the /proc/s390dbf/qdio_trace/hex_ascii.

![](bbox=[0.26, 0.73, 0.85, 0.88])

Figure 4-31 Survey in the QDIO layer