your source code file to an executable or an object code file. I explain more about the concept of the current file later in this book. Typically, unless you begin doing fancier things, the current file will simply be the source code file you have open in an edit window.

# Moving Around the Edit Window

When you're in NASM-IDE and an assembly language source code file is displayed in an edit window, any characters you type on the keyboard will be inserted into the file and displayed on your screen. You can move the cursor around within the current file using any of a number of cursor movement keys.

The easiest to remember are the PC's cursor keypad keys. The four arrow keys will move the cursor one character position in the arrow points. The PgUp key will move the cursor up one page (that is, the size of your text screen; typically 25, 43, or 50 lines depending on how you set it up—more than shortly) whereas PgDn will move the cursor one page down. The Home key will move the cursor immediately to the left margin, and the End key will move the cursor immediately to the end of the current line. (The end of the line is defined as the character after the rightmost nonblank character in the line.)

There are numerous cursor movement keys that you can use within JED. I describe them all in detail later in this chapter. You can also zain on a particular location in the file by clicking on a character with the mouse. The cursor will move immediately to the point at which you clicked. You can use the mouse to slide up and down within the file by clicking on the “thumb” of the scroll bar on the right-hand edge of the edit window, and dragging the thumb up or down. (The thumb is a small rectangle set into the scroll bar.)

Take a few moments scooting around inside EAT2.ASM until you feel comfortable with it.

# Making Changes to the File

The simplest way to change the file is simply to type something at the keyboard. All such characters will appear at the cursor, and the cursor will move one position to the right for each character.