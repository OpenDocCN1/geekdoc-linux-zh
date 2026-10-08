```
CLEARCASE_BLD UMASK=02
_INIT_UTS_PLATFORM=SUNW,SPARCstation-10
marty$ 
```

As you can see, other environment variables in addition to PATH make working on your UNIX system easier. You may want to issue other commands related to ksh variables. Table 6-4 summarizes some ksh-related variable commands you may want to issue on your system.

![](bbox=[0.87, 0.17, 0.97, 0.25])

# Table 6-4  ksh-Related Variable Commands

| Command | Description |
| :--- | :--- |
| **env** | Lists all environment variables (exported). These variables are normally uppercase and passed to child pro- cesses. |
| **set** | Prints all local and exported set variables. |
| **set -o** | Lists all built-in variables that are set to *on* or *off*. |
| **typeset** | Displays all variables and associated attributes, func- tions, and integers. |
| **typeset +** | Displays only the names of variables. |

You may want to try all these commands on your system to see what variables have been set for you.

If you want to know the value of a specific environment variable, you could use the echo command to see its value, as shown below for the environment variable HOME:

```
marty$ echo $HOME
/home/marty
```

Similarly, to view the operating system-type on this specific computer, you could issue the following command: