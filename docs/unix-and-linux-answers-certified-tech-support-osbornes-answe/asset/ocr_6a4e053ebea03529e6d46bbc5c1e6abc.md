insert mode, you can't just move down a page or over a word. And in external mode, you aren't really working with vi at all, but with ex. All this is just a bit different from most editors or word processors, and can take some getting used to. OK, a lot of getting used to.

# How do I move between modes in vi?

When you start vi, you're always in command mode. Where you go from there depends on the commands you issue. In order to switch to insert mode, type a command that expects text input (see "Inserting and Replacing Text" below). Similarly, to switch to external mode, type a command that begins with : since that's what precedes an ex command (see "Searching for (and Replacing) Text" below). To return to command mode, ESC is always the best bet.

# What do I do if I find myself suddenly in ex instead of vi?

Simply type vi to bring things back to normal. Chances are you accidentally pressed Q (that's the shifted "Q" key), which is the shortcut to ex.

# THE BASICS OF USING VI

# What is vi, and are there different versions of it available to me?

Short for "visual interface," vi is actually an extension of the ex editor, which is itself an extended version of the ed editor. Almost no one uses ed anymore, so we can forget that, and the only people who use ex are generally those stuck on some sort of terminal that won't support vi.

There are actually three versions of vi included in most implementations of UNIX—the standard one, which is mostly what we will talk about here, and the one that you start with the vi command. The second is a read-only version, useful for viewing files, that won't allow you to change files—either accidentally or on purpose. You run this version by typing view from the command line. And, finally, there is a brain-dead version for neophytes that you start by typing