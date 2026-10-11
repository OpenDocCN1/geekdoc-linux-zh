```
Subprogram: name
```bash
echo " $1 "
```
```

```
Subprogram: name2
```bash
echo " $1 "
```
```

# Chapter 16: Working with Database Files

+   1. Write a program that saves the string Hello World to the file myfile.

```
```bash
#!/bin/bash
echo "Hello World" > myfile
```
```

+   2. Write a program that saves the name John Smith to the file myfile and then appends the name Mary Jones to the same file.

```
```bash
#!/bin/bash
echo "John Smith" > myfile
echo "Mary Jones" >> myfile
```
```

+   3. How do you run the program greeting so that the output of the program prints to the file myfile?

```
```bash
greeting > myfile
```
```

+   4. Repeat the preceding exercise and append the output of the program greeting to the file myfile.

```
```bash
greeting >> myfile
```
```

+   5. Write a program that saves the following information to the file mydata. Then use the gawk utility to find and display the information for Mary Jones.

Bob Smith 555-1212
Mary Jones 555-5555
Tom Adams 555-7777
John Smith 555-4444

```
```bash
#!/bin/bash
echo "Bob Smith 555-1212" >> mydata
echo "Mary Jones 555-5555" >> mydata
echo "Tom Adams 555-7777" >> mydata
echo "John Smith 555-4444" >> mydata
gawk '$2 == */jones/ {print $1, $2, $3}' mydata
```
```