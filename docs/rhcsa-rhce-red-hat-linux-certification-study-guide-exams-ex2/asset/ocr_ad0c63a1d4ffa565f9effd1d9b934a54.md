Before you proceed, make sure the group ID assigned to group tg1 (in this case, 99999) is not already in use. Make sure to add the following line to /etc/shadow. A group password is not required:

tg1:::

3. Create a directory intended for use by the tg1 group:

```
# mkdir /home/testshared
```

4. Change the user and group ownership of the shared directory:

```
# chown nobody.tg1 /home/testshared
```

5. Log in as user test1. Make sure the login navigates to the /home/test1 directory. Run the umask command to confirm that files created from this account will have appropriate permissions. (The output of the umask command for regular users such as test1 should be 0002.) If there's a problem with the home directory or the umask output, you may have made an error earlier in this chapter with user settings. If so, repeat Steps 1–5 on a different VM.

6. Run the cd /home/testshared command. Now try to create a file with the following commands. What happens?

```
$ date >\test.txt
$ touch abcd
```

7. Now as the root user, set group write permissions on the testshared directory.

```
# chmod 770 /home/testshared
```

8. Log in again as user test1, navigate back to the /home/testshared directory, and then try to create a file in the new directory. So far, so good.

```
$ cd /home/testshared
$ date >\ test.txt
$ ls -l test.txt
```

9. Remove all permissions for other users on new files in the /home/testshared directory:

```
# chmod o-rwx /home/testshared/*
```