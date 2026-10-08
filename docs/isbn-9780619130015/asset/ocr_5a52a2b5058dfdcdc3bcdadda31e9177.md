**To display your system date:**

1. Type `date` in the command line, and press **Enter**.
A date like the one below appears:
`Mon Apr 20 21:30:08 EST 2000`

You may see the abbreviation EDT (eastern daylight time) instead of EST (eastern standard time), or another time zone abbreviation, such as PDT (Pacific daylight time) or CST (central standard time). Notice also that UNIX uses a 24-hour clock.

2. Type `Date` in the command line, and press **Enter**. You see the following system error message:
`bash: Date: command not found`

The system error message appears because you must enter the date command, like most UNIX commands, in lowercase letters.

The `date` command has an option, `-u`, which displays the time in Greenwich Mean Time (GMT)—GMT is also known as Universal Coordinated Time, for which the abbreviation is UTC.

**To display your system date:**

*   Type `date -u` in the command line, and press **Enter**.
A date like the one below appears:
`Mon Apr 20 23:43:148 UTC 2000`

# ### The cal Command

Use the `cal` command to show the system calendar. Your manager at Dominion, Rolf Williams, advises you that this is the command commonly used to schedule tasks and events.

**To display your system’s default calendar:**

1. Type `cal` in the command line, and press **Enter**. Without an option, the `cal` command shows a calendar of the current month. Assuming the current month is July of the year 2000, you see the default calendar shown in Figure 1-7.