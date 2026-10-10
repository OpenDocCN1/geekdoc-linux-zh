olders until you find what you need. Select multiple
files and folders using Ctrl-click if necessary.

You're given the option of restoring your selection to
their original locations, overwriting anything that's
already present, or you can opt to restore to a different
folder, which creates a separate copy of your restored
files in a location of your choosing. Whatever you
choose, click Restore, enter the encryption password if
necessary, and finally click Forward to bring them back.

# Different approach

Backups is fine for basic backup tasks, but it has two
weaknesses: you can only schedule daily or weekly
backups, and you can only have a single backup job.
Both shortcomings can be remedied with a tool called
**Back in Time**, which enables you to update backups
as often as every five minutes, plus lets you set up
multiple profiles, each one enabling you to back up
different folders with their own schedule, settings
and destination. Visit https://github.com/kit-team/
backintime to install the latest version – it's relatively
simple to use, as the annotation (above-right) reveals.

# System approach

System snapshots are designed to back up system
files, enabling you to roll your system back to a specific
point in time for whatever reason, but typically
because you've run into a problem after installing a
new app or update. So far the best tool for the job is
**Timeshift**, which comes bundled by default in Linux
Mint, and can be installed separately in Ubuntu.
Although the default Ubuntu repositories include
Timeshift, the version offered is frozen at the point of
your Ubuntu release – in the case of Ubuntu 22.04,

# NAVIGATE BACK IN TIME

![](bbox=[0.44, 0.12, 0.99, 0.345])

+   1.  **Profile**
+       Back In Time splits different jobs into profiles, each with its own backup source(s), destination, schedule and other settings.
+   2.  **Settings**
+       Click this button to set up new profiles and reconfigure existing ones – say by adding more folders or changing the backup schedule.
+   3.  **Timeline**
+       Use the Timeline pane to view and browse snapshots by date and time. Snapshots can be renamed using the pencil icon.
+   4.  **Backup folder**
+       All selected backup folders are listed here to aid navigation. You can also manually navigate using the Address bar above.
+   5.  **Browse and restore**
+       Right-click a folder or file in the Files pane to restore it to its original location or make a fresh copy in a new folder.
+   6.  **View progress**
+       In addition to this progress bar, you can monitor a backup's progress via the Back In Time menu bar icon.

that's version 21.09.1. If you'd prefer to keep Timeshift
up to date in Ubuntu (the current version at time of
writing is 22.11.2), install it through its own repository:

`$ sudo add-apt-repository -y ppa:tjaartje20080/timeshift`

`$ sudo apt-get update`

`$ sudo apt-get install timeshift`

Timeshift can be launched through the Mint or
Ubuntu launcher – indeed, you may have already set
up Timeshift when you first installed Mint, as System
Snapshots is offered during the initial setup process.

# Configuring Timeshift

The first time you open Timeshift you're prompted to
set up your backups. Before proceeding any further,
make sure you have a suitable backup drive ready –
while Timeshift can store snapshots on your system

![](bbox=[0.06, 0.54, 0.41, 0.73])

> If you plan to restore an earlier version of a file, hedge your bets by
> copying it to a separate location for a thorough comparison.

# » MINT'S BUILT-IN BACKUP TOOL

Linux Mint ships with a
file-based backup tool –
**MintBackup** – that offers two
separate backups in one app:
Personal Data backs up the
contents of your **Home**
directory, while Software
Selection covers the apps
installed on your PC through
**Software Manager**. You can
include apps installed

elsewhere in the list by
issuing the following
command in the terminal
before opening Backup:
`$ dpkg --get-selections > package_list.txt`
Type **cat package_list.txt**
to view the list of packages.
The app is simple to use –
when it comes to file
backups, everything in your

**Home** directory is selected
for backup except for hidden
files, but once you've set your
backup destination (as
always, this should be a
separate physical drive from
the one your **Home** folder
currently resides on), you can
exclude specific files and
directories, then choose
whether to include specific

hidden directories or files – a
good idea as many apps store
configuration information in
these folders. Click Apply and
the backup is made.

The big weakness of
MintBackup is that it can't be
set to run automatically on a
schedule, which is why we
recommend Mint users
switch to **Déjà Dup Backups**.