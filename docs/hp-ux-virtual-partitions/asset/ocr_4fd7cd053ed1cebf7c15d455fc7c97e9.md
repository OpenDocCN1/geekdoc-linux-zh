altPath    Modify the Alternate Boot Path
Parameter – Alternate Boot Path in decimal

conpath    Modify the Console Path
Parameter – Console Path in decimal

isauto1    List contents of the autoexecute file

display    Display the Primary Boot, Alternate Boot, and Console Paths

readnm     Display the contents of one word of NVM in
hexadecimal
Parameter – NVM address in decimal or standard
hexadecimal notation

readss     Display the contents of one word of Stable Storage in
hexadecimal
Parameter – Stable Storage address in decimal or
standard hexadecimal notation

# DIAGNOSTICS

isl displays diagnostic information through error messages written on the console and display codes on the LED display.

For the display codes, CEQX are informative only. CYKX and CY2X indicate errors, some of which are fatal and cause the system to halt. Other errors merely cause isl to display a message.

Non-fatal errors during an autoboot sequence cause the autoboot sequence to be aborted and isl to prompt for input. After non-fatal errors during an interactive isl session, isl merely prompts for input.

Fatal errors cause the system to halt. The problem must be corrected and the system RESET to recover.

+   - CE00    isl is executing.
+   - CE01    isl is autobooting from the autoexecute file.
+   - CE02    Cannot find an autoexecute file, autoboot aborted.
+   - CE03    No console found, isl can only autoboot.
+   - CE05    Directory of utilities is too big, isl reads only 2K bytes.
+   - CE06    autoexecute file is inconsistent, autoboot aborted.
+   - CE07    Utility file header inconsistent: COW values invalid.
+   - CE08    autoexecute file input string exceeds 2048 characters, autoboot aborted.
+   - CE09    isl command or utility name exceeds 10 characters.
+   - CE10    isl has transferred control to the utility.
+   - CE11    Internal inconsistency: Volume label - FATAL.
+   - CE12    Internal inconsistency: Directory - FATAL.
+   - CE13    Error reading autoexecute file
+   - CE14    Error reading from console - FATAL.
+   - CE15    Error writing to console - FATAL.
+   - CE16    Not an isl command or utility.
+   - CE17    Utility file header inconsistent: Invalid System ID.
+   - CE18    Utility file header inconsistent: Bad magic number.
+   - CE19    Utility would overwlay isl in memory.
+   - CE1A    Utility requires more memory than is configured.
+   - CE1B    Error reading utility into memory.
+   - CE1C    Error reading utility into memory.
+   - CE1D    Incorrect checksum: Reading utility into memory.
+   - CE1E    Console needed - FATAL.
+   - CE1F    Internal inconsistency: Boot device class - FATAL.
+   - CE21    Destination memory address of utility is invalid.