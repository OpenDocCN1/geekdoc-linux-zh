you'd like to be notified by pager whenever one of the filesystems has reached capacity. You are instructing **swatch** to look for the expression “authentication failure,” and you are specifying an e-mail message that indicates what action to take. The e-mail message will have the subject “Auth Failure Report.” The **echo** directive instructs **swatch** to include the offending message in the e-mail. The **throttle** directive ensures that you are only alerted once every 30 minutes, regardless of the frequency of the message within the 30-minute period.

```
watchfor /authentication failure/
echo
bell
throttle 00:30
mail=sysadmin@example.com,subject=Auth Failure Report
```

If it’s after hours, the following configuration file entry indicates that the staff should also be paged. This example looks for occurrences of the string “filesystem full” and sends two separate e-mail messages, one to **sysadmin@example.com**, and another to **sysadmin-pager@example.com**, but only during the hours of 5 P.M. to 9 A.M.

```
watchfor /filesystem full/
echo
mail=sysadmin@example.com,subject=FileSystem Full
mail=sysadmin-pager@example.com,when=1-7:17-9
```

Finally, consider the following example of a **swatch** configuration file that triggers corrective action at the same time that the administration staff is informed of the condition. This example is similar to the previous two, except that it invokes the execution of a script (**cleanup_old_files**) whenever the string “filesystem full” is encountered.

```
watchfor /filesystem full/
echo
mail=sysadmin@example.com,subject=Cleaning Files
exec 'cleanup_old_files'
```

# Running swatch

The **swatch** script accepts several command-line options. Table 3.1 describes the ones that you need to be most interested in.