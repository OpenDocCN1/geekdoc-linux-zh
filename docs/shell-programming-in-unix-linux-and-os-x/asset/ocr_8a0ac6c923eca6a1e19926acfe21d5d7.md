# Exported Variables 215

![](bbox=[0.142, 0.093, 0.678, 0.447])

Figure 10.6 Subshell execution

To summarize the local and exported variables work:

+   1. Any variable that is not exported is a local variable whose existence will not be known to its subshells.

+   2. Exported variables and their values are copied into a subshell's environment, where they may be accessed and changed. However, such changes have no effect on the variables in the parent shell.

+   3. Exported variables retain this characteristic not only for directly spawned subshells, but also for subshells spawned by those subshells (and so on the down line).

+   4. A variable can be exported any time or after it is assigned a value but takes on at the moment of export; subsequent changes aren't tracked.

# export -p

If you export -p, you'll get a list of the variables and their values exported by your shell:

```
$ export -p
export LOGNAME=steve
export PATH=/usr/bin::
export TIMEOUT=600
export TZ=EST5EDT
export y=10
$
```