Show only Unix domain sockets.

7. **Display Summary Statistics:**

```
ss -s
```

Display summary statistics for each protocol.

8. **Display Processes Associated with Sockets:**

```
ss -p
```

Show the process information for each socket.

9. **Filter by Port:**

```
ss -t -a 'sport = :80'
```

Display only TCP sockets with a source port of 80.

10. **Display Socket Details:**