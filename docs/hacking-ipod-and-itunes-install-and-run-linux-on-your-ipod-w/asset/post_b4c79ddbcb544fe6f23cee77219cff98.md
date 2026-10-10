
You can look up information directly on the site by artist, album, or song title. Ever wonder how many songs there are with a particular word in the title, such as “old” or “myxomatosis”? Now you can find out! Here’s how:

- 1. Go to the Gracenote site at www.gracenote.com/music (Figure 6–2).
- 2. Enter the information you want to search for. You can look specifically in the artist, album, or song fields, or choose to search in all fields.
- 3. To avoid bogus results that include your search term as part of a word (for example, searching for “old” and getting results that include “hold”, “cold”, and so on), click the “Exact Phrase” box.
- 4. Choose to see 10 or 25 results at a time.
- 5. Click Search to get your first set of results.

Each item in the search results is a link to that song’s entry. You can click a song to get more information about that song.

![](img/f481d8a0ca491080698039f72bf96e1b_165_0.png)

**FIGURE 6–2: Gracenote CBDB search page.**

![](img/f481d8a0ca491080698039f72bf96e1b_166_0.png)

For more cool scripts from Apple, see *Use Apple’s iPod Scripts* in Chapter 2.

### Check or uncheck multiple tracks

The “Enable | Disable Selected Tracks” script lets you turn the checkbox on or off for all the songs you have selected. iTunes uses the checkbox as a sort of master on/off switch for playing songs. If an unchecked song is due to be played in a playlist, iTunes simply skips over it. When you set the rules for a new smart playlist, you can specify whether you want to allow unchecked songs. To use this script, select the songs whose status you want to change, then run the script. You’ll get a dialog box asking you to give thumbs up (enable) or thumbs down (disable) on the songs (Figure 6-3).

![](img/f481d8a0ca491080698039f72bf96e1b_166_1.png)

Here’s a way to enable or disable a bunch of songs en masse without a script. Command-click (Control-click on Windows) any song’s checkbox. All the songs in that playlist will have their checkboxes turned on or off.

### Export library listings

iTunes includes a built-in command (File ⇨ Export Library) for exporting your music library to an XML file. XML is a great format for exchanging data, but it’s not very easy on human eyes. To demonstrate this point, Figure 6-4 has an example of part of an exported library XML file.

If you want to produce a text file of your library that’s intended for people rather than computers, use Apple’s “Library Summary” script. This script gives you a choice of several formats for your summary. To see the available formats, click the “Set Prefs” button when you run the script. You’ll get the list shown in Figure 6-5.

After you pick a format, the script then ponders your library contents and produces a simple text file showing all your music. A companion script, “iPod Library Summary”, performs the same function for your iPod.

![](img/f481d8a0ca491080698039f72bf96e1b_166_2.png)

**FIGURE 6-3: Enable | Disable Selected Tracks script shows you this dialog box.**

```xml
Library.xml

They\288ight\286iants/Robot\280Parade/Robot\280Parade\280Demo></string>

<key>File Folder Count</key><integer>6</integer>

<key>Library Folder Count</key><integer>1</integer>

</dict>

<key>36</key>

<dict>

<key>Track ID</key><integer>36</integer>

<key>Name</key><string>Deep Blue Something - Breakfast</string>

<key>Kind</key><string>MPEG audio file</string>

<key>Size</key><integer>4114480</integer>

<key>Total Time</key><integer>257097</integer>

<key>Date Modified</key><date>2004-02-21T22:01:52Z</date>

<key>Date Added</key><date>2004-02-20T01:03:02Z</date>

<key>Bit Rate</key><integer>128</integer>

<key>Sample Rate</key><integer>44100</integer>

<key>Normalization</key><integer>3350</integer>

<key>File Type</key><integer>1347174745</integer>

<key>File Creator</key><integer>1397375309</integer>

<key>Location</key><string>file:///localhost/Users/scott/Music/
iTunes/iTunes/280Music//291Library/280Music/iTuxp/Loss/285-17-03/Unknown/280Artist/
Unknown/280Album/Deep/280Blue/280Something/28-280Breakfas</string>

<key>File Folder Count</key><integer>6</integer>

<key>Library Folder Count</key><integer>1</integer>

</dict>

<key>38</key>

<dict>

<key>Track ID</key><integer>38</integer>

<key>Name</key><string>Robot Parade (Demo)</string>

<key>Artist</key><string>They Might Be Giants</string>

<key>Album</key><string>Robot Parade</string>

<key>Kind</key><string>MPEG audio file</string>

<key>Size</key><integer>452936</integer>

<key>Total Time</key><integer>28290</integer>

<key>Track Number</key><integer>1</integer>

<key>Date Modified</key><date>2004-03-14T23:55:11Z</date>

<key>Date Added</key><date>2004-02-20T01:03:32Z</date>

<key>Bit Rate</key><integer>128</integer>

<key>Sample Rate</key><integer>44100</integer>

<key>Normalization</key><integer>2476</integer>
```

