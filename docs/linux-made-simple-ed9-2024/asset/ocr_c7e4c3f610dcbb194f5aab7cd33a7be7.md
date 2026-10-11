![](bbox=[0.06, 0.09, 0.44, 0.28])

![](bbox=[0.46, 0.09, 0.78, 0.28])

> › Vim can be tricky to get to grips with, but it does at least include detailed help on board.

> › Gedit’s syntax highlighting supports a comprehensive list of programming languages and document types.

to do things like saving. And what’s the code to save? It’s `.iw`. Which makes a lot more sense if you think in slightly different terminology: that’s ‘w’ for ‘write’.

nano Definitely a great choice both for beginners and those who don’t want too much fuss. nano – and the non-GNU package it cloned, called pico – is a straightforward console text editor that retains the simplicity of most GUI editors. Don’t be fooled into thinking there isn’t complexity in there, because there’s plenty, but much of it is hidden under the surface. We’ll look at nano in more detail later on.

ged It’s console-based. It works on plain text. But as long as your console supports mouse input (and even if it doesn’t) ged is about as close as you could get to a GUI text editor, with proper menus and everything.

# On the desktop

As you might expect, there’s a little more deviation from the pure text-editor form on the desktop, but we’ll look at some of the prime candidates and define Windows Wordpad as our upper limit: feature rich, but still primarily about the words.

gedit This is the text editor that comes with most Gnome desktops, and probably our favourite. It expands on the basic text editor structure with syntax highlighting, full UTF-8 support, automatic indentation, a proper clipboard and more. gedit proves that if you have the choice to use a desktop editor, you probably should.

gvim The bonkers nature and terminology of vim, transplanted kicking and screaming onto the desktop. While it’s a bit easier to navigate thanks to its graphical user interface, you may still need some vim skills to get the most out of this hardcore editor.

Sublime It’s commercial software, and the thought of paying for a text editor might put you off. But Sublime is well respected, cross-platform, and for serious coders it’s the absolute cream of the text editing crop. Take just one case: editing a variable name. In other editors you could use the standard find and replace function, but why tweek other text in your code. Sublime’s intelligent handling of syntax makes renaming variables throughout your code easy and super-quick.

# Beginning nano

Let’s take a look at nano to see how easy it is to use. First we’ll need to get it running, and it’s important to do this as a super user, otherwise it’s unlikely to have the relevant privileges. Start by opening a terminal window, and type:

```
sudo nano test.txt
```

You’ll probably be asked for your administrator password after this. The command essentially says ‘open nano (the second clause) as a super user (first clause) and edit the file test.txt (third clause). This doesn’t create the file – it’s not like creating a new text document then opening it up – it just tells nano what you want to call it and, if you like, where you want to store it.

The nano interface appears, with your cursor in the main window. Type something in, then hit [Ctrl]+[X] (Ctrl is indicated by a carrot ‘^’ symbol in the help text at the bottom of the screen) to exit nano. You’ll be asked if you want to save the modified buffer; essentially nano is asking if you want to write what’s inside its buffer (the text in its interface) to the file. Hit [Y], hit enter to confirm the filename, and nano will exit. Back at the command line, type ls and you will see your new file listed. Open it back up with the same command that we used earlier – no trying [Up] on your keyboard to move back through your previous commands to phrase it again.

Now let’s try a little cut and paste. Enter the phrase ‘the quick brown fox jumps over the lazy dog’ (good excuse to check your keyboard’s working, aren’t it?) and move your cursor to the start of ‘jumps’ with the arrow keys. Use [Ctrl]+[6] to mark the start of your cut, highlight the rest of the word and hit [Ctrl]+[K] to put it in your cut buffer. Now move to the end of the line and hit [Ctrl]+[U] to paste the contents of the cut buffer at the cursor position.

![](bbox=[0.46, 0.67, 0.78, 0.86])

> › Nano sure ain’t pretty, but if you only need to edit a file, it’s the quickest and easiest option.

> Quick tip
> If you’re using a console text editor in a terminal window, you’ll find that most of them offer mouse support for selecting characters and such.