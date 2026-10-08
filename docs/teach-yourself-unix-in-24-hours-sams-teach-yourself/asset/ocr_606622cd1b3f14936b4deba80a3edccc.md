# Table 5.3. Permissions and binary equivalents.

| Permissions String | Binary Equivalent |
| --- | --- |
| --- | 000 |
| -x | 001 |
| -w- | 010 |
| -wx | 011 |
| r-- | 100 |
| r-x | 101 |
| rw- | 110 |
| rwx | 111 |

Knowing how to interpret decimal numbers using the rather complex formula presented earlier, you should not be surprised that the decimal equivalent of any binary number can be obtained by the same technique. Figure 5.6 shows how, with the binary equivalent of the r-x permission.

# Figure 5.6.
Expressing r-x as a single digit.

![](bbox=[0.568, 0.523, 0.703, 0.827])

If r-x is equal to 5, it stands to reason that each of the possible three-character permissions has a single-digit equivalent, and Table 5.4 expands Table 5.3 to include the single-digit equivalents.