
Party at Jack's
Fri Lunch with Kim and Jo, 12:30
Mon Book manuscript due

The `calendar` tool reportedly first appeared in Version 7 of AT&T UNIX, and was rewritten early on for the BSD family of Unix. While the BSD derivative is available for Debian as part of the `bsdmntutils` package, this tool isn't yet standard on all Linux distributions.

The following are recipes for writing your calendar files, including other calendar files in your own calendar file, and for automating the delivery of your reminders.

> NOTE: Emacs has its own equivalent to this tool, which it calls the "Diary." See Info file `emacs-e20.info`, node `Diary` for more information on this feature.

- 28.4.1 Making an Appointment File
- Making an input calendar files.
- 28.4.2 Including Holidays in Your Reminders
- Including other calendars in yours.
- 28.4.3 Automatic Appointment Delivery
- Automating the delivery of your appointments.

## 28.4.1 Making an Appointment File

To begin using `calendar`, you need to make a "calendar file" where you can enter your appointments. It's just a plain text file, and can be called either `calendar` or `.calendar`; the latter makes it a "hidden" file, as described in Listing Hidden Files.

Write each appointment or calendar entry on a line by itself; blank lines in the file are ignored. The format of a calendar entry is as follows:

```
[date] [tab or spaces] [text of reminder itself]
```

Just about every common date style is recognized. For example, the following are all valid dates for the fourth of July:

```
7/4
July 4
4 July
Jul. 4
Jul 4
```

Entries aren't constrained to a single day, either; you can have entries for a day of the week or for a certain month--- `Mon` or `Monday` for every Monday; `Jun` or `June` for the first day of every June. You can use an asterisk as a wildcard: `*/13` reminds you of something on the thirteenth of every month. When the date is omitted on a line, the date of the preceding appointment is assumed.

For example, suppose you have a file called `calendar` in your home directory that looks like this:

```
6/16    Finish draft of book
        Party at Jack's
6/20    Gallery reading
Fri     Lunch with Kim and Jo, 12:30
Mon     Book manuscript due
```

If the current date is 16 June, a Friday, and you run `calendar` in your home directory, you'll get the same output as in the example in the previous section, Managing Appointments.

> *NOTE:* In the example above, the entry for the party doesn't have a date on it—it used the date of the preceding entry, `6/16`.

## 28.4.2 Including Holidays in Your Reminders

The `calendar` package comes with a collection of prepared calendar files for many kinds of holidays and other occasions, which you can reference in your own calendar file to include their entries in your own reminders.

The prepared files are stored in `/usr/share/calendar`. The following table gives the name of each calendar file and describes its contents.

| CALENDAR FILE | DESCRIPTION |
|---|---|
| calendar.birthday | Births and deaths of famous people. |
| calendar.christian | Christian holidays. |
| calendar.computer | Significant dates in the history of computing. |
| calendar.history | Dates of U.S. historical events. |
| calendar.holiday | Standard and obscure holidays. |
| calendar.judaic | Jewish holidays. |
| calendar.music | Dates related to music, mostly 1960s rock and roll. |
| calendar.usholiday | U.S. holidays. |
| calendar.hindu | Hindu holidays. |

To have `calendar` output dates from one of these files along with your usual appointments, put the following in your calendar file, where *file* is the name of the particular calendar file you want to include:

```
#include <file>
```

For example, to output both US holidays and famous births and deaths when you run calendar, put these lines somewhere in your calendar file:

```
#include <calendar.usholiday>
#include <calendar.birthday>
```

NOTE: You can, of course, share your own calendar files with other users; this is useful for making special calendars for a group or organization. If the calendar file is in the current directory or `/usr/share/calendar`, you can just give the file name; otherwise, give its full path name in the include statement.

## 28.4.3 Automatic Appointment Delivery

You can automate your appointment service so that your appointments and reminders are delivered each time you log in or start a new shell, or you can have the day's reminders emailed to you each morning.

Add calendar to your `.bashrc` file to output the day's appointments and reminders every time you log in or start a new shell (see section Customizing Future Shells).

If you keep your calendar file in a directory other than your home directory, make sure that calendar (the tool) is called from that directory. For example, if your calendar file is in your `~/doc/etc` directory, you'd put the following line in your `.bashrc` file:

```
cd ~/doc/etc; calendar; cd
```

To have the system send you the day's appointments in email, use crontab to schedule a daily cron job process which runs calendar and, if there is any output, mails it to you with mail.
