```
```bash
-bash: ./HelloWorld.sh: Permission denied
$ id Christine
uid=1001(Christine) gid=1001(Christine) groups=1001(Christine)
```
```

Christine cannot execute this file because she is not the file’s owner, nor is she in the file’s group (see Listing 22.10). The third permission set applies to her and only allows her to read the file. To let her run the file, add her to the wheel group, set her as the file’s owner, or modify the file’s world permissions.

# ## Directory Permissions

While the directory permission settings look very similar to file permissions, their effect is different. Table 22.1 shows permission effects on actions (covered in Chapter 15) associated with the entity to whom the permission applies (owner, group, or other).

**TABLE 22.1 Directory permission effects**

| Permission | Effect |
| :--------- | :---- |
| r | Allows user to display directory’s files |
| w | Allows user to create, move (rename), modify attributes, and delete files within the directory |
| x | Allows user to change their present working directory to this directory (via the cd command) as long as this permission is set in all parent directories as well |

A few examples will help you to understand these permissions. For example, the user Christine can list the /etc directory’s contents, due to the directory’s read permission for other (world), as shown snipped in Listing 22.12.

```
**Listing 22.12:** Understanding directory permission effects of the read privilege
```bash
$ whoami
Christine
$ ls -1d /etc
drwxr-xr-x. 143 root root 12288 Jan  4 09:22 /etc
$
$ ls /etc
abrt                 gshadow-             profile
adjtime              gss                  profile.d
[...]
```
```