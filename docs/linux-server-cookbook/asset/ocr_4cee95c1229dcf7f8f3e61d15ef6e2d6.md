following code shows how to import the module named *math* and access a variable defined in that module.

```
```python
#!/usr/bin/python3
import math
print("PI value is:", math.pi)
```
```

To execute different system operations and to access the arguments during the script execution, there are two main modules:

+   *   **os**: This module provides functions to perform operating system tasks.
+   *   **sys**: This module provides access to some variables from the interpreter and the system.

The following code shows how to access the arguments of the application executed and how to run commands, showing the same information as the *shell script* shown before:

```
```python
#!/usr/bin/python3
import os, sys
print("The name of the script is", sys.argv[0])
print("The number of the arguments are", len(sys.argv))
print("The first argument value is", sys.argv[1])
print("The second argument value is", sys.argv[2])
print("The value for all arguments are: ", " ".join(sys.argv[1:]))
print("The current process id is", os.getpid())
rc = os.system("uptime")
print("The exit status for the command uptime was", rc)
rc = os.system("notexisting")
print("The exit status for the command notexisting was", rc)
```
```

Figure 12.10 shows the output of the command executing the previous code: