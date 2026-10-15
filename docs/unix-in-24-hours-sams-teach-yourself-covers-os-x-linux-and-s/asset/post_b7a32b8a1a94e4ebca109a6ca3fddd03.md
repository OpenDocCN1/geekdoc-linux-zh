
--Emacs: *Completions*      (Fundamental)--All-----
Switch to buffer: (default dickens.note) _

The default is okay, so I press Return. Voilà! I’m back in the Dickens file. One more C-x b; this time the default is buckaroo, so I again press Return to move back.

## 3. I’m in the buckaroo file, and I want to see what happens if I read

dickens.note into this file. This is done easily. I move the cursor to the end of the file with M->, press C-x i, and answer dickens.note to the prompt Insert file: ~/. Pressing Return yields the following screen display:

Click here to view code image

```
I found myself stealing a peek at my own watch and overheard
General Catbird’s
aide give him the latest.
"He’s not even here," went the conversation.
"Who?"
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren’t we informed? What’s wrong with him?"

    A Tale of Two Cities
    Preface

When I was acting, with my children and friends, in Mr Wilkie
Collins’s drama of The Frozen Deep, I first conceived the main idea
of this story. A strong desire came upon me then, to
embody it in my own person;
and I traced out in my fancy, the state of mind of which it would
necessitate the presentation
to an observant spectator, with particular
care and interest.

As the idea became familiar to me, it gradually shaped itself into
its present form. Throughout its execution, it has had complete possession
--**Emacs: buckaroo      (Fundamental)--Top-----
```

## 4. It’s time to quit and split. To do this, I press C-x s and wait for an emacs prompt or two. The first one displayed is this:

Click here to view code image

```
As the idea became familiar to me, it gradually shaped itself into
its present form. Throughout its execution, it has had complete possession
--**Emacs: buckaroo      (Fundamental)--Top-----
Save file /users/taylor/buckaroo? (y or n) _
```

I answer y to save this muddled file. I’m returned to the top of the file, and a quick C-x C-c drops me back to the system prompt.

One of the more useful facets of emacs you have learned about is the capability to work with multiple files.

## Summary

You have now learned quite a bit about the emacs editor. Some capabilities exceed those of the vi editor, and some are considerably more confusing. Which of these editors you choose is up to you, and your choice should be based on your own preferences for working on files. You should spend some time working with the editor you prefer, making sure that you can create simple files and modify them without any problems.

## Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

## Key Terms

- **buffer**: An area of the screen used to edit a file in emacs, the buffer actually represents a portion of memory used to store that information.
- **flow control**: The protocol used by a computer and terminal to make sure that neither outpaces the other during data transmission.
- **key bindings**: This is the emacs term for key mapping.
- **Meta key**: A key that is labeled either Meta or Alt on a keyboard. It is used much like the Control key in keyboard shortcuts.
- **named emacs command**: Some commands in emacs require you to type the command name, such as query-replace, rather than use a command key or two.
- **XON/XOFF**: This is a particular type of flow control in which the receiving end can send an XON (delay transmission) character until it’s ready for more information, when it sends an XOFF (resume transmission).

## Exercises

- 1. How do you get to the emacs help system?
- 2. Check your keyboard. If you don’t have a Meta or Alt key, what alternative strategy can you use to enter commands such as M-x?
- 3. What’s the command sequence for leaving emacs when you’re done?
- 4. What was the problem you might have with the Delete key? How can you solve that problem? What’s the alternative delete command if Delete isn’t available?
- 5. How do you do global search-and-replace in emacs, and what key do you press to stop a global search-and-replace when you are prompted for confirmation at the first match?
- 6. Use the emacs help system to list the emacs copyright information. What’s your reaction?
