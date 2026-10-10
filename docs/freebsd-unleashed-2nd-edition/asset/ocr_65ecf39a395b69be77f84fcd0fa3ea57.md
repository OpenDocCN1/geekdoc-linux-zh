As you can see, the default behavior is to do nothing, leaving the new file in /var/tmp/temproot for you to consider after you’ve finished running. This makes mergemaster a very safe utility to run.

If you select m to merge the two files, you are dropped into the sdiff environment. This shows you the old and new versions of the changed file, line by line, allowing you to choose between the left (old) and right (new) versions of each:

```
    *** Type h at the sdiff prompt (%) to get usage help
    pccard_beep="1"                # pccard beep | pccard_beep="2"            # pccard beep
    %
```

# **TIP**

Each changed line is merged individually, so the sdiff method can become tedious if you’re using it to merge very long files with lots of scattered changes. You may be better off simply making a backup copy of the existing file, replacing it completely in mergemaster, and then merging in the changes later with a text editor and two parallel terminal windows.

Because each changed line is shown on different halves of the same screen, sometimes the two sides look the same because the only differences might be on the right half of the line. This isn’t usually a problem (the only time it tends to crop up is on version-number lines in which a modification date appears toward the end of the line). You can get around it, though, by specifying a larger screen width with the -w option to mergemaster:

```
# mergemaster -cv -w 120
```

The sdiff command options are available by typing h at the prompt. Once you’re done picking your way through the lines, you’re brought back into mergemaster, where you are given yet another chance to review (or even remerge) your changes before moving the new file into place.

Once you’re all done, mergemaster asks whether you want to delete what’s left of /var/tmp/temproot. If you’ve left unmerged files to deal with later, select “no.” You then exit from mergemaster and have the chance to go to /var/tmp/temproot to merge these remaining files by hand.

# **Troubleshooting mergemaster**

The things that can go wrong with mergemaster, fortunately, aren’t destructive to the system—especially if you have backed up your /etc directory. A few kinds of missteps are common, though, such as the following: