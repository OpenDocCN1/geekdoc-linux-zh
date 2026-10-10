# EXAMPLES

```
```
shell1> flock /tmp -c cat
shell2> flock -w .007 /tmp -c echo; /bin/echo $? Set exclusive lock to directory /tmp and the second command will fail.
shell1> flock -s /tmp -c cat
shell2> flock -s -w .007 /tmp -c echo; /bin/echo $? Set shared lock to directory /tmp and the second command will not fail. Notice that attempting to get exclusive lock with second command would fail.
shell> flock -x local-lock-file echo 'a b c' 
Grab the exclusive lock 'local-lock-file' before running echo with 'a b c'.

(
    flock -n 9 || exit 1  # ... commands executed under lock ... ) 9>/var/lock/mylockfile
The form is convenient inside shell scripts. The mode used to open the file doesn't matter to flock; using > or >> allows the lockfile to be created if it does not already exist, however, write permission is required. Using < requires that the file already exists but only read permission is required.
[ "${FLOCKER" } != "${0}" ] &&& exec env FLOCKER="${0}" flock -en "${0}" "${0}" "${@}" || : 
This is useful boilerplate code for shell scripts. Put it at the top of the shell script you want to lock and it'll automatically lock itself on the first run. If the env var $FLOCKER is not set to the shell script that is being run, then execute flock and grab an exclusive non-blocking lock (using the script itself as the lock file) before re- executing itself with the right arguments. It also sets the FLOCKER env var to the right value so it doesn't run again.
```
```