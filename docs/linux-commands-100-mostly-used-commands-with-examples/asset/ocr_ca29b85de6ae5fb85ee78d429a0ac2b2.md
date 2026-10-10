```
chown -R newowner:newgroup mydirectory
```

This command recursively changes the ownership of all files and subdirectories within `mydirectory` to the user `newowner` and the group `newgroup`.

3. **Verbose Output:**

```
chown -c newowner:newgroup myfile.txt
```

This command provides a verbose output, indicating the changes made to the ownership of `myfile.txt`.

4. **Changing Ownership Based on Current Owner:**

```
chown --from=currentowner:currentgroup newowner:newgroup myfile.txt
```

This command changes the ownership of `myfile.txt` from the current owner `currentowner` and group `currentgroup` to the new owner `newowner` and group `newgroup`.

14. **ps:** Display information about running processes.