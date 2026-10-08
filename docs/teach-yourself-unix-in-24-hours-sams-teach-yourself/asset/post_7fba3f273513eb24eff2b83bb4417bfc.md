
Use :q! (shorthand for :quit) to quit without saving the changes.

| In general, if you try to use a colon command in vi and the program complains that it might do something bad, try the command again. followed by an exclamation point. I like to think of this as saying, "Do it anyway!" |

Stay in this file for the next task you'd like, or use :q to quit.

Moving about a file using these six key commands is, on a small scale, much like the entire process of the vi editor when working with files. Stick with these simple commands you're comfortable moving around, and you will be well on the way to becoming proficient using vi.

## 11.3: Moving by Words and Pages

Earlier, in the description of the vi editor, I commented that it's always in insert mode, all commands must include the Control key. Well, it turns out that vi has its set of control-key commands, commands that require you to hold down the Control key and press another key. In this section, you learn about Ctrl-f, Ctrl-b, Ctrl-u, and Ctrl-d. These move you forward or backward a screen and up or down half a screen of text, respectively.

I toss a few more commands into the pot, too: w moves you forward by word, b moves you backward by word, and the uppercase versions of these two commands have very similar, but not identical, functions.

- 1. To see how this works, you need to create a file that is longer than the size of your screen. An easy way to do this is to save the output of a common command to a file over and over until the file is long enough. The system I has lots of users, so I needed to use the vi command just once. You might have to append the output of who to the big.output file a couple times before the file is longer than 24 lines. (You can check using we, of course.)

