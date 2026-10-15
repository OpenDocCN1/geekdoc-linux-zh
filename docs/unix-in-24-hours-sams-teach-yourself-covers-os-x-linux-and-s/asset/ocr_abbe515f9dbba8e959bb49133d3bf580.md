insert mode. But vi has a special command, o, to open a line immediately below the current line for inserting text.

Type o and follow along:

Click here to view code image

```
"He's not even here," went the conservation.
"Banzai."
"Where is he?"
"At the hotpsial in El paso."
"What? Why weren't we informed? What's wrong with him?"
~
~
```

Now type the missing text:

Click here to view code image

```
"He's not even here," went the conservation.
"Who?"
"Banzai."
"Where is he?"
"At the hotpsial in El paso."
"What? Why weren't we informed? What's wrong with him?"
~
~
```

That's it. Press Escape to return to command mode.

6. The problem with the snippet of dialog we're using is that there's no way to figure out who is talking. Adding a line above this dialog helps identify the speakers. Again, use cursor motion keys to place the cursor on the top line:

Click here to view code image

```
"He's not even here," went the conservation.
"Who?"
"Banzai."
"Where is he?"
"At the hotpsial in El paso."
"What? Why weren't we informed? What's wrong with him?"
~
~
```

Now you face a dilemma. You want to open a line for new text, but you want the line to be above the current line, not below it. It happens that vi can do that, too. Instead of using the o command, use its big brother O (that's an uppercase letter O, not a zero). When I type O, here's what I see:

Click here to view code image

```
"He's not even here," went the conservation.
"Who?"
"Banzai."
"Where is he?"
"At the hotpsial in El paso."
"What? Why weren't we informed? What's wrong with him?"
~
~
```