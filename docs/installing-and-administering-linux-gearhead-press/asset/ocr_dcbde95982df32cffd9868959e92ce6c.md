+   7. Find all lines in the /etc/passwd file for usernames that start with team:

```
$ grep team /etc/passwd<Enter>
```

+   8. Find all lines in the /etc/passwd file that begin with the letter t:

```
$ grep '^t' /etc/passwd<Enter>
```

+   9. Find all lines in /etc/passwd that contain a digit from 0 through 9:

```
$ grep [0-9] /etc/passwd<Enter>
```

+   10. Repeat the search in the preceding step, but this time display only the number of lines that contain the pattern:

```
$ grep -c [0-9] /etc/passwd<Enter>
```

+   11. Use the ps and grep commands to display the processes that have been initiated by users other than yourself:

```
$ ps ua | grep -v username<Enter>
```

+   12. Display the contents of the /etc/passwd file in alphabetical order:

```
$ sort /etc/passwd<Enter>
```

+   13. Display the contents of the same file but in reverse order:

```
$ sort -r /etc/passwd<Enter>
```

+   14. Display the first ten lines of /etc/passwd:

```
$ head /etc/passwd<Enter>
```