```
% who big.output; wc -l big.output
40
% vi big.output
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_217_0.png)

## An Introduction to the vi Editor

```
|leungtc ttyV Dec 1 18:27 (magenta)
|tuyinhwa ttyRX Dec 3 22:38 (expert)
|hollens ttyRZ Dec 3 22:14 (dov)
|brandt ttyRB Nov 28 23:03 (age)
|holmes ttyJ Dec 3 21:59 (age)
|yuxi ttyN Dec 1 14:19 (pc15)
|frodo ttyro Dec 3 22:01 (mentor)
|labeck ttyrt Dec 3 22:02 (dov)
|chenk2 ttySR Dec 3 21:53 (mentor)
|chinese ttyS Nov 28 15:11 (gold)
|cdmmert ttyS Dec 3 22:53 (excalibur)
|yuenca ttyS Dec 3 23:00 (mentor)
|janitor ttyS Dec 3 18:18 (mentor)
|mathisb ttySB Dec 3 16:17 (dov)
|janitor ttySB Dec 3 16:18 (pc15)
|cs541 ttySC Dec 2 15:16 (colaria)
|yansong ttyL Dec 1 14:44 (math)
|mpds ttyS Nov 30 19:39 (localhost)
|md ttySU Dec 2 08:45 (miller)
|tassa ttySU Dec 3 18:18 (localhost)
|eichted ttySB Dec 3 23:21 (pc1)
|sweett ttySC Dec 3 22:40 (dov)
|"big.output" 40 Lines, 1659 characters
```

Because I have only a 25-line display and the output is 40 lines (you can see that on the line at the bottom), there is more information in this file than the screen can display at once.

- 2. To see the next screen, press Ctrl-f.
I press Ctrl-f and get the following output:

```
|eichted ttySB Dec 3 23:21 (pc1)
|sweett ttySC Dec 3 22:40 (dov)
|weiman ttySD Dec 3 23:01 (dov)
|tuttleno ttySF Dec 3 23:03 (indox)
|wu ttySF Dec 3 22:10 (term01)
|daurismg ttySP Dec 3 23:10 (dov)
|cs541 ttySH Dec 3 23:12 (xds)
|cq ttySI Dec 3 23:13 (expert)
|cdmmert ttySK Dec 3 22:37 (sun22)
|jrlee ttySN Dec 3 22:53 (mac1)
|fitzggeis ttySO Dec 3 23:18 (dov)
|doerrhb ttySO Dec 3 23:20 (dov)
|cdmmert ttySQ Dec 3 23:00 (sun22)
|frazier ttySR Dec 3 23:01 (dov)
|buckeye ttySS Dec 3 23:20 (mac2)
|mtaylor ttyst Dec 3 23:22 (dov)
|look ttySU Dec 3 23:12 (age)
```

| janitor ttsw Dec 3 18:29 (age) |
| ajones ttsys Dec 3 23:23 (rass) |

Notice that the entire screen was rewritten and the familiar tilde characters have popped again to let me know I have reached the end of the file. By default, vi has a two-line overlap when you move from screen to screen. If you look carefully, you can see that both echoed show up on both screens. This doesn't mean they appear twice; rather, vi is trying to help me not lost while I wander through the file.

- 3. Now, what do you think will happen if I press Control-u?

```
| leongtc tty0 | Nov 28 15:11 (gold) |
| chinese tty2 | Dec 3 22:53 (excalibur) |
| cdemont tty5 | Dec 3 23:00 (mentor) |
| yuenca tty6 | Dec 3 23:00 (mentor) |
| janitor tty7 | Dec 3 18:18 (age) |
| mathissp tty8 | Dec 3 23:17 (dov) |
| janitor tty9 | Dec 3 16:18 (age) |
| cs541 ttyc | Dec 2 15:16 (galeria) |
| yansong ttysl | Dec 1 14:44 (math) |
| mdps tty0 | Nov 30 19:39 (localhost) |
| nd ttyu | Dec 2 06:45 (muller) |
| jac ttya | Dec 3 18:15 (localhost) |
| eichted ttyb | Dec 3 23:21 (pc1) |
| sweett ttyysc | Dec 3 22:40 (dov) |
| wetan ttysd | Dec 3 23:01 (dov) |
| tuleteno ttyse | Dec 3 23:03 (indvay) |
| wu ttyf | Dec 3 23:10 (term01) |
| daurismj tjsq | Dec 3 23:12 (dov) |
| cs541 ttyh | Dec 3 23:13 (xds) |
| cq ttyc | Dec 3 22:37 (expert) |
| cdemmont ttysk | Dec 3 22:37 (xun22) |
| jrelee ttysn | Dec 3 22:53 (mac1) |
| fitzgs ttyso | Dec 3 23:18 (dov) |
```

The command has moved up half a screen. Notice where eichted and sweett are now. Instead of the text being replaced at once, as I used Control-f, the text was scrolled a line at a time, each new line being added as the program went along. The Control-u command might work either—one line or an entire screen at a time—for you.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_219_0.png)

## An Introduction to the vi Editor

- 4. Now it's time to try moving around in this file word by word. Type w once to see what happens.

| leungtc ttys0 | Nov 28 15:11 (gold) |
| chinese ttys2 | Dec 3 22:53 (excalibur) |
| cdemmert ttys5 | Dec 3 23:00 (mentor) |

Now w six times more, noting that the cursor stops three times in the field to indicate what time the user logged into the system (15:11 in this listing). Your cursor should be sitting on the parenthesized field:

| leungtc ttys0 | Nov 28 15:11 (gold) |
| chinese ttys2 | Dec 3 22:53 (excalibur) |
| cdemmert ttys5 | Dec 3 23:00 (mentor) |

- 5. It's time to move backward. Type b a few times; your cursor moves backward to the beginning of each word.

What happens if you try to move backward and you're already on the first word, or if you try to move forward with the w command and you're already on the last word of the? Let's find out.

- 6. Using the keys you've learned, move back to the beginning of the line that starts with leungtc, Instead of typing w seven times.

## Task 11.4: Inserting Text into the File Using i, a, o, and O

Being able to move around in a file is useful. The real function of an editor, however, is to enable you to easily add and remove—in editor parlance, insert and delete—information. The vi editor has a special insert mode, which you must use in order to add the contents of the file. There are four different ways to shift into insert mode, and you learn about all of them in this unit.

The first way to switch to insert mode is to type the letter i, which, mnemonically enough, inserts text into the file. The other commands that accomplish more or less the same thing are a, to append text to the file; o, to open up a line below the current line; and O, to open a line above the current line.

- 1. For this task, you need to start with a clean file, so quit from the big.output editing session and start vi again, this time specifying a nonexistent file called buckaroo:

```
% vi buckaroo
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_221_0.png)
