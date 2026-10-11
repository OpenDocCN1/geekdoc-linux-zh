> **Tip** Remember that you can also type `sudo -i` to enter a root shell, should you need to do several administrative commands. Then, just type `exit` to return to the regular non-admin shell.

You can also use the `-R` option to change ownership recursively. Let’s use a directory called `test_directory` as an example. Once again, it belongs to root and you want to make every file in that directory (and below) owned by natika.

```
sudo chown -R natika test_directory
```

The format for changing group ownership is just as easy. Let’s change the group ownership of `test_directory` (previously owned by root) so that it and all its files and subdirectories belong to group accounts.

```
sudo chgrp -R accounts test_directory
```

You can even combine the two formats. In the following example, the ownership of the entire `finance_data` directory changes to natika as the owner and accounts as the group. To do so, you use this form of the `chown` command:

```
sudo chown -R natika:accounts finance_data
```

> **Quick Tip** You can use the `-R` flag to **recursively change everything in a subdirectory** with `chgrp` and `chmod` as well.

Now, you are aware that files (and directories) are owned by some user and some group. This brings us to the next question.

# ## Who Can Do What?

From time to time, you need to modify file permissions. One reason has to do with security. However, the most common reason is to make a shell script file executable. This is done with the `chmod` command.