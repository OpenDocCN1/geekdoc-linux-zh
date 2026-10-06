Vim will display a suggested corrections and we choose from the list. It is also possible to maintain a personal dictionary of words not found in the main dictionary, for example specialized technical terms. Vim creates the personal dictionary automatically (in ~/.vim/speli) and words are added to it when we place the cursor on the highlighted word and type:

zg

Once the word is added to our personal dictionary it will no longer be marked as misspelled by the spelling checker.

![](bbox=[0.147, 0.29, 0.82, 0.6066699999999999])

# Suggested corrections

Help topics: 'spelllang' 'spell'

#  .vimrc Tricks

Before we go, there are a few more features we can add to our .vimrc file to juice things up a bit. The first one:

```
set laststatus=2
```

This will cause vim to display a status bar near the bottom of the display. It will normally appear when more than one window is open (lastatus=1), but changing this value to 2 causes it to always be displayed regardless of the number of windows. Next, we have:

```
set ruler
```

184 Vim, with Vigor