# Printing Now vs. Printing Later

Most printing you do will be like this: You finish editing a document, you want to print it. If you're working inside an application program, like WordPerfect or IslandCalc or whatever, just follow the commands appropriate to that program to print your document. Give it the destination you want, and go pick up the output when it's done.

One of the problems with working in a shared printer environment is that you can't always use the printer as you might want to because it would be too disruptive to others on the system. An example of this is large print jobs that could tie the printer up for long periods. How long is a long period? This is really subjective and depends on your environment. If you share a printer with a small group of three or four other people, and you ask first, you can probably get away with a print job that takes a half hour or even an hour. But try that on a centralized printer shared by 25 or 30 users and listen to the screams. There are a couple of ways to handle this problem, depending on how your system is set up. Probably the easiest one is to simply fire off the print job on your way out the door as the last thing at night. If that's not an option, here are some ideas to keep the peace.

# PRINTING LATER

# Is there a command I can use to hold my print job for later?

Yes. Use the hold option to get your file ready for printing but not actually start it until later. If you use the hold option when printing that big job, it'll be held until you tell it to actually go to the printer. Meanwhile, however, it's been fed to the spooler and is ready and waiting. Then, when the printer will be free for an extended period, you can start it up. To print the file bigdocument to the printer netlaser but hold it until you say, try this:

```
lp -dnetlaser -H hold -m bigdocument
```