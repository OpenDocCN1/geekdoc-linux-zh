Subprogram: name
```bash
echo "Bobby"
```

+   5. Modify the preceding exercise so that a second subprogram (with the name name2) displays the words He's my friend.
+   
+   Program:
+   ```bash
+   #!/bin/bash
+   echo "Hello"
+   name
+   name2
+   ```
+   
+   Subprogram: name
+   ```bash
+   echo "Bobby"
+   ```
+   
+   Subprogram: name2
+   ```bash
+   echo "He's my friend."
+   ```

# Chapter 15: Understanding Arguments . . . Not the Ones with Your Mother-in-Law

+   1. Write a program that accepts a person's name as an argument and then displays the name on-screen.
+   
+   Call the program:
+   ```bash
+   name Bob
+   ```
+   
+   Program: name
+   ```bash
+   #!/bin/bash
+   echo "$1"
+   ```
+   
+   2. Modify the program in the preceding exercise to accept and display the person's first and last name.
+   
+   Call the program:
+   ```bash
+   name Bob Smith
+   ```
+   
+   Program: name
+   ```bash
+   #!/bin/bash
+   echo "$1 $2"
+   ```
+   
+   3. Modify the preceding exercise to accept the first and last name as one argument.
+   
+   Call the program:
+   ```bash
+   name "Bob Smith"
+   ```