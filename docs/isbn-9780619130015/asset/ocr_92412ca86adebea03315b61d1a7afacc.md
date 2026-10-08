```
Pseudocode:

While entry = minus
do
    Reposition cursor in previous field.
    Enter the data.
    Reposition cursor on field following the field that was
    just entered (re-entered data)
    Continue testing while loop.
Done
```

![](bbox=[0.25, 0.27, 0.92, 0.68])

# ### Ensuring the Correct Shell Runs the Script

Each UNIX user has the freedom and capability of choosing which shell he or she prefers. When developing a shell script, you must be responsible for ensuring that the correct shell is used to interpret your script. This is because all shells do not support the same commands and programming statements.

You can instruct the system to run a script with a specific shell. You do so in the first line of the script. The line must start with the # character, followed by the