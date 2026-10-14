14. Create the icon as described earlier in the section, “The Icon Element.” Your icon for running the zile command in /home/dsl/.desktop/zile.lnk looks like this:

```
table Icon
Type: Program
Caption: Zile
Command: aterm -e /opt/bin/zile
Icon: /home/dsl/.xtdesktop/program.png
X: 420
Y: 384
end
```

# NOTE

I am using one of the generic icons available in DSL. Other generic icons are binary.png, gear.png, and shellscript.png. You can change the icon later by right-clicking the displayed icon. See Chapter 4 for details.

15. Create a file list for your new application. This prunes out directories and allows you to add the menu and icon. Create the file list for the entire Zile application by typing the following

```
# cd /
# find opt/zile -not -type d > /tmp/zile.list
```

16. Add link, menu, and icon lines to this file list using a text editor:

```
# beaver /tmp/zile.list
```

Here is what the zile.lst file looked like before adding your DSL-specific files:

```
opt/zile/bin/zile
opt/zile/share/zile/dotzile.sample
opt/zile/share/zile/TUTORIAL
opt/zile/share/zile/HELP
opt/zile/share/zile/FAQ
opt/zile/share/zile/AUTODOC
opt/zile/share/man1/zile.1
opt/zile/share/info/zile.info
```