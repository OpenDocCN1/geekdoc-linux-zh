# EXPLANATION

+   1. The $fh variable is assigned to the db filehandle and opened for reading.
+   2. Each line of the file is assigned, in turn, to the scalar $line while looping through the file.
+   3. If the scalar $line contains the regular expression Lori, the if block is entered.
+   4. The tell function is called and returns the current byte position (starting at byte 0) in the file. This represents the position of the first character in the line that was just read in after the line containing Lori was processed.
+   5. The value in bytes is stored in $currentpos. It is printed. Byte position 40 represents the position where Sir Lancelot starts the line.