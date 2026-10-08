
# Chapter 9: Migrating from Windows Systems

# FIGURE 9-1

Import Outlook Express mail into Thunderbird

![](img/1a233c34336fbf5a85d6eb785e401709_364_0.png)

This dialog lists all Microsoft email applications that have been detected on your system. If Outlook Express is detected on your system, the Outlook Express radio button is selected by default—select the Outlook button only if you want to migrate mail from Outlook instead. (If Outlook is installed on your computer.) Click Next to proceed to a status dialog that reports the progress of importing your mail account settings, address book, and mail folders into Thunderbird. Thunderbird will start on your system, displaying a dialog like the one shown in Figure 9-2

# FIGURE 9-2

The default client dialog in Thunderbird

![](img/1a233c34336fbf5a85d6eb785e401709_364_1.png)

Although you're migrating all of your mail to Ubuntu and will hopefully never need to read mail on Windows again, you may want to click OK with the E-Mail checkbox selected. This will modify your Windows mail application settings so that Windows will start Thunderbird, rather than Outlook or Outlook Express, if you accidentally click a link that causes you to read mail on your Windows system.

# Part II: Ubuntu Desktop Users

# Note

Unless you are using IMAP, you should not read your mail on your Windows system using Outlook or Outlook Express after migrating your mail to Thunderbird. If your e-mail account is a POP account and you read mail, new mail will be downloaded to your Outlook or Outlook mail files, but will not be reflected in the Thunderbird mail files that you converted. Subsequently reading mail with Thunderbird on your Windows system is OK because your mail will be stored in the Thunderbird mail files that you're.

At this point, you should create an external backup of all the directories discussed in the section, "Backing Up Your Personal Data"

# Note

After all this about Thunderbird, you're probably wondering, "Why the heck didn't Bill include a chapter on Thunderbird in this book?" I gave that serious thought, but eventually decided that encouraging people to use the mail clients in the Evolution PIM was the right thing to do. Thunderbird is an excellent client — many of my friends us swear by Thunderbird, and I have used it on a laptop or two twice in my life. However, I think that most Ubuntu users will get much more long-term value of sticking with Evolution.

# Where Thunderbird Stores Its Mail

Thunderbird stores the mail for each user in the user's profile directory. On a Windows system, your profile directory is located in one of the following directories (depending on the version of Windows that you are using), where USERNAME is your login name on the Windows machine (sometimes concatenated with the hostname of your Windows system):

```
C:\Users\USERNAME\AppData\Roaming\Thunderbird\Profiles
```

You should be able to navigate to this folder using Windows Explorer. Thunderbird profile directories in this directory have names of the form xxxxxxxx.default, where xxxxxxxx is not an actual part of the name, but represents a unique sequence of eight characters created for the first time that you started Thunderbird. Thunderbird contains all of your account information, including a Mail subdirectory that contains all of your account information and files.

On Linux systems, mail is stored in a directory whose name has the same format, but its location depends on the version of Thunderbird that you're:

- If you have downloaded, and are using the official version of Thunderbird from the Mozilla project rather than Synaptic or the Apt-Manager, your profile directory and profile initialization file (profiles.ini) will be located in a directory called .thunderbird that is located in your home directory.
- If you have installed Thunderbird using Synaptic or the Apt Manager, your profile directory and profile initialization file (profiles.ini) will be located in a directory called .mozilla (wait, the text says) If you have installed Thunderbird using Synaptic or the Apt Manager, your profile directory and profile initialization file (profiles.ini) called .thunderbird that is located in your home directory. This was an old name for the directory that holds Thunderbird initialization files and has been preserved by the Ubuntu and Debian folks to guarantee compatibility with older Thunderbird installations.

# Chapter 9: Migrating from Windows Systems

In my opinion, it's unfortunate that Ubuntu and Debian have preserved the old name for the directory that holds Thunderbird initialization and profile information, but no one asked me.

# Tip

On Mac OS X systems, your Thunderbird profile directory is stored in one of two locations, either ~/Library/Thunderbird/Profiles or ~/Application Support/Thunderbird/Profiles. ■

# Installing or Updating Thunderbird

- If you have just installed Thunderbird for the first time, proceed to the next section ("Importing Mail into Thunderbird: New Users") for information on what files to copy from your Windows system, to put them on your Ubuntu system, and how you'll need to modify the Thunderbird profile file.
- If you've installed and used Thunderbird on your Ubuntu system before, you'll want to preserve your old Thunderbird profile, and should skip this section, "Importing Mail into Thunderbird: Existing Users."

# Importing Mail into Thunderbird: New Users

If you have never used Thunderbird on your Ubuntu system before, you can copy over the converted mail and profile initialization information from your Windows system and have Thunderbird it immediately.

To do this, create the directory ~/.thunderbird before starting Thunderbird. Next, recursively copy the xxxxxxxx.default directory from your Windows backups to the ~,thunderbird directory that you just created in your Ubuntu home directory. You can do this by copying this directory from the CD, DVD, or network location depending on the version of Thunderbird that you are using.

```
C:\Documents and Settings\USERNAME\Application Data\Thunderbird\Profiles
C:\Users\USERNAME\AppData\Roaming\Thunderbird\Profiles
```

# Tip

If you are installing Ubuntu on a new machine, you can use Samba to mount a shared Windows drive on your Ubuntu system, and copy the files over. See Chapter 25, "Connecting to Other Systems," for information on mounting shared Windows drives on your Ubuntu system. ■

# Part II: Desktop Users

You should also copy the following file from the backup of this directory from your Windows system into your ~/.thunderbird directory, depending on the version of Windows that you are using:

On Windows XP and earlier systems:

```
C:\Documents and Settings\USERNAME\Application Data\Thunderbird\profiles.ini
```

On Windows Vista and later systems:

```
C:\Users\USERNAME\AppData\Thunderbird\profiles.ini
```

When copied from a Windows system, this file will initially look something like the following:

```
[General]
StartWithLastProfile=1
[Profile0]
Name=default
IsRelative=1
Path=Profiles/hushy55.default
```

After copying it to your Ubuntu system, use a text editor to modify the version of this file that you copied from your Windows system and remove the Profiles directory from the Path variable. An updated version of this same file would look like the following:

```
[General]
StartWithLastProfile=1
[Profile0]
Name=default
IsRelative=1
Path=hushy55.default
```

When you start Thunderbird for the first time on Ubuntu, it will instantly use the Profile directory from your Windows system, and things should look exactly the same as they did there. If this is the case, congratulations! Your mail has been migrated successfully, and you can now restore your normal e-mail existence using Thunderbird as your default mail client.

# Tip

If you subsequently want to switch to using Evolution, you can easily import your Thunderbird mail into those applications as described later in the section, "Importing Thunderbird into Evolution.",

# Importing Mail into Thunderbird: Existing Users

If you've already been using Thunderbird on Ubuntu and are simply migrating old mail from a Windows system, the directory ~/.thunderbird will already exist in your home directory on your Ubuntu system. That directory will already contain a default Profile directory named something like xxxxxxxx.default and your profile initialization file, profiles.ini.
