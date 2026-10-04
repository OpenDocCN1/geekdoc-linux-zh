Putting a number before any of the commands in this block extends their function as follows:

+   - ns substitute next n characters with new text;
- ncw change n words to the right of the cursor;
- ncb change the n words before the current cursor;
- ncd change next n lines with new text.

In addition to the previous commands there are also two further change commands which can prove useful:

+   - c$ change characters to end of line for new text;
- c0 change characters to start of line for new text.

# 3.3 Command Mode

All the commands covered so far have been fairly simple, at least in terms of the number of keystrokes required to enter them. However, there are a large number of commands with a more complex structure, and also a lot of configuration options which can be set. All of these are entered via command mode. All the command mode features have one thing in common - they all start with a colon (:). As soon as you enter the colon, the cursor will jump to the start of the bottom line of the screen, where a colon will be displayed. Any characters you type now, up to a Return or Enter, will appear along the bottom line of the display so that you can check and, if necessary, correct your input.

# 3.3.1 Quit Commands

The only way you have seen to exit from the editor is to use the ZZ command in edit mode. This not only exits but also saves any changes you have made to your text back into the original file, overwriting its previous contents. It may be that you only want to exit from the editor without saving the editor contents. This can be because you have made no changes to the text or because, having changed the text, you now wish to abort the changes and quit the editor anyway. The two commands to do this are:

+   - :q quit the editor if no changes have been made;
- :q! quit the editor aborting any changes made.

It is good practice to get into the habit of using :q where you can as this will reduce the chance of typing :q! by accident, which might result in the loss of some valuable material.