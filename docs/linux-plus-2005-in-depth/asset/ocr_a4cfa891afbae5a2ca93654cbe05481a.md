Although the vi editor is the most common text editor used on Linux and UNIX systems, other text editors that are easier to use exist.

The mcedit editor (Midnight Commander Editor) is an easy-to-use text editor that contains support for regular expressions and the ability to use the mouse for highlighting text. To edit the project4 file using the mcedit editor, simply type mcedit project4 at a command prompt and the following is displayed on the terminal screen:

```
project4	[--···] 0 L: 140 1/18 0 1/583b
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache Lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
```

1Help 2Save 3Mark 4Replac 5Copy 6Move 7Search 8Delete 9Pulldn 10Quit

Note that you can access much of the functionality of mcedit by using the function keys on the keyboard as described at the bottom of the screen (F1 = Help, F2 = Save, and so on).

Although mcedit is a simple and straightforward text editor to use, it lacks the functionality seen in the vi editor. An alternative to the vi editor that offers an equal set of functionality is the GNU Emacs (Editor MACros) editor. To open the project4 file in the Emacs editor, simply type emacs project4 and the following is displayed on the terminal screen:

```
File Edit Options Buffers Tools Help
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.
```