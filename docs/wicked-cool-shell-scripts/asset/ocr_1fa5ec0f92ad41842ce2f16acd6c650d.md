```
$ getbtcaddr 1Ezw0HtiXB4iFwedPr49iwyjZn2nnekhoj
Details for address 1Ezw0HtiXB4iFwedPr49iwyjZn2nnekhoj
First seen: Sun Mar 11 11:11:41 CDT 2012
Current balance: 2000000
Satoshis sent: 716369585974
Satoshis recv: 716371585974
```

*Listing 7-19. Running the getbtcaddr script*

# Hacking the Script

The numbers printed to the screen by default are pretty large and a bit difficult for most people to comprehend. The scriptbc script (Script #9 on page 34) can easily be used to report in more reasonable units, such as whole Bitcoins. Adding a scale argument to the script would be an easy way for the user to get a more readable printout.

# #62 Tracking Changes on Web Pages

Sometimes great inspiration comes from seeing an existing business and saying to yourself, "That doesn't seem too hard." The task of tracking changes on a website is a surprisingly simple way of collecting such inspirational material. The script in Listing 7-20, changetrack, automates that task. This script has one interesting nuance: when it detects changes to the site, it emails the new web page to the user, rather than just reporting the information on the command line.

# The Code

```
#!/bin/bash

# changetrack--Tracks a given URL and, if it's changed since the last visit,
# emails the new page to the specified address

sendmail=$(which sendmail)
sitearchive="/tmp/changetrack"
tmpchanges="$sitearchive/changes.$" # Temp file
fromaddr="webscraper@intuitive.com"
diperm=755 # read+write+execute for dir owner
fileperm=644 # read+write for owner, read only for others

trap "$(which rm) -f $tmpchanges" 0 1 15 # Remove temp file on exit

if [ $# -ne 2 ] ; then
 echo "Usage: $(basename $0) url email" >&2
 echo " tip: to have changes displayed on screen, use email addr '-'" >&2
 exit 1
fi

if [ ! -d $sitearchive ] ; then
 if ! mkdir $sitearchive ; then
```