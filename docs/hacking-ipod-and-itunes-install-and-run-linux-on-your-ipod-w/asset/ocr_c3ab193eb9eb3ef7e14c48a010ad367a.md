+   See if you can construct a touch-tone generator with notes on your iPod. Get recordings of each of the tones a telephone can generate into iTunes. Then build a note containing numbers with links to their proper tones. For extra credit, read information from your iPod's Contacts and dial their numbers.

# ## Refferer notes

Note Reader lets you create notes that hold no content of their own, but immediately open another note they point to. You can use this kind of note as a form of indirection. To do this, create a file that has one hyperlink in it, and give the file a name that ends in .link. When you open that file, you won't see its contents—instead, the linked file will open immediately. For example, create the following file:

```
<A HREF="camera"> </a>
<TITLE>My birthday present</TITLE>
```

Save the file as a note with the name mylist.link. Because the file ends with .link, when you select in the Notes folder, it will open the link it contains, which is the note called “camera”. We've also given the note a title, “My birthday present”, so that the “.link” name won't appear in the Notes folder.

The link can be to a song or playlist, too. If you link to music, the tunes will start playing when you open the note. This feature lets you create notes that play music as soon as they're opened, without having to select links.

Another Note Reader indirection trick lets you create a file that's a list of links to other notes. If you give this file a name ending with .linx, Note Reader will display it as if it were a folder of links instead of a note of links. So, for example, create a note with the following text:

```
<a href="Something Good">start</a>
<a href="Anything Can Happen">middle</a>
<a href="Trance Atlantic Flight">end</a>
```

Save the note in a file named sample.linx. When you go to Notes, you won't be able to open sample.linx directly. Instead, it will show up in Notes with an arrow after its name, as if it were a folder. Clicking the arrow shows the links in the folder, in the order they're listed in the file. If you then pick one of the links, you'll see the note it points to.

As with .link files, you can fill your .linx notes with musical hyperlinks. When you select one of those, a song starts to play. You can even mix notes with songs in the same .linx file. Put a <TITLE> tag in the .linx folder to give it a different name when viewed in the Notes list.

# ## Taking over the notes folder

You can gain control of the Notes folder by creating a file of hyperlinks, naming it main.linx, and putting it into the main Notes folder. When you go to Notes on the iPod, it lists the links from main.linx and totally ignores anything else in the Notes