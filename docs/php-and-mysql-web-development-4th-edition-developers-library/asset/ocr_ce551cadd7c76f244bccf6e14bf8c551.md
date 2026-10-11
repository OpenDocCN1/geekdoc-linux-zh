1056  Appendix F  MySQL Program Reference

+     - `--sort-records=n,-R n`  
+       
+       Sorts data rows according to the order in which rows are listed in index n. Subsequent retrievals based on the given index should be faster. The first time you perform this operation on a table, it may be very slow because your rows will be unordered. `ALTER TABLE ... ORDER BY` accomplishes the same thing as `--sort-records`, and normally will be faster.

+     - `--sort-recover,-n`  
+       
+       Forces sorted recovery even if the temporary file necessary to perform the operation would become quite large.

+     - `--start-check-pos=n`  
+       
+       The position n at which to begin reading the data file. This option is used only for debugging.

+     - `--tmpdir=dir_name,-t dir_name`  
+       
+       The pathname of the directory to use for temporary files. The default is the value of the `TMPDIR` environment variable, or `/tmp` if that variable is not set. The option value can be given as a list of directories, to be used in round-robin fashion. Under Unix, separate directory names by colons; under Windows or NetWare, separate them by semicolons.

+     - `--unpack,-u`  
+       
+       Unpacks a packed table that was packed by `myisampack`. This option can be used to convert a compressed read-only table to modifiable form. It cannot be used with `--quick` or with `--sort-records`.

+     - `--update-state,-U`  
+       
+       Updates the internal flag that is stored in the table to indicate its state. Tables that are okay are marked as such, and tables for which an error occurs are marked as in need of repair. Using this option makes subsequent invocations of `myisamchk` with the `--check-only-changed` option more efficient for tables that are okay.

+     - `--wait,-w`  
+       
+       If a table is locked, waits until it is available. Without `--wait`, `myisamchk` waits 10 seconds for a lock and then prints an error message if no lock can be obtained.

# F.3.3  Variables for myisamchk

The following `myisamchk` variables can be set using the instructions given in Section F.2.1.2, “Setting Program Variables.”

For tables that contain `FULLTEXT` indexes, note the caution described in the introductory `myisamchk` program description.