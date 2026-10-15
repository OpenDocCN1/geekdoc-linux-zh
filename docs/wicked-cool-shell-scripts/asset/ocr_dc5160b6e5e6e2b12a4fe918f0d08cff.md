# Listing 2-18: Testing the DIR shell script to list files

This listing of the specified directory, sorted from oldest to newest, indicates file sizes (though directories always have a size of 0).

# Hacking the Script

At this point, it might be tough to find someone who remembers the MS-DOS command line, but the basic concept is powerful and worth knowing. One improvement you could make, for example, would be to have the Unix or Linux equivalent command be displayed before being executed and then, after a certain number of system invocations, have the script show the translation but not actually invoke the command. The user would be forced to learn the new commands just to accomplish anything!

# #21 Displaying Time in Different Time Zones

The most fundamental requirement for a working date command is that it displays the date and time in your time zone. But what if you have users across multiple time zones? Or, more likely, what if you have friends and colleagues in different locations, and you’re always confused about what time it is in, say, Casablanca, Vatican City, or Sydney?

It turns out that the date command on most modern Unix flavors is built atop an amazing time zone database. Usually stored in the directory /usr/share/zoneinfo, this database lists over 600 regions and details the appropriate time zone offset from UTC (Coordinated Universal Time, also often referred to as GMT, or Greenwich Mean Time) for each. The date command pays attention to the TZ time zone variable, which we can set to any region in the database, like so:

```
$ TZ="Africa/Casablanca" date
Fri Apr 7 16:31:01 WEST 2017
```

However, most system users aren’t comfortable specifying temporary environment variable settings. Using a shell script, we can create a more user-friendly frontend to the time zone database.

The bulk of the script in Listing 2-19 involves digging around in the time zone database (which is typically stored across several files in the zonedir directory) and trying to find a file that matches a specified pattern. Once it finds a matching file, the script grabs the full time zone name (as with TZ="Africa/Casablanca" in this example) and invokes date with that as a subshell environment setting. The date command checks TZ to see what time zone it’s in and has no idea if it’s a one-off or the time zone you sit in most of the time.