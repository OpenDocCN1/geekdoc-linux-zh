# Running sed With External File Scripts

To run **sed** with a script, do the following:

+   1. Log in to an account that has access to the **sed** script you want to use.
+   2. Type the following to run the script on a file:

```
`sed -f script file`
```

Or, type the following to run the script on input from STDIN:

```
`process | sed -f script`
```

To run the script that you wrote in the previous section, type:

```
`sed -f ~/sedscript /mnt/cdrom/textfiles/dev_dict.txt
> /home/user/dev_dict_new.txt`
```

# Using The cut Command

To use the **cut** command, do the following:

+   1. Log in to the account you want to work with.
+   2. Determine the file or data you want to work with:

+   - If you want to work with a file, start with the following:

```
`cut`
```

+   - If you want to work with data from another program, start with this format:

```
`generate_data | cut`
```

+   3. Determine what you want to cut. For example, perhaps you want to alter a file listing in the format "ls -la" so that you get only the file’s permissions. The "ls -la" command generates output in the following format:

```
`permissions links owner group size time_last_changed name`
```

Each of these items is a numbered field, beginning with 1. So, you want to keep field 1 only.