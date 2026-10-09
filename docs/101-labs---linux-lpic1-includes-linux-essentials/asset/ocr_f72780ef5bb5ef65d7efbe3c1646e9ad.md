# **Task 2:**

Now, try to predict what the output of each command will be before running it (see **Answers 1-7** below):

+   - egrep [0-3] lab53.txt
+   - egrep [e68] lab53.txt
+   - egrep "^[0-9a-zA-Z]+$" lab53.txt
+   - egrep "[0-9][A-Z][0-9]" lab53.txt
+   - egrep "[;:]" lab53.txt
+   - egrep v ".*" lab53.txt
+   - egrep "[ls] i2i" lab53.txt

`egrep` (short for `grep -E`) uses extended regex, instead of basic regex, which is the default.

# **Task 3:**

Finally, apply some of what you’ve learned about regex to these `sed` substitution commands. Again, what will the output be (see **Answers 8-10** below)?

+   - sed -E 's/[A-Z]/_/g' lab53.txt
+   - sed -E 's/^[a-z]+$/[omitted]/' lab53.txt
+   - sed -E 's/([a-z]+)/1/**g' lab53.txt

# **Answer 1:**

abc123
01234567890
A1B2C3D4E5
6F7G8H9I0J

# **Answer 2:**

456def
Hello World!
01234567890
6F7G8H9I0J
Quoth the raven: 'Nevermore.'

# **Answer 3:**

abc123
456def
password
01234567890