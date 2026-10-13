should return 1 if both arguments are not supplied or if the first argument is not a directory.

If sufficient space is present, your function should return 0. This enables you to use it as follows:

```
if isSpaceAvailable /usr/local 20000 ; then
: # perform some action
fi
```

(HINT: Use the function getSpaceFree.)

4. Modify your isSpaceAvailable function to accept an optional third argument that specifies the units of the amount space to check.

The default should remain in kilobytes, but you should support m or mb indicating megabytes and g or gb indicating gigabytes. If some other units are given, assume that the user meant kilobytes.

(The following conversion factors apply to this problem: 1 megabyte equals 1024 kilobytes, and 1 gigabyte equals 1024 megabytes.)

(HINT: Use the bc command.)

5. Write a function called isUserRoot that determines whether the ID of a user is equal to 0. If no user is given, it should determine whether the ID of the current user is root. (HINT: Use getUID.)

# Terms

**Executable Code** The part of the script that consists of all the commands in the script outside of the function definitions.

**Library** A repository of functions that can be accessed by shell scripts.