# What the Heck Is Script-Fu?

283

# FIGURE 21.5

The effect after having defined some fairly standard variables. With Script-Fu logo creation is almost too easy.

![](bbox=[0.233, 0.113, 0.599, 0.253])

> You might have noticed that the Script-Fu dialog boxes have no drop-down menus or preview boxes in reference to fonts (like the Text tool does). This isn't so bad, except that you might remember all the fonts installed on your system, or you might just want to browse the fonts to see what suits your fancy. Actually, this is not a problem because there are many good third-party font previewers to choose from. For example, if you're running a standard linux setup, you already have a program called xfontsel. This program is okay if you have a few fonts and are running at 1280 × 1024 resolution or above, because the font list tends to scroll way off. For the rest of us, there are two good options. If you are a KDE user, there is a program in the distribution called kfontshow, which is a very handy application. Otherwise, there's a similarly good program that completes the GNOME project called fontsel (see Figure 21.6). I like this program. You should go ahead and snag it from http://glade.pn.org/fontsel/ right away (along with the rest of the GNOME distribution, where you're at it). Another thing to keep in mind is that many scripts require some involved font information from you, such as foundry, weight, and so on. Not only is it difficult to remember which found font belongs to, but some fonts have different ideas of weight—some normal whereas others use medium, for example. This is another situation where one of these fonts utilities will come in handy. Fortunately, future versions of GIMP (what's in development right now) will include an implementation of Script-Fu with more robust Font, Pattern, and Gradient dialog boxes.

You probably observed that the application of this script involves many individual steps. As it renders the effect, you can observe each plug-in referenced from within the script doing its thing. So, the script did nothing you couldn't do by hand—it simply performed these actions for you.