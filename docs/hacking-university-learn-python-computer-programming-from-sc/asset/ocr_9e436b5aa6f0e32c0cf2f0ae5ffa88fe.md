# Pwd

# Ls

Save the script. Now we have to set the permissions to allow it to be run. Use “sudo chmod 777 script.sh”, and then run the script with “./script.sh”. So long as you copied the script exactly, it will ask for your name and then show you your directory and files. Take the concept and expand it further in your own scripts. You can run commands from installed programs as well, so you can write a script that automatically joins a domain, or one that connects to the network specified. Shutting down remote computers is a great automatic task as well.

Scripts can either be run manually or set to execute at certain times. To run a certain script every time the user logs in, open the “startup applications” program from dash and create a new app with the script as the source. Now every time that user logs in the script will run automatically. This is useful for setting up certain options or starting background services without requiring the user to do it themselves.

Scheduling tasks for a certain time can be done with the Cron system daemon. It is installed be default on some systems, but if not “sudo apt-get install cron” can be used. Start the service with