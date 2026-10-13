This is a terrific example of a succinct script that is written by someone who really understands the nuances of shell scripts. The renice command lowers the priority of its own shell (recall $$ is the PID of the shell) as much as possible by setting it to +19. Every other task on the system is now more important than this shell script. The very next line does the real work by launching updatedb, which rebuilds the locate filename database.

5. One more example, a rather sophisticated use of shell scripting and file name expansion through patterns.

```
# cat tmpwatch
/usr/sbin/tmpwatch 240 /tmp
/usr/sbin/tmpwatch 720 /var/tmp
for d in /var/{cache/man,catman}/{cat?,X11R6/cat?,local/cat?}; do
  if [ -d "$d" ]; then
    /usr/sbin/tmpwatch -f 720 $d
  fi
done
```

The tmpwatch program removes files that haven't been accessed in more than a specified number of hours, and here you can see that it helps keep the uncompressed man page directories clear of old man pages (the /cat directories). Here, it's expiring files more than 720 hours (30 days) old.

You can have administrative jobs run with the cron system through a number of different ways. You can create an explicit crontab file for root, drop a new script with a time specifier in /etc/cron.d, or write a script and place it in cron.hourly, cron.daily, cron.weekly, or cron.monthly and let the cron system schedule it automatically.

For regular users, the only option available is crontab files, but as has been demonstrated, they're reasonably straightforward to create, so it's not too onerous.

# Explanation of crontab Entries Presented Earlier

Every day at 5 p.m.:
0 17 * * * top -b -n1 | head -9 | mail -s 'top status' taylor

Every day at 5 a.m.:
0 5 * * * cd /web/chatter/comics; ./build-comics-page.sh > ../index.html

At noon on the first day of each month:
0 12 1 * * /home/taylor/scripts/doitall

At midnight on the 3rd day of August each year:
0 0 3 8 * mail -s 'happy birthday Dave' taylor@intuitive.com < birthday.note