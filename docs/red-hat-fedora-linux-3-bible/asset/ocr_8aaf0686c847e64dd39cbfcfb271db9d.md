as in specifying 0–3/3 in the third field to represent every third day of the month, or */5 in the first field to denote every five minutes.

Lines beginning with a `#` character in any of the *crontab-format* files are comments, which can be very helpful in explaining what task each command is designed to perform. It is also possible to specify environment variables (in Bourne shell syntax, for example, `NAME="value"`) within the *crontab* file. Any variable can be specified to fine-tune the *environment* in which the job will run, but one that may be particularly useful is `MAILTO`. The following line will send the results of the *cron* job to a user other than the one who submitted the job:

```
```
MAILTO=otheruser
```
```

If the following line appears in a *crontab* file, all output and error messages that haven’t already been redirected will be discarded:

```
```
MAILTO=
```
```

# Modifying scheduled tasks with *crontab*

The files in `/var/spool/cron` should not be edited directly. They should only be accessed via the *crontab* command. To list the current contents of your own personal *crontab* file, type the following command:

```
```
$ crontab -l
```
```

All *crontab* entries can be removed with the following command:

```
```
$ crontab -r
```
```

Even if your personal *crontab* file doesn’t exist, you can use the following command to begin editing it:

```
```
$ crontab -e
```
```

The file automatically opens in the text editor that is defined in your `EDITOR` or `VISUAL` environment variables, with vi as the default. When you’re done, simply exit the editor. Provided there are no syntax errors, your *crontab* file will be installed. For example, if your user name is `jsmith`, you have just created the file `/var/spool/cron/jsmith`. If you add a line (with a descriptive comment, of course) to remove any old core files from your source code directories, that file may look similar to this:

```
```
# Find and remove core files from /home/jsmith/src
5 1 * * 8,9,10,11,12, Wed find /home/jsmith/src -name core.[0-9]* -exec rm {} \; > /dev/null 2>1
```
```

Because core files in Fedora consist of the word *core*, followed by a dot (.) and process ID, this example will match all file beginning with *core*., followed by a number. The root user can access any user’s individual *crontab* file by using the `-u *username*` option to the *crontab* command.