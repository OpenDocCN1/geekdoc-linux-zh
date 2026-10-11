+   5. You have three files called letter1, letter2, and letter3, which are all letters. How can you quickly determine which one is addressed to your boss?

+   a. tail letter?
+   b. nl letter?
+   c. expand letter?
+   d. head -5 letter?

Answer a is incorrect; this would display the last 10 lines of each letter. Answer b is incorrect; the nl command numbers each line. Answer c is incorrect; expand converts tabs to spaces. **Answer d is correct; this would display the first five lines of each file so that you could look for your boss’s name.**

+   6. The file containing your telephone list is approximately 2MB in size. How could you divide it into two equally sized pieces?

+   a. split -k 1 phone
+   b. pr -2 phone
+   c. od phone
+   d. split -k 2 phone

**Answer a is correct; the split command would divide the file phone into two sections of approximately 1MB each.** Answer b is incorrect; the pr command formats the file into pages. Answer c is incorrect; the od command would display the file in octal format. Answer d is incorrect; here split is directed to divide the file into 2MB pieces.

+   7. What does the paste command do by default?

+   a. Combines two or more files sequentially.
+   b. Combines two or more files side by side.
+   c. Combines two or more files by interleaving the lines.
+   d. Combines two or more files and sends them to the printer.

Answer a is incorrect; the paste command can combine files sequentially, but it requires the -d option. **Answer b is correct; the paste command combines files on a line-by-line basis with the lines being separated by a tab and displayed side-by-side.** Answer c is incorrect; paste does not mix the files. Answer d is incorrect; paste does not print the file.