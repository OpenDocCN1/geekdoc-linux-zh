+   **Listing 24–A**
+   Summary of the mywc.
+   script.

```
NAME
mywc-labeled word count
SYNOPSIS
mywc filename
DESCRIPTION
This is the outline for mywc:
Select sh
Run wc on $1 and capture output with set
Print the filename ($4)
Print the number of lines ($1)
Print the number of words ($2)
Print the number of characters ($3)
```

The shell script that implements the outline is shown in Listing 24–2B.

+   **Listing 24–B**
+   The mywc.
+   script.

```
#!/bin/sh
# Label the output from wc
set `wc $1`
echo "File: $4"
echo "Lines: $1"
echo "Words: $2"
echo "Characters: $3"
```

+   1 Use the text editor to create the script file. Open a file named mywc and enter the script shown in Listing 24-2B. Write and quit the file when finished.
+   2 Make the script executable. Use chex for this:
+   $ chex mywc <Return>
+   mywc is now executable:
+   -rwxr-xr-x 1 yourlogin 59 Date time mywc
+   3 Test the new script. You might run mywc on the file chex:
+   $ mywc chex <Return>
+   File: chex
+   Lines: 5
+   Words: 17
+   Characters: 84