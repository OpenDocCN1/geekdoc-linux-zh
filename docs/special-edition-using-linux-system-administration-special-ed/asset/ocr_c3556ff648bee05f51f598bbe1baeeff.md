> > **Note**
> > If you kill the children of a runaway process first, you may not succeed in terminating the runaway process. When the children are terminated, the parent may immediately spawn new children to replace the ones you killed. Sometimes, attempting to kill the children of a runaway process before killing the parent runaway process leads to rapid spawning of new children until the only way to solve the problem is to reboot the system because so many children have launched that the system becomes non-responsive.

+   - Sometimes a process will refuse to stop with the standard `kill PID` command. As outlined earlier in this chapter, this can normally be handled by using the `SIGKILL (9)` signal with the kill command, as in either of the following examples:

```
kill -9 PID
kill -KILL PID
```

PART II
CH 8