Save the script. Now we have to set the permissions to allow it to be run. Use “sudo chmod 777 script.sh”, and then run the script with “./script.sh”. So long as you copied the script exactly, it will ask for your name and then show you your directory and files. Take the concept and expand it further in your own scripts. You can run commands from installed programs as well, so you can write a script that automatically joins a domain, or one that connects to the network specified. Shutting down remote computers is a great automatic task as well.

Scripts can either be run manually or set to execute at certain times. To run a certain script every time the user logs in, open the “startup applications” program from dash and create a new app with the script as the source. Now every time that user logs in the script will run automatically. This is useful for setting up certain options or starting background services without requiring the user to do it themselves.

Scheduling tasks for a certain time can be done with the Cron system daemon. It is installed as default on some systems, but if not “sudo apt-get install cron” can be used. Start the service with “service cron start” and create a new crontab file with “crontab -e”. Select nano as your text editor. At the bottom of the created file, add a new line with our scheduled task. The format goes as follows:

minute, hour, day, month, weekday, command

And we format it with these options to specify when to run the command. Time numbers start with 0, so the hours range from 0 to 23 and minutes are from 0 to 59. Replace any option with an asterick to specify that it will run on any value. Pay attention to these examples:

```
0 12 * * * ~/script.sh
```

This will run the script.sh found in the Home directory every day at noon.