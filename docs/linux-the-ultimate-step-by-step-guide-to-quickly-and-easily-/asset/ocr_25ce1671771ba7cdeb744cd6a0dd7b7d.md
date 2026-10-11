+   3. Deactivate nounset.

+   4. Execute `disc/var` and `ls` in an installed shell.

The reverberation command is expected to demonstrate the after effects of the `ls` command. Precluding will cause the shell to execute the first document as a command.

+   5. Add the variable `embvar` into an inserted shell and reverberation it.
+   Does the variable exist in your present shell now?

+   6. Clarify what “`set - x`” does. Can this be useful?

(Optional)

+   7. Given the accompanying screenshot, add four characters to the command so that the aggregate yield is FirstMiddleLast.
+   [paul@RHEL4b ~]$ `reverberate First; resound Middle; reverberate Last`.

+   8. Display a long listing (`ls - l`) of the passwd command utilizing the `which` command inside an installed shell.

# 15.4. Arrangement: shell insetting

+   1. Discover the rundown of shell alternatives in the man page of bash.
+   What is the distinction between situated

u and `set - o nounset`?

Check the man of bash and look for nounset - both mean the same thing.

+   2. Add nounset to your shell. Test that it demonstrates a lapse message when utilizing nonexistent variables.

```
```
set - u

Or

set - o nounset

Both lines have the same impact.
```
```

+   3. Deactivate nounset.
+   
+   ``` 
+   set +u
+   
+   Or