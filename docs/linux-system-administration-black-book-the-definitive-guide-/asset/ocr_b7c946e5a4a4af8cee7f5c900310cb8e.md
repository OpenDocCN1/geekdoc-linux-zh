+   21. The script now has to wait for the first `passwd` prompt. Adjust the previous line to:

```
```bash
passwd $user >> passwdoutput
```
```

+   22. Adding a password by hand gives you the following output:

```
```
Changing password for user pferd
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
```
```

So, the first thing you want to watch for is perhaps just UNIX. As with other examples in this chapter, you can create an **until** loop that waits for this word to appear, by entering the following:

```
```bash
until grep -c "UNIX" passwdoutput do
done
```
```

+   23. To answer the prompt, you need to send the password and then send a carriage return. You might use

```
```bash
echo "$pass\r"
```
```

+   24. You should do something similar for the second prompt:

```
```bash
until grep -c "Retype" passwdoutput do
done
echo "$pass\r"
```
```

+   25. The rest of the items are not necessary to set up a valid user account. Each of them should be handled with **if** statements. For the full name, you might start with:

```
```bash
if [ $name !- "empty" ]
then
    usermod -c $name $user
fi
```
```

+   26. To change from the default group, use:

```
```bash
if [ $group !- "empty" ]
then
```
```