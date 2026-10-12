```
Checking MyISAM file: names.MYI
Data records:         5   Deleted blocks:           0
- check file-size
myisamchk: Warning: Size of datafile is: 89 Should be: 204
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
myisamchk: error: Found wrong record at 0
MyISAM-table 'names.MYI' is corrupted
Fix it using switch "-r" or "-o"
```

+   3. To fix a corrupted database, you could run the following command:
+       ```bash
+       # myisamchk -r /var/lib/mysql/allusers/names.MYI
+       - recovering (with keycache) MyISAM-table 'names.MYI'
+       Data records: 5
+       Found wrong stored record at 0
+       Data records: 4
+       ```

+   4. If for some reason the -r options doesn't work, you can try running the myisamchk command with the -o option. This is a slower, older method of repair, but it can handle a few problems that the -r option cannot. Here is an example:
+       ```bash
+       # myisamchk -o /var/lib/mysql/allusers/names.MYI
+       ```

If your computer has a lot of memory, you can raise the key buffer size value on the myisamchk command line, which will lessen the time it takes to check the databases. For example, you could use the following command line:

```
myisamchk -r -O --key_buffer_size=64M *.MYI
```

This would set the key buffer size to 64MB.