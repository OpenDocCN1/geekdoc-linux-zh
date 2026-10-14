⇒ To find out what you did on September 11, 2001, type:

```
$ touch -d "Sep 11 2001" /tmp/911 [RET]
$ touch -d "Sep 12 2001" /tmp/912 [RET]
$ find ~ -daystart -newer /tmp/911 \! -daystart -newer /tmp/912 [RET]
```

This lists all the files that were last modified on September 11, 2001. Use -anewer to list files that were last accessed that day, and -cnewer to list files that were last changed that day. Two temporary files are made with special timestamps, /tmp/911 and /tmp/912.

# 27.9 Using Other Reminder Tools

The following table lists additional tools that can be used to generate reminders, including calendars and appointment managers.

Ccal
Replacement for cal that outputs calendars in color.
DEB: ccal

Evolution
"Groupware" suite that includes calendar and address facilities.
DEB: evolution
RPM: evolution
WWW: http://ximian.com/products/evolution/

Gcal
Outputs many types of calendars, including astronomical ones.
DEB: gcal
RPM: gcal
WWW: http://www.gnu.org/software/gcal/gcal.html

KOrganizer
Appointment manager for KDE, with built-in calendar and scheduler; uses vCalendar file format.
DEB: korganizer
RPM: korganizer
WWW: http://www.kde.org/