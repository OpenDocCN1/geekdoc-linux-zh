![](bbox=[0.55, 0.02, 0.95, 0.38])

# Hour 15

# Running Jobs in the Future

The gist of our study together through this point in the book has been learning how to accomplish tasks, and then how to automate them with aliases and shell scripts (though the latter will be covered in greater detail later in the book). What’s been missing has been any sort of scheduler, a way whereby you can instruct the Unix system to run a specified command or set of commands in the future.

That’s what this hour focuses on, and it’s one of my favorite parts of Unix: crontab. Through the cron mechanism, as crontab is called generally, you can specify Unix commands or shell scripts to run at a specific minute, hour, day, or date. Just as importantly, you can also specify how frequently it should be run, so if you want to perpetually sidestep the problem of forgetting your anniversary by scheduling an annual e-mail greeting to your spouse, it’s a breeze with cron.