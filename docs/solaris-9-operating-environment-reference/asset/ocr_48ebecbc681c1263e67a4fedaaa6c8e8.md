# 1524

# vi, view, veit

+   - itextESC Insert text.
- cwnewESC Change word to new.
- easESC Pluralize word (end of word; append s; escape from input state).
- x Delete a character.
- dw Delete a word.
- dd Delete a line.
- 3dd Delete three lines.
- u Undo previous change.
- ZZ Save changes and exit.
- :qCR Discard changes and quit.
- /textCR Search for text.
- ^U ^ Scroll up or down.
- :cmCR Execute the specified ex or ed command.

# Counts Before vi Commands

You can type numbers as a prefix to some commands. Numbers are interpreted in one of these ways.

+   - z G Line/column number.
- ^D ^ Scroll amount.

most of the rest

Repeat effect.

# Interrupting, Canceling

+   - ESC End insert or incomplete command.
- DEL Delete or rub out interrupts.

# Manipulating Files

+   - ZZ If modified, write and exit; otherwise, exit.
- :wCR Write back changes.
- :w!CR Force write if permission originally not valid.
- :qCR Quit.
- :q!CR Quit, discard changes.
- :e nameCR Edit file name.
- :e!CR Reedit, discard changes.
- :e + nameCR Edit starting at end of file name.
- :e +nCR Edit starting at line n.