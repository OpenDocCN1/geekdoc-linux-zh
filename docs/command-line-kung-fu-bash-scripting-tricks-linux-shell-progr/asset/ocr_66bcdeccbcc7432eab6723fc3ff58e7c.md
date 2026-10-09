# SHELL SCRIPTING

# Use a for Loop at the Command Line

```
$ for VAR in LIST
do
# use $VAR
done
```

When you need to perform the same action for a list of items, you can use a for loop right from your shell.

```
$ for USER in bob jill fred
do
sudo passwd -l $USER
logger -t naughty-user $USER
done

Locking password for user bob.
passwd: Success
Locking password for user jill.
passwd: Success
```