**FIGURE 6-4:** iTunes exports library files as XML.

You can use XML exporting to transfer playlists to a new computer. For details, see Move Your Playlists to Another Computer in Chapter 5.

## Miscellaneous quick tricks

A few scripts in Apple’s collection simply provide shortcuts for features you could achieve in other, less hacky but more tedious ways. These include “Open Scripts folder,” “Play Random Track”, and “Set Genre to Specific EQ”. I’ll describe each of them in this section.

![](img/f481d8a0ca491080698039f72bf96e1b_168_0.png)

**FIGURE 6-5:** Choose from various formats for your library summary.

If you want to look at the iTunes script folder, you can navigate to the Finder, find your Home directory, then drill down to the iTunes Scripts folder. But it's much quicker to use the “Open Scripts folder” AppleScript in iTunes. This script will switch to the Finder and open the folder in a new window.

You can use the “Play Random Track” script to quickly find and play any track from your library. Of course, you could achieve the same result by going to the library, closing your eyes, and double clicking somewhere in the song list, but the script is better, because when you click with your eyes closed, you might miss and accidentally launch missiles or something bad like that. Another advantage to using this script is that it doesn't take you away from your current playlist.

The “Set Genre to Specific EQ” script is handy for making sure, for example, that all your jazz tracks have a Jazz equalizer setting. To use the script, you just pick a playlist, a genre, and an equalizer setting. Here's how it works:

- 1. Choose “Set Genre to Specific EQ” from the Scripts menu.
- 2. You can decide whether to apply a specific EQ setting to all tracks of a particular genre in the entire library or only in a chosen playlist (Figure 6-6). Click the option you want.

![](img/f481d8a0ca491080698039f72bf96e1b_168_1.png)

**FIGURE 6-6:** Select whether to change EQ settings for all songs of a genre or only those in a specific playlist.

- 3. If you chose “playlist” in step 2, the script will ask you to pick the playlist you want.
- 4. Next, you’ll get a list of all possible genres. Pick the one you want to look for.
- 5. In the next step, you choose the EQ preset you want to apply.
- 6. After picking the EQ preset, the script displays a progress dialog box as it goes through your tunes and applies the setting you selected.

![](img/f481d8a0ca491080698039f72bf96e1b_169_0.png)

> You can set any bunch of tracks to the same equalizer setting with a few additional steps. Start by selecting all the tracks you want to set. Then choose File Get Info and go to the Options tab. Pick the setting you want from the Equalizer Preset pop-up, click OK, and you’re done.

## Doug's AppleScripts for iTunes

The undisputed king of iTunes scripting sites is Doug's AppleScripts for iTunes at http://www.malcolmadams.com/itunes/. This popular site's proprietor is Doug Adams, who has been writing, collecting, and publishing iTunes scripts since early 2001. The site now contains more than 260 scripts. Many of the scripts are clever and extremely useful, and a few reach the “what would I ever do without this?” level. The scripts are available for free, and if you use them and like them, you can make a donation on the site to help keep it running, a practice I highly recommend.

In this section, I’ll discuss some of the niftiest scripts available from Doug's AppleScripts. The site is very dynamic, with new scripts always arriving, so you should be sure to return often to check out the latest.

### Handle duplicate tracks

As your digital music collection grows, you’ll inevitably have to deal with the problem of duplicate tracks. Sometimes you'll forget which CDs you've ripped, or you'll move music from one disk to another, or you might even buy a track you've already ripped. You can use a set of handy scripts described in this section to help clean up duplicates.

#### Remove duplicates

This script simply looks through the selected playlist for multiple copies of the same track. If it finds any, it removes the superfluous copies from the playlist. To be considered duplicates, two (or more) playlist entries must refer to the exact same track: that is, the same file on disk. So, different tracks that have the same song name, or even tracks with the same name and artist that are on different albums (such as a “greatest hits” collection), are not considered duplicates. Remove Duplicates provides a report when it’s finished, as shown in Figure 6–7, but it doesn’t give you a chance to preapprove its work before it deletes duplicates—you just have to trust it.
