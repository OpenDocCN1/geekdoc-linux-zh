```
C. `ps -A`
D. `view`
```

Correct answer and explanation: **A**. **A** is the correct answer because the `top` program shows current system utilization and statistics for running programs.

Incorrect answers and explanations: **B**, **C**, and **D**. **B** is incorrect because `iostat` shows CPU and disk drive usage but it does not provide any information about specific programs. **C** is incorrect because `ps -A` will show all running processes but does not show how much of the system any processes is using. **D** is incorrect because `view` is used to open a file in `vi` in read-only mode.

+   5. You have a script called `my_script` you'd like to run every Sunday night at 8:30. You type in `crontab -e` to edit your crontab file. What would the correct entry in your crontab file look like?
+   	A. `8 30 * * * Sun my_script`
+   	B. `30 8 * * * Sun my_script`
+   	C. `30 20 * * 1 my_script`
+   	D. `20 30 * * * Sun my_script`

Correct answer and explanation: **C**. **C** is the correct answer because the crontab format requires the minutes be put in the first column, the hours in 24-h format in the second column, the day of the month (\`*\` for any) in the third column, and the month (again a \`*\` for any) in the fourth column. The fifth column is the day of the week. Sunday can be represented with either a \`1\`, \`7\`, or *Sun*. If the three-character abbreviation is used, case doesn't matter.

Incorrect answers and explanations: **A**, **B**, and **D**. **A** is incorrect because the hours and minutes are reversed, and the hours are not in 24-h format. **B** is incorrect because the hours are not in 24-h format. **D** is incorrect because the hours and minutes are reversed. Don't forget that on a real machine, you should include the path to your script.

+   6. You just got a new gps-based Network Time Protocol server so you no longer have to mooch off some university over the Internet. You edit the appropriate config file to add the IP address of your server. What do you need to do next?
+   	A. Nothing. The `ntp` service automatically detects the change and will start using your new time source.
+   	B. Use `chkconfig -d ntp` to turn off the service, then `chkconfig -a ntp` to turn it back on with the new settings.