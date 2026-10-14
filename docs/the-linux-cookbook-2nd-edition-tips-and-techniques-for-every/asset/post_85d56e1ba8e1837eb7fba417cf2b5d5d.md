
## Jpilot

Keeps names and addresses on a Palm desktop, and includes date book, address book, to-do list, and a facility for making memorandums; extensive plug-ins have been developed for it.
DEB: jpilot
RPM: jpilot
WWW: http://jpilot.org/

## Our CLOCK

Analog clock for X that inverses its colors when you have new mail waiting; has built-in appointment facility.
DEB: rxvt
RPM: rxvt
WWW: http://sourceforge.net/projects/rxvt/

## Plan

Graphical schedule planner.
DEB: plan
RPM: plan
WWW: http://me.in-berlin.de/~bitrot/plan.html

## QuickList

Keep track of any sort of thing you can put in a list.
DEB: quicklist
RPM: quicklist
WWW: http://tinyurl.com/2a9d5

## Remind

Reminder service with WWW facilities.
DEB: remind

## Wmdate

Prints calendar in the “docking bar” of window managers, such as Window Maker.
DEB: wmdate
RPM: wmdate

## Xwrits

Reminds you to take a break from typing.
DEB: xwrits

## Xcal

The original graphical calendar for X. Has programmable alarms and an appointment and memo facility.
DEB: xcal

## 28. Scheduling

Sometimes it is useful to specify a command or set of commands so that they run not immediately, but at some other time. This chapter describes techniques for handling this sort of function, as well as techniques for monitoring commands that are currently running.

### 28.1 Running a Command on a Delay

The sleep tool does nothing but wait (or "sleep") for the number of seconds specified as an argument. This is useful for ringing the system bell, playing a sound file, or running some other command at your terminal after a short delay.

To do this, give the number of seconds to "sleep" as an argument to sleep, followed by a semicolon character (;)¹ and the commands to run. This runs the given commands only after sleep waits for the given number of seconds.

Since the shell where you type this command will be unusable until the commands you give are executed (or until you interrupt the whole thing), type this command in an xterm or virtual console window (see Recipe 2.3 [Using Consoles and Terminals], page 32) other than the one you are working in.

Here are two ways to use this.
- To ring the bell in five seconds, type:
  $ sleep 5; echo -e '\a' RET
- To announce the time in 30 seconds, type:
  $ sleep 30; saytime RET

You can also give the time in minutes, hours, or days. To do this, follow the argument with a unit, as listed in the following table.

| s | Seconds |
| m | Minutes |
| h | Hours |
| d | Days |

To announce the time in exactly five minutes, type:
$ sleep 5m; saytime & RET

### 28.2 Running a Command on a Timer

Use at to run commands on a timer. It takes as an argument the exact time you want to run a command, and then it reads commands from the standard input, starting from the "at" prompt and ending when you type CTRL-D on a line by itself. It schedules a job for the commands you give, and it runs them at the specified time (see Recipe 3.3 [Managing Jobs], page 70). The commands are executed by /bin/sh, the default shell; as a reminder, at warns you about this fact when you specify the commands.

To mail yourself a reminder at five minutes after 5 p.m. today, type:

```
$ at 17:05 RET
warning: commands will be executed using /bin/sh
at> mail chuck -s "IT'S TIME TO GO!" < /dev/null RET
at> CTRL-D <EOT>
job 5 at 2003-08-09 17:05
$
```

In this example, the username is chuck and the job number scheduled by at is 5.

The at tool understands many time formats, from the month, day, and year to the hour and minute (optionally given in military time, or followed by "AM" or "PM"), and the special words "midnight," "noon," and "teatime" (the last of which translates to 4 p.m.). You can use the suffixes "today" or "tomorrow," and you can use a "+" after a time followed by a number of minutes, hours, days, or weeks—for example, "8pm + 2 days" means to run two days from 8 p.m. tonight. So to run a command at a week from midnight, use "midnight + 1 week."

To schedule ~/bin/clean and ~/bin/tidy to run at 9 p.m. tomorrow, type:

```
$ at 9pm tomorrow RET
warning: commands will be executed using /bin/sh
at> ~/bin/clean RET
at> ~/bin/tidy RET
at> CTRL-D <EOT>
job 6 at 2003-08-09 17:10
$
```
