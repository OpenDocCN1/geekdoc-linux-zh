# An Overview of the emacs Editor

```
---Emacs: buckaroo (Fundamental)---All---
```

2. Now I'll flip back to the other buffer with C-x b. When I enter that command, however, it doesn't automatically move me there. Instead, it offers this prompt:

```
--*-Emacs: buckaroo (Fundamental)---All----
Switch to buffer: (default dickens.note) _
```

When I type ?, I receive a split screen indicating the possible answers are:

> I found myself stealing a peek at my own watch and overhead
General Catbird's
aide give the latest.
"He's not even here," went the conversation.
"Banzai.."
"Where the hell is he?"
"At the hospital in El Paso."
"What when we weren't informed? What's wrong with him?"

```
--*Emacs: buckaroo (Fundamental)---All----
Possible completions are:
"Buffer List"
"Help"
"scratch"
dickens.note _
```

```
---Emacs: "Completions" (Fundamental)---All----
Switch to buffer: (default dickens.note) _
```

The default is okay, so I press Return and voila! I'm back in the Dickens file. One more C-x b; this time the default is buckaroo, so I again press Return to move back.

+   3. I'm in the buckaroo file, and I want to see what happens if I read dickens.note into this file. This is done easily. I move the cursor to the end of the file with M->, press

![](bbox=[0.875, 0.673, 0.998, 0.788])