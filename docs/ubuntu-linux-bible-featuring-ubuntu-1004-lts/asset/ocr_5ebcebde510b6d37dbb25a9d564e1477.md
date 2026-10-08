# Note

You can download this script and others in this book from my web site at www.vonhagen.org/scripts. The name of this script is import_thunderbird_mail.sh. ■

You can find out the name of the Thunderbird profile directory by listing the directory ~/.thunderbird:

```
$ ls ~/.mozilla_thunderbird
hf8dwpmj.default profiles.ini
```

In this case, your Profile directory is the directory h8dwpmj.default. In this case, the command to run this script and its output from execution be the following:

```
$ import_thunderbird_mail.sh -t h8dwpmj.default
Copying /Personal Folders.sbd/Writing to Writing-imported
Copying /Personal Folders.sbd/Inbox to Inbox-imported
Copying /Personal Folders.sbd/Personal to Personal-imported
```

The next time you start Thunderbird on Ubuntu, you should see the imported mailboxes, as shown in Figure 9-3.

# FIGURE 9-3

Existing and imported mailboxes in Thunderbird

![](bbox=[0.056, 0.523, 0.661, 0.856])