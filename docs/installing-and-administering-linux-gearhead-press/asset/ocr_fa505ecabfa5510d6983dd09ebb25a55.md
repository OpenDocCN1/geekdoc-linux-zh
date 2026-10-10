# Shell Commands, Continued

| COMMAND | DESCRIPTION |
|---|---|
| test | Used for conditional test; has two formats: |
| | 1. $ if test expression |
| | Example: |
| | $ if test $ - -eq2 |
| | 2. $ if [expression] |
| | Example: |
| | $ if [ #-eq 2 ] |
| | Please Note: Spaces are required |
| | Operators: |
| | -eq = |
| | -lt < |
| | -le =< |
| | -ne <> |
| | -gt > |
| | -ge => |
| | String operators: |
| | = Equal |
| | != Not equal |
| | -z Zero length |
| | File status (for example, -opt file 1) |
| | -f Ordinary file |
| | -r Readable by this process |
| | -w Writable by this process |
| | -x Executable by this process |
| | -s Nonzero length |