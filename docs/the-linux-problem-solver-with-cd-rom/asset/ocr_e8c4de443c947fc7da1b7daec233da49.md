# PROBLEM 115

Symptoms: Applications look hideous. You encounter unexpected changes in applications other than the one you’re trying to modify. X applications stop working.

Problem: You’re using * to start a line in an X resource file:

Fix: This is one of the worst things you can put in an .Xdefaults file:

```
*foreground: blue
```

Because this matches all applications’ class names [and the widget class names underneath], be ready for a lot of blue windows. Find the full name of the specific widget you want; tools like editres can help you.

# Finding Widget Class Names with editres

Figuring out a widget class name is usually the hardest part of changing that class’s setting. Manual pages usually help, but sometimes it’s just not that easy; they may talk about a name only as the last portion of a class hierarchy. When you just can’t track a name down and you’re willing to tear the entire widget tree apart, bring out the big guns in the form of a program called editres. You can also use editres to figure out undocumented settings for commercial programs.

Although it comes with most modern X distributions, editres is not well known. It’s a somewhat crusty GUI for navigating the resources in X widget trees. Start it up without any arguments. When you get the window, pull down the Commands menu and select Get Tree (see Figure 9-1). The mouse pointer then changes to a cross. Move it to a simple application that’s running on your desktop (xclock, for example), then click. The editres window responds by showing a tree of names. If the tree is too large to fit in the entire window, use the map box in the upper left corner.

Click on one of the leaf names on the right (such as "clock" for the xclock tree) to invert it, then select Show Resource Box from the Commands menu. A window pops up showing all the resource names under that leaf—but that’s not all (see Figure 9-2). Select one that looks promising (like the foreground setting in xclock.clock—let’s say you’re having trouble with xclock’s foreground color). If you want to change the resource value of the current program (and you don’t mind too much if the program crashes), type an option (such as red for xclock.clock.foreground) in the box at the bottom, to the right of Enter Resource Value. Click on Apply to see if this actually changes the program. To get rid of the Resource Box window, click the close button, conveniently labeled as the Popdown Resource Box button.