
# Keep your Linux install backed up

**Nick Peers** reveals the tools, techniques and tips you need to protect everything from personal files to your entire Linux installation.

### OUR EXPERT
- Nick Peers
- Has been an ardent backup fanatic since spending one Christmas holiday manually recovering hundreds of text files one at a time from the command line back in the late '90s.

Do you need reminding of the importance of backups? From protecting your irreplaceable data to ensuring system glitches are mere annoyances rather than catastrophes, everyone needs a good backup regimen. In this tutorial we'll explore the best tools on offer from Ubuntu and Mint to provide everything you need, and we'll cover both backup and restore scenarios, whether reverting individual files to earlier versions or undoing a recent botched update or unwanted app installation. You'll never endure the stomach-churning pain of data loss again.

### QUICK TIP
- Mint users will notice the version of Déjà Dup Backups offered in the main repositories isn't the latest – that said, there's little difference between it and the rather bloated 900MB-plus Flatpak version, which is why we recommend you install the older System Package version instead.

## Home folder

The most important part of any backup regimen is to protect your personal files, from documents to photos and videos. Unlike your OS or apps, which can be reinstalled, your personal files can't easily be recreated – if at all. Both Ubuntu and Mint ship with tools to provide the means to automatically back up these files. Mint's file backup tool is covered in the first box (opposite), but Ubuntu users are better served by their file backup tool Backups. Access it by typing `backups` into the launcher's search tool. It's actually a rebadged and integrated version of Déjà Dup Backups, and Mint users can add this via Software Manager (search for ‘deja' and choose the System Package version). After installation, you'll find it under the label Backups.

Once launched, click Create My First Backup. Your Home folder is selected by default under Folders To Back Up, while Downloads and Rubbish Bin are excluded under Folders To Ignore. Use the + buttons to add more to either list before clicking Forward.

Next, you're prompted to select a location for your backup. In addition to any locally attached storage, there are options to back up directly to Google Drive (just enter your credentials when prompted), or you can back up to any network drive (click the ? button to sync to use, such as `smb://computer-name/folder`). Once selected, click Forward again.

Next, you're given the option of encrypting your backup (which is compressed into a `tar.gz` file) using a password before being returned to the main screen. From here, click Back Up Now to take your first backup.

You'll also see a Back Up Automatically switch – you can find the same switch under Preferences > General,

![](img/5cfcf2f4448dccdd1c5c2a2851544557_55_0.png)

which is accessed via the menu button. Beneath this is an Automatic Backup Frequency option, which can be toggled between Daily and Weekly as required.

The General tab is also where you can change the destination of your backups, plus set a backup retention scheme, with backups kept for ever by default (basically until you run low on disk space), or kept for a minimum of three, six or 12 months. Finally, to change what's backed up, switch to the Folders tab.

## Restoring backups

When your backup runs, any new files are added and changed files are recorded, too. They don't overwrite the original backed-up files, which means that not only can you restore the latest version of any backed up file, but you can roll back changes on individual files, too.

Should you need to restore any files from your backup, open Backups again, but this time switch to the Restore tab and wait while your backups are scanned. Once the initial scan is complete, you'll see a Files-like view of all the folders stored in the backup.

In the bottom-right is a Date field that displays the date (and time if more than one backup exists on a specific date) of the selected backup. If you're looking to restore an earlier version of a file, use this drop-down to select the date/time of the backup you want.

Backups requires you to manually select the folders or files to restore. To restore everything, press Ctrl+A followed by Restore; otherwise browse through the folders until you find what you need. Select multiple files and folders using Ctrl-click if necessary.

You're given the option of restoring your selection to their original locations, overwriting anything that's already present, or you can opt to restore to a different folder, which creates a separate copy of your restored files in a location of your choosing. Whatever you choose, click Restore, enter the encryption password if necessary, and finally click Forward to bring them back.

## Different approach

Backups is fine for basic backup tasks, but it has two weaknesses: you can only schedule daily or weekly backups, and you can only have a single backup job. Both shortcomings can be remedied with a tool called **Back in Time**, which enables you to update backups as often as every five minutes, plus lets you set up multiple profiles, each one enabling you to back up different folders with their own schedule, settings and destination. Visit https://github.com/kit-team/backintime to install the latest version – it's relatively simple to use, as the annotation (above-right) reveals.

## System approach

System snapshots are designed to back up system files, enabling you to roll your system back to a specific point in time for whatever reason, but typically because you've run into a problem after installing a new app or update. So far the best tool for the job is **Timeshift**, which comes bundled by default in Linux Mint, and can be installed separately in Ubuntu. Although the default Ubuntu repositories include Timeshift, the version offered is frozen at the point of your Ubuntu release – in the case of Ubuntu 22.04, that's version 21.09.1. If you'd prefer to keep Timeshift up to date in Ubuntu (the current version at time of writing is 22.11.2), install it through its own repository:

```bash
$ sudo add-apt-repository -y ppa:tjaartje20080/timeshift
$ sudo apt-get update
$ sudo apt-get install timeshift
```

Timeshift can be launched through the Mint or Ubuntu launcher – indeed, you may have already set up Timeshift when you first installed Mint, as System Snapshots is offered during the initial setup process.

### Configuring Timeshift

The first time you open Timeshift you're prompted to set up your backups. Before proceeding any further, make sure you have a suitable backup drive ready – while Timeshift can store snapshots on your system...

![](img/5cfcf2f4448dccdd1c5c2a2851544557_56_0.png)

#### Navigate Back In Time

- **1. Profile**
  Back In Time splits different jobs into profiles, each with its own backup source(s), destination, schedule and other settings.
- **2. Settings**
  Click this button to set up new profiles and reconfigure existing ones – say by adding more folders or changing the backup schedule.
- **3. Timeline**
  Use the Timeline pane to view and browse snapshots by date and time. Snapshots can be renamed using the pencil icon.
- **4. Backup folder**
  All selected backup folders are listed here to aid navigation. You can also manually navigate using the Address bar above.
- **5. Browse and restore**
  Right-click a folder or file in the Files pane to restore it to its original location or make a fresh copy in a new folder.
- **6. View progress**
  In addition to this progress bar, you can monitor a backup's progress via the Back In Time menu bar icon.

> If you plan to restore an earlier version of a file, hedge your bets by copying it to a separate location for a thorough comparison.

### Mint's Built-in Backup Tool

Linux Mint ships with a file-based backup tool – **MintBackup** – that offers two separate backups in one app: Personal Data backs up the contents of your **Home** directory, while Software Selection covers the apps installed on your PC through **Software Manager**. You can include apps installed elsewhere in the list by issuing the following command in the terminal before opening Backup:

```bash
$ dpkg --get-selections > package_list.txt
```

Type `cat package_list.txt` to view the list of packages. The app is simple to use – when it comes to file backups, everything in your **Home** directory is selected for backup except for hidden files, but once you've set your backup destination (as always, this should be a separate physical drive from the one your **Home** folder currently resides on), you can exclude specific files and directories, then choose whether to include specific hidden directories or files – a good idea as many apps store configuration information in these folders. Click Apply and the backup is made.

The big weakness of MintBackup is that it can't be set to run automatically on a schedule, which is why we recommend Mint users switch to **Déjà Dup Backups**.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_56_1.png)
