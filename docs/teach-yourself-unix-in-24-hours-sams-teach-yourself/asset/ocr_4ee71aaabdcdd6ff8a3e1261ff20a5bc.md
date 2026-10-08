92 Hour 5

execute permission only. This means that users can run the application, but they can't
examine it to see how it works or copy it. (Copying requires the ability to read the file.)

![](bbox=[0.171, 0.188, 0.266, 0.263])

# JUST A Minute

Though actual programs with execute-only permission work fine, a special
class of programs called shell scripts fail. Shell scripts act like a UNIX
command-line macro facility, which enables you to save easily a series of
commands in a file and then run them as a single program. To work,\however, the shell must be able to read the file and execute it, too, so
shell scripts always require both read and execute permissions.

There are clearly a few permutations on the different permissions: read, write and
execute. In practice, a few occur most commonly, as listed in Table 5.2.

# Table 5.2. The most common file permissions.

| Permission | Meaning |
|---|---|
| --- | No access is allowed |
| r-- | Read-only access |
| r-x | Read and execute access, for programs and shell scripts |
| rw- | Read and write access, for files |
| rwx | All access allowed, for programs |

These permissions have different meanings when applied to directories, but --- always
indicates that no one can access the file in question.

Interpretation of the following examples should help:

```
---r-- 1 taylor 3843 Oct 10 16:22 iecc.list
---rw-- 1 taylor 280233 Oct 10 16:22 mailing.lists
---rw-- 1 taylor 1031 Oct 7 15:44 newlists
---rwx-x-- 1 taylor 64 Oct 9 09:31 the.script
```

The first file, iecc.list, has read and write permission for the file owner (taylor) and is off-limits
to all other users. The file mailing.lists offers similar access to the file owner (taylor) andnto the group but offers read-only access to everyone else on the system. The third file,
newlists, provides read and write access to both the file owner and group, but no access to
anyone not in the group.

5