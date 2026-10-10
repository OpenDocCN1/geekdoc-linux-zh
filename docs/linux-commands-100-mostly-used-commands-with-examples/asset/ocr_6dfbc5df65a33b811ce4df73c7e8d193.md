```
#!/bin/bash
`current_user=$(logname)`
`echo "The script is being run by $current_user"`
```

In a script, you can use the `logname` command to store the current user's login name in a variable for later use.

# 72. export: Set environment variables.

The `export` command in Linux is used to set an environment variable. Environment variables are dynamic values that affect the behavior of processes running on the system. These variables are accessible by any child process of the shell that sets them.

+   **Examples:**

+   **1. Setting a Simple Variable:**

```
`export MY_VARIABLE="Hello, World!"`
```

This sets the environment variable `MY_VARIABLE` with the value "Hello, World!".

+   **2. Appending to the PATH:**