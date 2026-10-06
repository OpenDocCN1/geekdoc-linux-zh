# Chapter 20 ♦ Playing Music and Video 515

Insert the music CD you want to play, and then at a shell prompt type:

```
$ cdp
```

You should see a blue screen containing the cdp display. To start the CD on a track other than 1, include the track number with the play command. Here's an example of starting a CD on track 5:

```
$ cdp play 5
```

When cdp starts, you can see all the tracks, how long each track plays, and total play time. To control the play of the CD, use the following controls (turn on Num Lock) to use these numbers from the numeric keypad:

+   9—Play
8—Pause/Resume
7—Stop
6—Next Track
5—Replay Current Track
4—Previous Track
3—Forward 15 Seconds
2—Quit (Stop Music, Edit, and Exit)
1—Back 15 Seconds
0—Exit (Continue Music and Exit)
— Help (Press the period key)

The cdp display also lets you the names of artist, CD, and each song. Because this information is saved, you can see each time you play the CD. Type these commands while the cdp display is showing to edit information about the CD currently playing:

+   a—Edit the Artist Name and press Enter.
c—Edit the CD Name and press Enter.
Enter—Edit the title of the current song and press Enter.

![](bbox=[0.136, 0.796, 0.195, 0.856])

If you try to edit a song name and cdp crashes, type eject to stop the CD from playing. Editing the song name seems to work better if you pause the song first.

The arrow keys are also pretty handy for controlling CDs in cdp. The up arrow is for pause/play, and the left arrow is to go back a track. The right arrow is to go forward a track, and the down arrow is to eject.