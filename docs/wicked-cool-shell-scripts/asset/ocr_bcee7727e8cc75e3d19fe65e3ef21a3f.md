Also worthy of note is the simple solution to processing comma- and dash-separated lists of values. The punctuation is simply replaced with spaces, and each value is tested as if it were a stand-alone numeric value. That's what the ${ } sequence does in the for loops at ②, ⑥, ④, ⑤, and ⑥:

```
$(echo "$dow" | sed 's/[,\-]/ /g')
```

This makes it simple to step through all numeric values, ensuring that each and every value is valid and within the range for that specific crontab field parameter.

# Running the Script

This script is easy to run; just specify the name of a crontab file as its only argument. To work with an existing crontab file, see Listing 6-9.

```
$ crontab -l > my.crontab
$ verifycron my.crontab
$ m my.crontab
```

Listing 6-9: Running the verifycron script after exporting the current cron file

# The Results

Using a sample crontab file that has two errors and lots of comments, the script produces the results shown in Listing 6-10.

```
$ verifycron sample.crontab
Line 10: Invalid day of week value "Mou"
>>>> 10: 06 22 * * Mou /home/ACEsystem/bin/del_old_ACinventories.pl

Line 12: Invalid minute value "99"
>>>> 12: 99 22 * 1-3,6 /home/ACEsystem/bin/dump_cust_part_no.pl

Done. Found 2 errors in 13 crontab entries.
```

Listing 6-10: Running the verifycron script on a cron file with invalid entries

The sample crontab file with the two errors, along with all the shell scripts explored in this book, are available at http://www.nostarch.com/wcss2/.

# Hacking the Script

A few enhancements would potentially be worth adding to this script. Validating the compatibility of month and day combinations would ensure that users don't schedule a cron job to run on, for example, 31 February. It could also be useful to check whether the command being invoked can actually be found, but that would entail parsing and processing a PATH variable (that is, a list of directories within which to look for commands