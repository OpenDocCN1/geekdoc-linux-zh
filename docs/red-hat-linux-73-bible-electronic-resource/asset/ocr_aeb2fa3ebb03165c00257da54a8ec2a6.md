+   * The `strippostcc` parameter can be used to cause To, Cc, and Bcc lines to be removed from locally posted articles. The default is to not strip them out (false), as indicated by the following line:

```
strippostcc:         false
```

# Posting exponential backoff parameters

A set of backoff parameters is used to control high-volume news posters. This feature works by indexing news clients by either user name or IP number. After the number of posts from the user or IP number reaches the limit set for the time period you set, posting backoff occurs, which is when your server sleeps for a period of time before posting anything. In this way, posts get through at an increasingly slower rate.

The backoff feature is off by default. To turn it on, you need to set the backoffauth parameter to true. The time between postings is used to determine the sleep time. By default, no location is defined for storing backoff information. A common place to put the database of backoff information is in /var/lib/news/backoff (set by backoffdb parameter).

The backoffk parameter lets you set how sleep time is multiplied. If it were set to 3, the sleep time will triple the sleep time for each subsequent post. The backoffpostfast can be used to increase the backoff sleep time when posts from the same identity arrive in less than the backoff time. The backoffpostslow parameter, by default, allows up to 86,400 postings from the same identity (because it is set to 1). Divide 86,400 by the value of backoffpostslow to allow fewer posts per day.

The number of postings that are allowed before the backoff feature kicks in is set to 10,000 by the backofftrigger parameter. The following lines are examples of the default settings for the set of backoff commands.

```
backoffauth:         false
backoffdb:           
backoffk:            1
backoffpostfast:     0
backoffpostslow:     1
backofftrigger:      10000
```

# Monitoring parameters

The innwatch program can be set up to log INN server activities. The doinnwatch parameter indicates whether or not to have the innwatch program started from the /etc/rc.news script (which starts automatically when the innd script starts the INN server at boot time). The logging service is off (false) by default.

Other monitoring-related parameters set thresholds for a variety of INN server attributes that the monitoring service looks out for. These include watching for free space running out in the