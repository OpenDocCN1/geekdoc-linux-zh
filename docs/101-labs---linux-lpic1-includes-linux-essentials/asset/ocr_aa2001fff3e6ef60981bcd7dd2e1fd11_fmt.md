
- `touch bar`
- `ls -l bar`
- `umask $0`

The `bar` file should have no permissions set— you’ve masked them all out with `umask`.

# Task 6:

Finally, clean up with `sudo rm foo bar`

# Notes:

The first octal bit of `chmod` deals with `setuid` and `setgid` (and the sticky bit, on directories). When set, these bits will run an executable file as the user/group owner, rather than the user running the executable. This opens up security risks, particularly when a program is owned by `root`. For this reason, most systems will ignore the `setuid`/`setgid` bits when set on shell scripts.
