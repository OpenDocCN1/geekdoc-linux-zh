
## If you have used Customize to set up font-lock colors

If you have used Customize to set up font-lock colors, it's likely that few or none of them will be the basic eight colors supported by a console, such as red, green, and yellow. There are so many more pleasing colors available in X Windows that it would be a shame to be forced to use the eight console colors in X just so font-lock would work in an Emacs console.

Looking at a Customize buffer for font-lock faces, you would think that there is no provision for two sets of colors—one for the console and one for X. Actually, there is a way to set up colors this way, but for some reason it is hidden.

To locate this setting, first bring up a Customize buffer for one of the faces. A good first one to work with is the Default face, which controls the attributes of all text not belonging to one of the font-lock faces.

Click the middle mouse button on the State drop-down menu; this is where you saved settings earlier. Farther down the menu, notice the item “Show all display specs.” Select this, and you will see a new menu called Display. Activate this menu and select “checklist.” A series of labeled check boxes appears. Select the items Type and X, and make sure that TTY remains unchecked.

Now, any changes you make to the foreground and background colors will be applied only to Emacs under X Window. Repeat this procedure for all the font-lock faces. The result will be that default color choices will be used in a console Emacs session, and the more-complex colors you have chosen will be used for Emacs under X. This procedure works identically with XEmacs.

### Customize from the minibuffer

If you know the name of a particular Customize group, variable, or face, you don't necessarily need to start up the Customize browser at all. Pressing M-x and then typing `customize-face`, `customize-group`, or `customize-variable` lets you access the particular Customize buffer you need. This is particularly useful when you know at least part of the Customize item's name (Tab completion helps here) but don't know in which group it can be found.

## Emacs and X Resource files

A couple of years ago, Custom was more limited in what it could control. Many Emacs users learned to make many of the changes just discussed in either their `~/.Xresources` or `~/.Xdefaults` file. Linux distributions use one or the other of these files to store settings for many X programs. Emacs still pays attention to these settings, but it is a good idea to phase out the use of this file for Emacs settings. It’s easier to get the Emacs behavior you want if Emacs reads all its settings from your `.emacs` file rather than trying to read from that file and the X resource file. There is less chance of conflict between the two if you comment out (with exclamation points) all Emacs settings in the X resource file and try to set up everything in Emacs using both Customize and any hand-coded Lisp you might have written.

## Limitations of Customize

As the Custom library has evolved over the past few years, more and more of the many Emacs options have been made customizable. It was a massive job, both for the core Emacs developers and the external package authors, and Emacs users are grateful. There are still some little-used options that aren’t included and a few packages (mostly small ones) that haven’t been adapted to use Customize. The great bulk of the work has been done, though, and it’s not much to ask of Emacs users that they occasionally make a manual addition to an .emacs file to enable a new package.

## Introducing Emacs Macros

A macro is simply a recorded sequence of keystrokes that can be played back at will. Whenever you find yourself repeating a procedure in Emacs, you might want to consider creating a macro.

Macros can be temporary, lasting only until you either quit Emacs or create a new macro. You can use more than one macro in a session if you give the macros names. Once you name a macro, you can save it to a file for reuse. You can even assign a keybinding to a macro so that it can be executed quickly.

This might seem a bit abstract, so before the macro techniques are introduced, a real-world example should help you see how macros can be used to save time.

## A Macro Example

Some time ago, I was writing a series of text files, each of which needed a header with the date the file was written. I didn't want to have to type the date each time; it seemed that there had to be a way to automate the process.

My first thought was to use the “insert-shell-command-output” key command. The Linux date utility returns the time and date when executed, so I tried pressing Ctrl-u M-l, typing `date`, and pressing Enter.

The output that was inserted into my buffer looked like this:

> Fri Dec 29 09:36:45 CST 2000

That wasn't quite what I was looking for; I didn't want the time inserted, and I didn't like the order of the date's units. I read the date manual page, and next I tried pressing Ctrl-u M-l, typing `date '+%A, %-d %-b %Y'`, and pressing Enter.

This time, the output was acceptable:

> Friday, 29 Dec 2000

But this command had two problems: It took longer to type the command than to type the date itself, and the cursor ended up at the beginning of the inserted date, which forced me to move the cursor to the end of the date and then press Enter for a new line.

This was a perfect situation for a macro. It was a tedious and repetitive typing task that I knew I would be doing often. I created a macro that recorded the keystrokes, including the cursor movement and newline so that after the macro executed I'd be ready to resume typing. I named the macro “mymtime” and then gave it its own keybinding, Ctrl-c m. I saved it in my ~/.emacs file so that the new command would always be available. Read on to learn how to do this.

## Recording and Playing Back Macros

The key command Ctrl-x ( starts a keyboard macro.

Everything you type, including other keyboard commands and minibuffer M-x commands, is recorded in the macro until you end it by pressing Ctrl-x ).

To execute the macro you just created, press Ctrl-x e.

Macros that are intended for temporary use in a single file can be given arguments that make the macro repeat a certain number of times. There are two ways to do this. For example, if you know that after recording a macro you will want it to repeat three times, end the macro by pressing Ctrl-u, typing `3`, and pressing Ctrl-x ).

If you want the last-recorded macro to repeat an indefinite number of times (such as throughout an entire file), press Ctrl-u, type `0`, and press Ctrl-x e.

Here is an example of that command. Imagine that you want to add three spaces of indentation to the beginning of each paragraph. First, you record a macro that would do this once (start this with point at the beginning of a paragraph):

- 1. Press Ctrl-x ( to start recording the macro.
- 2. Press the spacebar three times.
- 3. Press M-q to reformat the paragraph.
- 4. Press M-] to move forward one paragraph.
- 5. Press Ctrl-x ) to end the macro recording.

Now that the macro is recorded, make sure that point is at the beginning of the paragraph and then press Ctrl-u, type `0`, and press Ctrl-x e.

The macro will work on each paragraph in succession.

Substituting a number for the `0` in the command will execute the macro that many times rather than all the way to the end of the file.

> This macro will work in XEmacs only if adaptive-fill mode is turned off. It’s turned on by default in XEmacs, and in GNU Emacs this mode is disabled.

![](img/c8827ea52a0796def3f6891892ed9d3a_110_0.png)

## Naming and Saving Macros

Creating macros takes time. Sometimes you have to make two or three attempts before a macro does exactly what you want. Naming a macro is the first step toward saving a macro permanently, and doing this also lets you create more than one macro in a single Emacs session.

Naming a macro requires that you execute the following rather lengthy minibuffer command: Press M-x and type `name-last-kbd-macro`

> Tab completion works well with this particular command, because there don’t seem to be other Emacs commands that begin with name. Press M-x, type name, and press Tab. The remainder of the command will be completed for you. If you find yourself naming many macros, you might consider binding this command to a key.

![](img/c8827ea52a0796def3f6891892ed9d3a_110_1.png)
