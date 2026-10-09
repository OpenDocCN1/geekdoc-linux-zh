**Task 2:**
Now, try to predict what the output of each command will be before running it (see **Answers 1-7** below):

+   - grep [0-3] lab52.txt
+   - grep [e68] lab52.txt
+   - grep "^[0-9a-zA-Z]\+$" lab52.txt
+   - grep "[^0-9][A-Z]([0-9]" lab52.txt
+   - grep "<\\.>" lab52.txt
+   - grep -v "." lab52.txt
+   - fgrep -v "." lab52.txt

That last command is a bit of a curveball. `fgrep` (short for `grep -F`) treats an expression as a literal string and does not use regex matching. So it is excluding all matches containing a literal `.`—which, of course, is none of them.

**Answer 1:**
```
abc123
01234567890
A1B2C3D4E5
6F7G8H9I0J
```

**Answer 2:**
```
456def
Hello World!
01234567890
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

**Answer 3:**
```
abc123
456def
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
```

**Answer 4:**
```
abc123
456def
1234567890
```