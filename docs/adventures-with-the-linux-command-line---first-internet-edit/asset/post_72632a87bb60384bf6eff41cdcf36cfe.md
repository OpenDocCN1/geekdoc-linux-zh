
Using the browser is easy. To select a file or directory, we can use the up and down arrows (or Ctrl-p and Ctrl-n) to move the cursor. Press Enter will open the selected file or directory.

## :find

:find command loads a file by searching a path variable maintained by vim. :find we can specify a partial file name, and vim will attempt to locate the file and automatically complete the name when Tab key is pressed.

The action of :find command can be enhanced if the characters "***" are appended to the end of the path. The best way to do this is:

```
:set path=**
```

Adding this to the path allows :find to search directories recursively. For example, we could change the current working directory to the top of a project's source file tree and :find to load any file in the entire tree.

## wildmenu

Another cool enhancement we command command line can apply is the wildmenu. This is a highlighted bar that will appear above the command line when we are entering file names. The word "wild" in the name refers to use of the "wild" key, by default When the wild key is pressed, automatic completion is attempted with the list of possible matches displayed in the wildmenu. Using the left and right arrow keys (or Ctrl-p and Ctrl-n) allows us to choose one of the displayed items.

```
#!/bin/bash
# This is a shell script to demonstrate features in vim. It
# doesn't really do anything, it just shows what we can do.
# This program is free software: you can redistribute it in/or
# modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of
# the license, (or at your option) any later version.
# This program is distributed in the hope that it will be useful,
# but without any warranty. The expected warranty of
# FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License at -http://www.gnu.org/licenses/ for
# more details.
# Constants
# -l
bash_history logout .bashrc
```

The wildmenu

We can turn on the wildmenu with this command:

```
:set wildmenu
```

## Opening Files Named in a Document

If the document we are editing contains a file name, we can open that by placing cursor on the file name and typing either of these commands:

```
gf Open file name under cursor
^^f Open name under cursor in new window
```

Help topics: netrw :find 'path' 'wildmenu' gf ^^f

## One Does Not Live by Code Alone

While vim is most often associated with writing code of all sorts, it's good at writing ordinary prose as well. Need proof? All of the adventures were written using vim running on a Raspberry Pi!

We can configure vim to work well with text by creating a file for the file type in the ~/.ftplugin/ directory:

```
""" ~/.ftplugin/text.vim
setlocal textwidth=75
setlocal tabstop=4
setlocal shiftwidth=4
setlocal expandtab
```

Vim, with Vigor

This configuration will automatically wrap lines at word boundaries once the line exceeds 75 characters, and will set tabs to 3 spaces wide. Remember when textwidth is non-zero, vim will automatically constrain line length, and we can use the gqip command to reformat paragraphs to the specified width.

## Spell Checking

When we write, it's handy to perform spell checking while we type. Fortunately, vim can do this, too. If we add the following lines to our text.vim file, vim will help fix those pesky spell mistakes:

```
local spelllang=en_us
local dictionary=/usr/share/dict/words
local spell
```

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

![](img/9aafc495f4afbc0a97de2b31a0d13f46_192_0.png)

xterm does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

![](img/9aafc495f4afbc0a97de2b31a0d13f46_192_0.png)

xterm does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

![](img/9aafc495f4afbc0a97de2b31a0d13f46_192_0.png)

xterm does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It de-fact does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

xterm offers tabs for profiles, it does not have strange extra feature: it can display a Tektronix 4014 graphics terminal emulator window. The Tektronix 4014 was an early and expensive terminal that was compatible with computer systems in the 1970s. It's extremely obscure today. The normal text editor is called the VIM. The name comes from the DEC vt220, a popular terminal of the era, and most people use the terminal for a certain extent. xterm is not quite the same as the VT terminal, and has its own specific entry (the tout adventure for some background on Terminal). The environment variable named TERM is used by X and termfo to identify the terminal type, and thus send it the correct codes. To see the current value of the TERM variable, we can do it on the

## Highlighted misconceptions

Correcting misspelled words is very easy. Vim provides the following commands:

- s Next misspelled word
- s Previous misspelled word
- z Next misspelled word
- z Previous misspelled word
- z Display suggested corrections

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. The final line turns on the spell checker. When active, the spell checker highlights misspelled words (that is not found in the dictionary) as we type.

The first line defines the language for spell checking, in this case US English. Next, we specify the dictionary to use. Most Linux distributions include this list of words, but other dictionaries can be used. It de- does not appear to have, it actually has 3 different ones, which are made visible by holding the (Ctrl) key and pressing a mouse button. Different menus appear according to which button is pressed. The scroll bar on the side of the terminal has a behavior similar after enabling the scroll bar with menu, use the middle mouse button to drag the slider.

## Summing Up

While vim is most often associated with writing code of all sorts, it's good at writing ordinary prose as well. Need proof? All of the adventures were written using vim running on a Raspberry Pi!

We can configure vim to work well with text by creating a file for the file type in the ~/.ftplugin/ directory:

```
""" ~/.ftplugin/text.vim
setlocal textwidth=75
setlocal tabstop=4
setlocal shiftwidth=4
setlocal expandtab
```
