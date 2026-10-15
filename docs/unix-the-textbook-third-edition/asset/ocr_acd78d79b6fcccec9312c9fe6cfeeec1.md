```
#include "unistd.h"
#include "stdlib.h"
```

You start by moving to the first character of the first line. Next, in Command mode, you execute the following commands:

```
qa
^
i#include "<Esc>
$
a"<Esc>
j
q
```

These commands do the following:

+   1. Start recording a macro in register a.
+   2. Move to the beginning of the line.
+   3. Insert the string #include " at the beginning of the line.
+   4. Move to the end of the line.
+   5. Append the double quotation mark (") character to the end of the line.
+   6. Go to the next line.
+   7. Stop recording the macro.

Now that you have done the work once, you can repeat the change by typing the command "@a" three times.

The "@a" command can be preceded by a count, which will cause the macro to be executed that number of times. In this case you would type: "3@a".

# EXERCISE 3.3

How would you open a unique history window for the / and ? commands?

# EXERCISE 3.4

Where does the cursor have to be positioned in the buffer if you want to execute a modified version of the substitute command :s/everyone/computer scientists/ correctly?