
## An Overview of the emacs Editor

### JUST A MINUTE

Now press Delete once to remove the last letter of the new word, and type e to reinsert it. Instead of backing up a character at a time, I am instead going to use M-Delete to delete the word just added. The word is deleted, but the spaces on other side of the word are retained.

### Preface

When I was acting, with my children and friends, in Wilkie Collins's drama of Frozen Deep, I first conceived the main idea of this story. A strong desire upon me, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular I will try to see if I can get this sentence to the way I prefer.

3. On the other hand, it's probably not good to revisit classic stories as Tale of Two Cities, the best move is for me to delete this sentence. If I press C-x Delete, which is an example of a multi-keystroke command in emacs, will it do the right thing? Recall that C-x deletes the previous sentence. If I press C-x Delete, and the results are helpful, not completely what I want to accomplish:

emacs also requires some multistroke commands, where you might press a command and follow it with a second keystroke. This allows you to have many commands to control your text, it also means you need to know many commands.

### An Overview of the emacs Editor

Finally, using C-x u three times causes the original text to be restored: Undo! If you don't have a Delete key, some of the deletion commands will be unavailable to you. Generally, though emacs has many ways to delete text as vi, if not more. The best feature is that, unlike vi, emacs remembers edit changes from the beginning of your session. You can always back up as far as you want by using C-x undo. The deletion command keys are summarized in Table 13.2.

### Table 13.2. Deletion commands in emacs.

| Command | Meaning |
| --- | --- |
| Delete | Delete the previous character. |
| C-d | Delete the current character. |
| M-Delete | Delete the previous word. |
| M-d | Delete the next word. |
| C-x Delete | Delete the previous sentence. |
| M-k | Delete the rest of the current sentence. |
| C-k | Delete the rest of the current line. |
| C-x u | Undo the last edit change. |

## Task 13.4: Search and Replace in emacs

### DESCRIPTION

Because emacs retains the line of screen for its own prompts, searching and replacing is easier than in vi. Moreover, the system prompts for the fields and asks, for each occurrence, whether to change it. On the other hand, command isn't a simple key press but rather it is an example of a named emacs command. A named emacs command is one that requires you to use its name, such as query-replace, rather than a command key.

Searching for a pattern is done by pressing C-s, and searching backward is done with C-r (mnemonic forward or reverse search). To leave the search you've found you want, press Escape, and to cancel the search, returning to your starting point, use C-g.

You might find that pressing C-s does very strange things to your system. In fact, ^s and ^q are often used as flow control on a terminal, and by pressing C-s, you're actually telling the emulator to stop sending information until it is C-q. Flow control is the protocol used by your computer and terminal to make that neither outpaces the other during data transmission. If this happens to you, you need to turn off XON/XOFF flow control. Ask your system administrator for help.

Search and replace is a whole new feature in emacs. To start a search and replace, use M-x-replace. emacs will prompt for what to do. Once a match is shown, you can type a variety of different commands to affect what happens; n makes the change; n leaves it as is but moves to the next match; Escape or q quits mode; and automatically replaces all further occurrences of the pattern without further prompting.

### ACTION

1. I'm still looking at the dickens.note file, and I have moved the cursor to the top-left corner using M-<. Somewhere in the file is the word revolution, but I'm not sure where. Worse, every time I press C-s, the terminal freezes until I press C-q, because of flow control problems. Instead of searching forward, I'll search backward by first moving the cursor to the bottom of the file with M-> and then pressing C-.

```
Emacs: dickens.note-----------Fundamental)---Bot
I-search backward:
```

As I type each character of the pattern Revolution, the cursor dances backward, matching the pattern as it grows longer and longer, until emacs finds the word I seek:

2. Now I type the query-replace feature. To begin, I move to the top of the file with M-> and then press C-x, which causes the notation to show up on the bottom status line:

I type query-replace and press Return. Emacs understands that I want to find all occurrences of a pattern and replace them with another.

I type the word I want to replace. I think I'll change French to Danish, because maybe Tale of Two Cities really takes place in London and Copenhagen. To do this, I type French and press Return. The prompt again changes this:

I type Danish, and again press Return.

I opt to make this and all other possible changes in the file, by pressing t, and the screen changes to tell me that there were no more occurrences:

### Table 13.3. Options during query and replace.

| Command | Meaning |
| --- | --- |
| y | Change this occurrence of the pattern. |
| n | Don't change this occurrence, but look for another. |
| q | Don't change this occurrence. Leave query-replace completely also can use Escape for this function). |
| ! | Change this occurrence and all others in the file. |
