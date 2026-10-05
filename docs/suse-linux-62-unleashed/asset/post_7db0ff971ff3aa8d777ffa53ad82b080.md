
# SuSE System Administration
PART III

## LISTING 22.3 retrieve_one—Automating FTP Retrieval

```
# Usage "retrieve_one HOST:FILE" uses anonymous FTP to connect
# to HOST and retrieve FILE into the local directory.
```

```bash
MY_ACCOUNT=myaccount@myhost.com
HOST=`echo $1 | sed -e "s/::.*//"`
FILE=`echo $1 | sed -e "s/::.*//"`

LOCAL_FILE=$(basename $FILE)`
```

```bash
# -v report all statistics.
# -n: connect without interactive user authentication.
ftp -v $HOST << SCRIPT
  user anonymous $MY_ACCOUNT
  get FILE $LOCAL_FILE
  quit
SCRIPT
```

retrieve_one is useful for purposes such as ordering a current copy of a FAQ into your local directory; start experimenting with it by making a request with the following:

```bash
# retrieve_one rtf.mit.edu:/pub/userset-by-hierarchy
-->/comp/linux/answers/linux/info-sheet
```

SuSE comes with other utilities you can use for FTP retrieval. See Chapter 10, “FTP,” for information about the ncftp and gftp commands.

## HTTP Retrieval

For an HTTP interaction, let the Lynx browser do the bulk of the work. The Lynx browser that accompanies the SuSE distribution is adequate for all but the most specialized purposes. You can obtain the latest version at http://lynx.browser.org. Although most Lynx think of HTTP as an interactive browser, it's also handy for dropping a copy of the latest headlines, with live links, in a friend's mailbox with this:

```bash
# lynx -dump http://www.cnn.com mail someone@somewhere.com
```

To create a primitive news update service, script the following and launch it in the background (using the ampersand, &):

```bash
NEW=/tmp/news.new
OLD=/tmp/news.old
URL=http://www.cnn.com
while true
  do
```

# Automating Tasks
CHAPTER 22

```bash
mv $NEW SOLD
lynx -dump -nolist $URL >$NEW
diff $NEW SOLD
# Wait ten minutes before starting the next comparison.
sleep 60
```

Any changes in the appearance of CNN's home page will appear onscreen session every 10 minutes. This simple approach is less practical than you might first expect because CNN periodically shuffles the content without changing the information. It's an instructive example, however, and a starting point from which you can elaborate your own scripts.

## Conclusions on Shell Programming

Shells are glue; there's a way to get an application to perform an action from the command line, there's almost certainly a way to wrap it in a shell script that gives you power over argument validation, iteration, and input/output redirection. These are powerful techniques and well worth the few minutes of study and practice it takes to begin learning them.

Even small attentions pays off. My personal rule of thumb is to write tiny, disposable, one-line shell scripts when I expect to use a sequence twice during a session. For example, although I have a sophisticated set of reporting commands for analyzing Web logs, I also find myself going to the trouble of editing a disposable script such as /tmp/ for quick, ad hoc queries.

```bash
ls -t /var/log/* | grep -v "old" | wc -l
```

This particular example reports on the number of requests for pages that include the string and exclude the most recent log. As you become proficient with shell constructs, it will become easy for you to write one-line shell scripts.

## Scheduling Tasks with cron and Jobs

SuSE Linux comes with several utilities that manage job scheduling. cron (or crontab)—has a couple of interfaces, and different engineers use both launches a process at a certain time of day, day of week, or even day of the month. Each user can have his own crontab, and output from the executed cron job is sent as an email to the user's mailbox (img/cbac72550c7126a22162e94d91a0c360_676_0.png).

The daemon is started by the cron script under the /etc/init.d directory when you boot SuSE Linux. This daemon checks your system's /etc/crontab file as well every minute, looking for any tasks scheduled to run. As a system administrator, you can schedule system tasks in /etc/crontab or in root's own crontab. It's important to note that these are two distinct files. initially contains several entries:

```bash
SHELL=/bin/sh
PATH=/usr/bin:/sbin:/bin:/usr/lib/sbin
MAILTO=root
* * * * root -x /usr/sbin/atrun && /usr/sbin/atrun
0 21 * * * root -x /usr/sbin/faxclean && /usr/sbin/faxclean
5 22 * * * root -x /usr/sbin/texpire && /usr/sbin/texpire
25 23 * * * root -x /usr/sbin/facron && /usr/sbin/facron | mail Master
```

```bash
# check scripts in cron.hourly, cron.daily, cron.weekly and cron.monthly
*/15 * * * root -x /usr/lib/cron/cron-runs && /usr/lib/cron-runs
0 0 * * root rm -f /var/cron/lastrun/cron.daily
0 0 * * 6 root -f /var/cron/lastrun/cron.weekly
0 0 1 * root rm -f /var/cron/lastrun/cron.monthly
```

Before looking at the individual entries, it's important to understand the significance of the first five columns on a crontab line. For the first five columns, * is a placeholder that means "any" or "all". The first column specifies the minute a particular cron job runs, and will be a number between 0 and 59, inclusive. Please note that for the first five columns, it is possible to specify ranges by typing, example, 3-10, which would cause a cron job to run from 3 minutes to 10. There are other shortcuts to specifying cron entries; type man 5 crontab for more details.

The next four lines specify the hour (0-23), the day of the month (0-31), and day of week (0-7). Cron will logically "and" these conditions to determine when to run a particular script. The only exception is if a day of month and day of week are specified, it will "or" these two fields. In all other cases, replacing * with a numeric value limits the times that a particular command will execute.

Scripts set to run on an hourly, daily, weekly, monthly basis will be found under the /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly directories. The fifth entry in the preceding listing beginning with */15 runs a script responsible for executing the files in these four directories. This particular cron job runs every 15 minutes (the initial hyphen on this line is a special extension that tells cron not to write a message to the system log every time this job executes). Personal tasks, created by the crontab command, are saved under the /var/cron directory. Personal at jobs are saved under the /var/spool/atjobs directory and will have group and file ownership of the creator, like this:

```
-rwx ------ 1 ball ball 1093 Apr 19 17:47 a00020020eb209c
```

The difference between crontab and at is that crontab should be used to schedule and run periodic, repetitive tasks on a regular basis, whereas at jobs are usually meant to run once at a future time.

(img/cbac72550c7126a22162e94d91a0c360_678_0.png)
