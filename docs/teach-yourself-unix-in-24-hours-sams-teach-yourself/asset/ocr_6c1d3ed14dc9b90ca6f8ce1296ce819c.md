Before I actually add any information to this new file, I'm going to define a few
abbreviations to make life a bit easier. To do this, I type : , which, as you know,
moves the cursor to the bottom of the screen. Then I'm going to define tyu as a
simple abbreviation for the lengthy phrase Teach Yourself UNIX in a Few Minutes:

```
:abbreviate tyu Teach Yourself UNIX in a Few Minutes_
```

Pressing Return moves the cursor back to the top.

+   2. Now I'll try the abbreviation. Recall that in the .exrc, lines beginning with a
double quote are comments and are ignored when vi starts up. I press i to enter
insert mode and type " Sample .exrc file as shown in tyu. The screen
looks like this:

```
"Sample .exrc file as shown in tyu_
```

As soon as I type a space or a punctuation character, or press Return, the abbre-
tion expanded. In this case, I opt to move to the next line by pressing Return:

```
"Sample .exrc file as shown in Teach Yourself UNIX in a Few Minutes
```

+   Press Escape to leave the insert mode.
3. This feature can also be used to correct common typos you make. I know that I
have a bad habit of typing ten instead of the. Because vi is smart about abbre-
nion expansion, I can "abbreviate" the as teh and not get into trouble:

```
:ab teh the_
```

![](bbox=[0.066, 0.888, 0.133, 0.966])