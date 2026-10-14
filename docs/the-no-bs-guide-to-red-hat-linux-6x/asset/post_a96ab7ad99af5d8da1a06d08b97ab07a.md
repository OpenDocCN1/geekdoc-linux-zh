
location. Place the mouse pointer over a button on the lower toolbar, and a small pop-up help window will show what that button does.

In Figure 7-13, I've created a very basic HTML file using just ten mouse clicks. All of the HTML tags (the uppercase text enclosed in < > symbols) were entered automatically, and I had to type only the text that will appear on the Web page.

## MORE ABOUT GNOTEPAD+

Gnotepad+ is free software developed and distributed under the GNU General Public License, which means you can view the source code and contribute your own updates to the developer. The program is written and maintained by Andy Kahn, who has a Gnotepad+ Web site at http://ack.netpedia.net/gnp/.

## THE GEDIT EDITOR

The gEdit editor (see Figure 7-14) is another text editor designed for the X Windows GNOME environment. It supports user-written plug-ins, which allow gEdit to be extended to support new features while keeping the size of the core program small. It also supports multiple documents and, of course, standard text-editor functions such as search

![](img/3137cdda7122042e86dbeafe9840d4ed_210_0.png)

*Figure 7-13: Creating an HTML file with Gnotepad+*

![](img/3137cdda7122042e86dbeafe9840d4ed_211_0.png)

Figure 7-14: The gEdit editor

and replace, a toolbar, printing, cutting, copying, and pasting. If you are a programmer, you may find gEdit preferable to Gnotepad+ because of the programming plug-ins available for gEdit.
To start gEdit, enter the command

```
gedit
```

from a shell prompt, or select the GNOME Foot • Applications • gEdit menu item. You can also add a gEdit button to your GNOME taskbar by choosing Gnome Foot • Panel • Add new launcher. Specify gedit as the program name, and pick an icon you like.

## USING GEDIT

Using gEdit is not much different than using Gnotepad+ or other graphical editors. Instead of boring you with yet another "here's how to use this editor" sermon, let's focus on some of the more interesting plug-ins available for gEdit. The plug-ins menu is shown in Figure 7-15.
The Spell Check plug-in (see Figure 7-16) looks for misspelled words and displays possible alternatives. For some reason, I couldn't get the "Replace" button to replace the incorrect word in the file with the selected alternative. Your mileage may vary.

The Reverse plug-in reverses the text in the current document. The only thing good about this is that you can unreverse the text by running it again. Actually, this plug-in is meant to serve as a tutorial for people interested in writing plug-ins. You can find more about writing plug-ins at the gEdit Web site mentioned at the end of this section.

The Project Manager plug-in allows you to manage programming projects, displaying a tree of the C source-code files and the header include files used by the source file. Double-clicking on the source file or a header file will open it into gEdit.

The View in Browser plug-in renders and displays the current HTML document.

The Encryption plug-in encrypts or decrypts the current document using the ROT13 encryption algorithm, which is a simple character-substitution scheme. Don’t use this for serious encryption needs. Instead, use the PGP program discussed in Chapter 11, “Compression, Encoding, and Encryption.” Better yet, write a PGP plug-in for gEdit and share it with the world!

The Email plug-in will email the current document to any email address. A dialog box lets you fill in the From, To, and Subject lines before sending.

![](img/3137cdda7122042e86dbeafe9840d4ed_212_0.png)

Figure 7-15: The gEdit Plugins menu

![](img/3137cdda7122042e86dbeafe9840d4ed_212_1.png)

Figure 7-16: The gEdit Spell Check plug-in

The Diff and CVS Diff plug-ins are for programmers who want to compare two files using the diff command. (See Chapter 6, "Important Linux Commands," for more about the diff command.)

## MORE ABOUT GEDIT

The gEdit editor is free software developed and distributed under the GNU General Public License, which means you can view the source code and contribute your own updates to the developers. There is a gEdit Web site at http://gedit.pn.org/.
