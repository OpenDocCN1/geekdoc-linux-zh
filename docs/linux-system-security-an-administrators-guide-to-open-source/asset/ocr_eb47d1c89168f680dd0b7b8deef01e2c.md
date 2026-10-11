# Table 14.2 Tripwire Selection Masks

| Selection Mask | Description |
|---|---|
| p | permission and file type |
| i | inode number |
| n | link count |
| u | UID |
| g | GID |
| s | file size |
| a | access timestamp |
| m | modification timestamp |
| c | inode change timestamp |
| 0 | null signature |
| 1 | MD5 (RSA Data Security, Inc., MD5 Message-Digest Algorithm) |
| 2 | Snefru (Xerox Secure Hash Function) |
| 3 | CRC-32 (POSIX1003.2; not useful for security purposes) |
| 4 | CRC-16; not useful for security purposes |
| 5 | MD4 (RSA Data Security, Inc., MD4 Message-Digest Algorithm) |
| 6 | MD2 (RSA Data Security, Inc., MD2 Message-Digest Algorithm) |
| 7 | SHA-1 (NIST Secure Hash Algorithm) |
| 8 | Haval (a 128-bit signature algorithm) |
| 9 | reserved for future use (currently null) |
| +mask | includes the mask in the fingerprint; for example, +pin means to include permission, inode number, and link count |
| -mask | excludes the mask from the fingerprint; for example, -pin means to exclude permission, inode number, and link count |
| R | +pinugsm12-ac3456789 (read-only template, for read-only files and directories) |
| L | +pinug-sacm123456789 (log files template, for files that are both read from and written to) |
| N | +pinugsgamc123456789 (ignore nothing template) |
| E | -pinugsgamc123456789 (ignore everything template) |
| > | for files that increase in size (such as log files); generates an alert only when file is smaller than previously recorded |