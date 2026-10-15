This chapter is essential for all Unix guru-wannabes. If you're a Unix novice, you should start at the beginning of this chapter and work through each spread in sequence. With these basic skills mastered, you can then skip through this book and learn new skills that look useful or interesting to you. If you've used Unix before, you might peruse this chapter to review the basics and dust off any cobwebs you might have.

The skills covered in this chapter apply to any version of Unix you might be using, including Linux or BSD through your local Internet Service Provider, Solaris, AIX or HP-UX at work, your Mac OS X or Linux system at home, or any other flavor (that's the technical term) you can find. Keep in mind, though, that the exact output and prompts you see on the screen might differ slightly from what is illustrated in this book. The differences probably won't affect the steps you're completing, although you should be aware that differences could exist. (As much as possible, our examples will give you a sample of the diversity of Unix systems.)

# The SSH Preferences Dialog

In the Preferences dialog, you can fix some of the idiosyncrasies that are caused by how your SSH program talks to the Unix system. You can't identify these idiosyncrasies until you actually start using your Unix system, but you should remember that you can fix most problems here. For example:

+   ♦ If your Backspace and Delete keys don't work, look for an option in your SSH or telnet program that defines these keyboard functions.

+   ♦ If you start typing and nothing shows up onscreen, set local echo to on.

+   ♦ If you start typing and everything shows up twice, set local echo to off.

+   ♦ If you want to be able to scroll up onscreen to see what's happened during your Unix session, change the buffer size to a larger number.

Exactly which options you'll have will vary from program to program, but these are ones that are commonly available. Click OK when you're done playing with the settings.