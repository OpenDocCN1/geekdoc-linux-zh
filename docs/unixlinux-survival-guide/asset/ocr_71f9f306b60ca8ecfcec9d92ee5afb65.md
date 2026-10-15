# 2.2.1 Creating the Script

Step one would be to create a directory for storing and testing the scripts to be created (see Listing 2.2). Depending on your needs, creating a tree of directories for your different projects would be a good idea. Again, you don’t have to follow these examples verbatim; just create something that is usable for you and reflects your train of thought. Remember, though, a directory tree containing all the valuable work is easier to back up than countless directories scattered all over the hard disk. See Chapter 4 for scripts to automate the process.

![](bbox=[0.12, 0.36, 0.18, 0.46])

> One word of advice—use a "normal" account for development work, unless it is absolutely necessary to switch to superuser. An account with restricted rights on the system prevents possible damage to it. Some commands have destructive side effects, and it is better to get an error message than to re-install the whole system. Programs with the potential to take the computer down should be tested on a test system, which resembles the target platform as close as possible. If the test system needs to be reinstalled, it is a lesson learned; if a production server needs to be reinstalled, that’s a far more serious matter.

# LISTING 2.2 A Directory Structure for Development 1

```
erikk@unixhost:~> mkdir -p work/df_check
erikk@unixhost:~> ls -lR work
work:
total 2
drwxr-xr-x  2 erikk  staff      512 Jun 29 10:49 df_check

work/df_check:
total 0
```

The structure shown in Listing 2.2 is rather simplistic. There is a directory called work, which contains a directory named df_check. Depending on the needs, this structure could be sufficient. A more structured approach is shown in Listing 2.3.

# LISTING 2.3 Directory Structure for Development 2

```
erikk@unixhost:~> mkdir -p work/df_check/RCs work/df_check/doc
erikk@unixhost:~> touch work/df_check/ToDo.txt
erikk@unixhost:~> ls -lR work
work:
total 2
```