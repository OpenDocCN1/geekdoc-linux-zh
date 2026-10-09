+   Let’s begin with the policy file. Tripwire’s policy file defines which files and directories tripwire should monitor for changes, and what sort of changes are significant. For some files, e.g. /bin/login, any change in file contents, modification date, or ownership is suspicious, but we’d expect them to be accessed frequently. Other files, such as log files, are expected to grow in size, but not change ownership.

The policy file that is installed with the RPM in /etc/tripwire/twpol.txt tells Tripwire to monitor many files that probably don’t exist on our system, so we’ll get lots of spurious error messages when we run an integrity check. What we really need to do is edit the policy file so that files and directories that don’t exist aren’t monitored, and conversely, if there are files and directories that do exist but are commented out in the policy file are reinstated. It would be tedious to do this by hand, so let’s use our new-found knowledge of Perl to write a script to do it for us.

+   The algorithm we need to employ is straightforward. If we find a line that looks like an instruction to Tripwire to check a file or directory (optional whitespace, string beginning with /), then we should check that the file or directory exists. If not, we should comment out the line to prevent Tripwire from generating an error.
+   
+   Similarly, if we find a line in the policy file that looks like a commented out file (optional whitespace, #, optional whitespace, string beginning with /), then we should check if the file or directory exists. If it does, then we’ll remove the comment to reinstate the file.

+   We’ll write the script as a filter, so it reads configuration lines from STDIN and writes to STDOUT. Any lines that don’t look like either of the types of line we’re interested in are passed through unmodified. It would be nice to know how much work we’ve saved ourselves by counting up the number of lines that the script modifies.
+   
+   Here’s the script (hopefully your new knowledge of Perl will give you an idea of the structure that we’ve employed, even if the details are still a bit beyond you – they’ll come with practice):

```
#! /usr/bin/perl -w

# Filter for Tripwire policy file. Looks for lines that
# start with optional whitespace and a filename, and
# comments them out if the file does not exist. Also
# looks for commented out lines containing filename and
# removes comment if they do exist.

$Additions = 0;
$Removals = 0;
```