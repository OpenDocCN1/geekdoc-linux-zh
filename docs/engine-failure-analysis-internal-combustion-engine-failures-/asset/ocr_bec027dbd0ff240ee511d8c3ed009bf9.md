# EXAMPLES

This Command Does the Following
history \| less Displays the current history list and pipe to less for convenient reading.
history -n Adds this session's new commands to .bash_history.

# jobs

```
jobs [ option ] [ job ID ]
```

Lists all running or suspended jobs.

# OPTIONS

Use This Option To Do This
-l List job IDs and process IDs
-n List only those jobs that have been altered since the last time this command was used
-p List process IDs only
-x command Replace the command being used with the specified command

# kill

```
kill [ option ] id
```

Terminate the process specified by id. To kill the process, you must be the owner or have superuser status (see su in Chapter 1). For a list of signals and signal IDs, see the “Signals” section in this chapter.