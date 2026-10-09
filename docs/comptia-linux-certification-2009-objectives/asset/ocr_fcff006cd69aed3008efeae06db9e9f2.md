# **Symptom**

# **Cause And Solution**

| Symptom | Cause And Solution |
| :--- | :--- |
| The user is unable to log in. | **Cause:** The settings in the user account or the group account could be wrong. **Solution:** Check the user or group account settings, including the permission to log in to the system, the shell, and the path of the home directory. |
| The user is unable to access files and directories. | **Cause:** The required permission is not granted to the user. **Solution:** Check the user or group quota and the privileges granted to the user. |
| The user is unable to execute basic commands or applications. | **Cause:** The environmental variable is not properly set. **Solution:** Check the environmental variables and the library files of the application. |
| The scheduled jobs are not executed. | **Cause:** The `crond` daemon has not started or stopped due to the invalid configuration. **Solution:** Check whether the `crond` daemon is running. Otherwise, check whether the configuration set in the crontab file is correct. |
| The user is unable to switch between the runlevels. | **Cause:** The `PATH` variable is not set properly or permission is not granted to the user to switch between runlevels. **Solution:** Check whether the user is granted the necessary privileges required to change the runlevel or if the path of the `sbin` directory is set in the `PATH` variable. |

# Core System Variables

Core system variables affect the behavior of applications and commands. Some of the system variables and their functions are given in the following table.

| Use This Variable | If You Need To Specify |
| :--- | :--- |
| `HOSTNAME=Hostname` | The hostname of the system. |
| `SHELL=Shell path` | The shell path for the system. |
| `MAIL=Mail path` | The path where mail will be stored. |
| `HOME=Home directory` | The home directory of the user. |
| `PATH=User path` | The path in which the user needs to operate. |
| `HISTSIZE=Number` | The number of entries to be stored in the history. |
| `USER=User name` | The name of the user. |