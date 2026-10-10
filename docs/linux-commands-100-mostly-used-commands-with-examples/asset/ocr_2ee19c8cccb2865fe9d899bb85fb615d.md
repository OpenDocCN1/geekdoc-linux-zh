```
```
# Print lines with more than 3 fields
awk 'NF > 3 {print}' filename
```
```

# 8. **Reading from Command Output:**

AWK can read from the output of other commands.

```
```
# List files and their sizes in the current directory
ls -l | awk '{print $9, $5}'
```
```

# 9. **Formatting Output:**

Use `printf` for better formatting.

```
```
# Print the first and second columns with specific formatting
awk '{printf "Name: %-10s Score: %d\n", $1, $2}' filename
```
```

# 10. **Multiple Commands:**