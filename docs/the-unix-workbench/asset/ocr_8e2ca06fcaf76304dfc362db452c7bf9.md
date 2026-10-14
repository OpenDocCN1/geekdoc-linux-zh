you want to do more complex tasks with cron it’s better for cron to execute a bash script that you’ve written in advance. That way you can just specify bash /path/to/script.sh in the last column of the table.

Using stars in all columns is the simplest line of a cron table, so let’s look at some examples of more complex table entries:

```
# m h dom mon dow   command
00 * * * * bash /path/to/script.sh    # Runs every hour at the start of the hour
00 12 * * * bash /path/to/script.sh    # Runs every day at noon
* 12 * * * bash /path/to/script.sh    # Runs every minute between 12pm and 12:59pm
00 00 05 * * bash /path/to/script.sh    # Runs the 5th day of every month at midnight
00 00 * 07 * bash /path/to/script.sh    # Runs every day in the month of July at midnight
00 00 * * 2 bash /path/to/script.sh    # Runs every Tuesday at midnight
```

Besides numbers and the star there are a few other characters that you can use in cron table columns including a hyphen (-) for specifying ranges and a comma (,) for specifying lists of items. For example 00-29 in the Minutes column would specify the first thirty minutes of an hour, while 1,5 in the Day of Week column would specify Monday and Friday.

Let’s take a look at another example of a cron table that uses hyphens and ranges so you can get a sense of how each character works.