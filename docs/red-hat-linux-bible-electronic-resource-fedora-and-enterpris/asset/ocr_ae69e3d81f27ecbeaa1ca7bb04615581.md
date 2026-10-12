If information about the CD doesn't appear, you can add Artist and Title information about the CD yourself. Then you can select each track to type in the track name. To add the name of the artist and the disc title, click in the appropriate box and type in that information. Figure 8-2 shows the CD Player and the CDDB Track Editor.

![](bbox=[0.127, 0.172, 0.616, 0.48])

**Figure 8-2:** Play CDs and store artist, title, and track information with gnome-cd.

# Playing CDs with cd\_p

If you are working from a dumb terminal or just don’t have your X desktop running, you can run the cd\_p utility (which comes with Red Hat Linux) to play CDs. I don’t suggest running this from a Terminal window; it doesn’t display properly. First, insert the music CD you want to play. Then, to start cd\_p, at a shell prompt type:

```
$ cd\_p
```

You should see a blue screen containing the cd\_p display. If instead of starting on the first track you want to start on another track (for example, track 5), type:

```
$ cd\_p play 5
```

When cd\_p starts, you can see all the tracks, how long each track plays, and total play time. To control the play of the CD, use the following controls (turn on Num Lock to use these numbers from the numeric keypad):

+   • 9 — Play
+   • 8 — Pause/Resume
+   • 7 — Stop
+   • 6 — Next Track