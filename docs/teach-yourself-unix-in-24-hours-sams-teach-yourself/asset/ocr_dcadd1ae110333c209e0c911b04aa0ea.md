4. Now move back into insert mode by typing i, and enter a few sentences from a favorite book of mine:

![](bbox=[0.168, 0.187, 0.263, 0.269])

> Movie buffs perhaps will recognize the text used in this hour comes from the book Buckaroo Banzai. The film The Adventures of Buckaroo Banzai Across the Eighth Dimension is based on this very fun book.

"He's not even here," went the conservation.
"Banzai,"
"Where is is he?"
"At a hotpsial in El paso,"
"What? Why werent we informed? What's wrong with him?"_

I deliberately left some typing errors in the text here. Fixing them will demonstrate important features of the vi editor. If you fixed them as you wanted, that's okay, and if you added errors of your own, that's okay, too!

Press Escape to leave insert mode. Press Escape a second time to remind you that you're already in command mode.

+   5. Use the cursor motion keys (h, j, k, and i) to move the cursor to any point on the first line

> "He's not even here," went the conservation.
"Banzai,"
"Where is is he?"
"At the hotpsial in El paso,"
"What? Why werent we informed? What's wrong with him?"_

It turns out that I forgot a line of dialog between the line I'm on and the word Banzai. One way to enter the line would be to move to the beginning of the line "Banzai,"; insert the new text, and press Return before finding Escape to quit insert mode. But vi has a special command—oto open a line immediately below the current line for inserting text. Type o and follow along:

![](bbox=[0.055, 0.883, 0.135, 0.963])