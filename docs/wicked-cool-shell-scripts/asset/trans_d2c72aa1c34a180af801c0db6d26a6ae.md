

```
if [ $? -ne 0 ]; then
echo "$(basename $0): Failed trying to mkdir $gsync" >&2
exit 1
fi
fi

for name # Loop over the arguments passed to the script.
do
echo "Copying file $name to your Google Drive"
cp -a "$name" "$gdrive/gsync/"
done

exit 0
```

Listing 13-8: The syncgdrive script

## How It Works

Like Script #89 on page 300, this script checks whether the particular cloud service daemon is running before copying a file or files into the Google Drive folder. This is accomplished in the block of code at 1.

To write really clean code, we should probably check the return code from the open call, but we’ll leave that as an exercise for the reader, okay? 😊

After this, the script ensures the existence of a subdirectory on Google Drive called gsync, creating it if needed, and simply copies the designated file or files into it using the handy -a option to cp to ensure that the creation and modification times are retained.

## Running the Script

Simply specify one or more files that you’d like to have synced up with your Google Drive account, and the script will do all the behind-the-scenes work to ensure that happens.

## The Results

This is cool, actually. Specify a file you want copied to Google Drive, as Listing 13-9 shows.

```
$ syncgdrive sample.crontab
Starting up Google Drive daemon...
Copying file sample.crontab to your Google Drive
$ syncgdrive "~/Documents/what-to-expect-op-ed.doc"
Copying file /Users/taylor/Documents/what-to-expect-op-ed.doc to your Google Drive
```

Listing 13-9: Starting Google Drive and syncing files with the syncgdrive script

Notice that the first time it runs, it has to launch the Google Drive daemon, too. After you wait a few seconds for the files to be copied to the cloud storage system, they show up in the web interface to Google Drive, as shown in Figure 13-1.

![](img/4ffb1cc24a1b24b49254839643abedb2_340_0.png)

Figure 13-1: Sample.crontab and an office document synced with Google Drive automatically show up online.

## Hacking the Script

There’s a bit of false advertising here: when you specify a file to sync, the script doesn’t keep it in sync with future file changes; it just copies the file once and is done. A really interesting hack would be to create a more powerful version of this script in which you specify files you want to keep backed up and it checks them on a regular basis, copying any that are new up to the gsync directory.

## #93 The Computer Says . . .

OS X includes a sophisticated voice synthesis system that can tell you what’s going on with your system. Often it’s located in the Accessibility options, but you can do a lot with a computer that can, for example, speak error messages or read files out loud.

It turns out that all of this power—and a bunch of fun voices—is also accessible from the command line in OS X, through a built-in utility called say. You can test it out with this command:

```
$ say "You never knew I could talk to you, did you?"
```

We knew you’d think it was fun!

There’s a lot you can do with the built-in program, but this is also a perfect opportunity to write a wrapper script that makes it easier to ascertain what voices are installed and get a demo of each one. The script in Listing 15-10 doesn’t replace the say command; it just makes the command easier to work with (a common theme throughout this book).

## The Code

```
#!/bin/bash
# sayit--Uses the "say" command to read whatever's specified (OS X only)

dosay="$(which say) --quality=127"
format="$(which fmt) -w 70"

voice=""          # Default system voice
rate=""           # Default to the standard speaking rate

demovoices()
{
  # Offer up a sample of each available voice.
  voicelist=$(say -v \? | grep "en_" | cut -c1-12 \
    | sed 's/\/_/;s/_/ /g')

  if [ "$1" = "list" ] ; then
    echo "Available voices: $(echo $voicelist | sed 's/ /, /g')" \
      | $format
    echo "HANDY TIP: use \"$(basename $0) demo\" to hear all the voices"
    exit 0
  fi

  for name in $voicelist ; do
    myname=$(echo $name | sed 's/_/ /')
    echo "Voice: $myname"
    $dosay -v "$myname" "Hello! I'm $myname. This is what I sound like."
  done

  exit 0
}

usage()
{
  echo "Usage: sayit [-v voice] [-r rate] [-f file] phrase"
  echo "  or: sayit demo"
  exit 0
}

while getopts "df:r:v:" opt; do
  case $opt in
    d ) demovoices list  ;;
    f ) input="$OPTARG"  ;;
```

