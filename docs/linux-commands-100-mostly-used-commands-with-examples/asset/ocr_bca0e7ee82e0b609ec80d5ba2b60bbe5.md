# 84. tail: Display the last part of a file.

The `tail` command in Linux is a powerful utility that allows you to display the last few lines of a text file or a stream of data. It is particularly useful for monitoring log files in real-time or quickly checking the end of a large file.

# Examples:

+   1. **Display the last 10 lines of a file:**

```
tail filename
```

+   2. **Display a specific number of lines from the end of a file:**

```
tail -n 20 filename
```

This will display the last 20 lines of the file.

+   3. **Follow a file in real-time (similar to `tail -f`):**

```
tail -f filename
```