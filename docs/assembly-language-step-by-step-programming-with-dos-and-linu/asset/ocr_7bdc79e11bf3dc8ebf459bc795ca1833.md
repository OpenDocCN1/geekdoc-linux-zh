In this case, the error was pretty blatant, and NASM-IDE has no trouble spotting it. That may not always be the case. There is no ironclad guarantee after spotting an error, the cursor will be placed at the location of the error. Assembly language is nothing if tricky. You have to be able to identify errors based on what you've written, not simply on where NASM-IDE suggests they may be hiding.

In this case NASM-IDE has the error to right, and you can fix the error by nuking the whole line with a quick Ctrl-Y. After that, press F2 to save the file to disk again. Then press F9 again to try the assembly process once more.

Note that the error information window will still appear. However: "No errors occurred." Every time you assemble, the error information message will appear, either with this message—or with an error message or a warning. (More on warnings later on.)

# The Executable File

If you don't see any error messages in the error information window, that means NASM got through it all right and created the executable .COM file that is the point of the whole exercise. You can run the EAT2.COM file from the DOS prompt, just like you can run any .COM or .EXE file from the DOS prompt. However, it's easier than that. NASM-IDE can run your executable program for you, right from inside NASM-IDE.

The shortcut is Ctrl-F9. If you prefer, you can pull down the Assemble and select Run. NASM-IDE will go away for a moment, and instead you'll see a blank DOS screen with the output of your program on it—in this case, the backhanded advertising slogan for Joe's Restrant. See Figure 5.5.

Getting back to NASM-IDE is no big deal: Just do as the screen instructs you, and press any key.

# NASM-IDE's Editor in Detail

NASM-IDE's beating heart, the text editor deserves a little space all to itself. People who have read earlier editions of this book (there were two, in, though the first one didn't live very long and really doesn't count) may notice a remarkable resemblance between NASM-IDE's text