This sequence first synchronizes the file system buffers and then clears the page cache, dentries, and inodes.

# 3. **With Options**:

```
sync -f -d -v
```

+   - `-f` : Force the sync operation even if file systems are clean.
+   - `-d` : Enable disk write caching.
+   - `-v` : Verbose mode.

# 4. **Sync before Shutdown**:

```
sync && shutdown -h now
```

This command syncs the file system and then initiates a system shutdown.

# 5. **Viewing Sync Progress**:

```
watch -n 1 sync
```

This updates the sync status every second.