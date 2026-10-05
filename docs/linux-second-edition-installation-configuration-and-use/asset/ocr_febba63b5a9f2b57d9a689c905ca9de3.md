# Text mode

If you work with indents, the indented text mode be more convenient than the above procedures: this mode is activated with Alt+X text-mode. When you want to process flow text in this mode (which will normally be the case), you must also activate the appropriate minor mode with Alt+X auto-fill-mode. Minor modes define some additional commands which can be used in parallel with an arbitrary major mode – see also page 558.)

The only essential feature of the indented text mode is that, when breaking lines, Emacs automatically and without complicated preparations each new line by the same amount as the preceding one. Also, Alt+Q for manual line breaking now follows the first line indent without 'ifs' or 'bits'.

In addition, the indented text mode has two new commands: Alt+Shift+S centers the current line.

| Alt+X text-mode activates text mode Alt+X auto-fill-mode activates the minor mode for flow text Alt+Q carries out line breaking, on the basis of the current indent |
| Alt+S centers the current line |
| Alt+Shift+S centers the current paragraph |

If you want to center lines or paragraphs without switching to text mode, you can call the corresponding commands in all other modes with Alt+X center-line and Alt+X center-paragraph, respectively.

# 16.8 Searching and replacing

Incremental search

The quickest way to search for text is to use Ctrl+S search. Compared with the search commands in other editors, this command has a special feature: it starts as soon as the first character of the search has text. If, for example, you search for 'second mode' and enter Ctrl+S, the cursor jumps to the first word that starts with 'sec'. Instead of entering further characters, you can press Ctrl+S again to jump to the next word that starts with 'sec'. (If you only enter case letters, Emacs does not differentiate between upper and lower case.)

If at this point you were actually looking for 'sending mode', you delete the 'c' with Emacs jumps back to the first word (starting with the position where search began) that begins with 'se'. If you now enter the 'n', Emacs advances to the first word that starts with 'sen'. Just try it out – you will immediately love the concept!