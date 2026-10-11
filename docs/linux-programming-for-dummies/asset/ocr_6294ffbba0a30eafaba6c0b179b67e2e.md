# ## Chapter 17: Making Your Program Print Stuff Out

+   1. Send the words `Hello world` to the printer.

```
```
echo "Hello world" | lp
```
```

+   2. Print the following data to the printer:

+   * Bob Smith 555-1212
+   * Mary Jones 555-5555
+   * Tom Adams 555-7777
+   * John Smith 555-4444

```
```
echo "Bob Smith 555-1212" | lp
echo "Mary Jones 555-5555" | lp
echo "Tom Adams 555-7777" | lp
echo "John Smith 555-4444" | lp
```
```

+   3. Write the data in the preceding exercise to a file with the name `mydata` and then print the contents of the file.

```
```
echo "Bob Smith 555-1212" >> mydata
echo "Mary Jones 555-5555" >> mydata
echo "Tom Adams 555-7777" >> mydata
echo "John Smith 555-4444" >> mydata
cat mydata | lp
```
```

+   4. How can you print a formatted file (that’s to say, change its fonts)?
+   
+      Use a Linux utility such as `troff`, which enables you to specify margins, fonts, and other formats for text that you’re printing.

+   5. Modify the following program so that the data the `gawk` utility selects prints rather than appears on-screen.

```
```
#!/bin/bash
echo "Bob Smith 555-1212" >> mydata
echo "Mary Jones 555-5555" >> mydata
echo "Tom Adams 555-7777" >> mydata
echo "John Smith 555-4444" >> mydata
gawk '$2 ~ /J|S|/ {print $1, $2, $3}' mydata
```
```

**Answer:**

```
```
#!/bin/bash
echo "Bob Smith 555-1212" >> mydata
echo "Mary Jones 555-5555" >> mydata
echo "Tom Adams 555-7777" >> mydata
echo "John Smith 555-4444" >> mydata
gawk '$2 ~ /J|S|/ {print $1, $2, $3}' mydata | lp
```
```