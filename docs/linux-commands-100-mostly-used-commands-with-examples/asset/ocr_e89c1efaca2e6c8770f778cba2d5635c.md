This command finds directories in the specified path.

# 5. Search for Files Modified in the Last N Days:

```
find /path/to/search -mtime -7
```

This command finds files modified within the last 7 days.

# 6. Search for Files Larger Than a Specific Size:

```
find /path/to/search -size +1M
```

This command finds files larger than 1 megabyte.

# 7. Execute Command on Found Files:

```
find /path/to/search -name "*.log" -exec rm {} \;
```

This command finds all files with a ".log" extension and removes them using the `rm` command.

# 8. Combine Multiple Criteria with Logical Operators:

```
find /path/to/search -name "*.txt" -o -name "*.md"
```