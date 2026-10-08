# Chapter 9: Migrating from Windows Systems

In my opinion, it's unfortunate that Ubuntu and Debian have preserved the old name for the directory that holds Thunderbird initialization and profile information, but no one asked me.

# Tip

On Mac OS X systems, your Thunderbird profile directory is stored in one of two locations, either ~/Library/Thunderbird/Profiles or ~/Application Support/Thunderbird/Profiles. ■

# Installing or Updating Thunderbird

+   - If you have just installed Thunderbird for the first time, proceed to the next section ("Importing Mail into Thunderbird: New Users") for information on what files to copy from your Windows system, to put them on your Ubuntu system, and how you'll need to modify the Thunderbird profile file.
- If you've installed and used Thunderbird on your Ubuntu system before, you'll want to preserve your old Thunderbird profile, and should skip this section, "Importing Mail into Thunderbird: Existing Users."

# Importing Mail into Thunderbird: New Users

If you have never used Thunderbird on your Ubuntu system before, you can copy over the converted mail and profile initialization information from your Windows system and have Thunderbird it immediately.

To do this, create the directory ~/.thunderbird before starting Thunderbird. Next, recursively copy the xxxxxxxx.default directory from your Windows backups to the ~,thunderbird directory that you just created in your Ubuntu home directory. You can do this by copying this directory from the CD, DVD, or network location to you backed up the following directory depending on the version of Thunderbird that you are using.

```
C:\Documents and Settings\USERNAME\Application Data\Thunderbird\Profiles
C:\Users\USERNAME\AppData\Roaming\Thunderbird\Profiles
```

# Tip

If you are installing Ubuntu on a new machine, you can use Samba to mount a shared Windows drive on your Ubuntu system, and copy the files over the network. See Chapter 25, "Connecting to Other Systems," for information on mounting shared Windows drives on your Ubuntu system. ■