Remember what I said in the previous hour, when I introduced the emacs editor: emacs is modeless, so be prepared for an editor that is quite unlike vi. And because it's modeless, there's no insert or command mode. The result is that you have ample opportunity to use the Control key.

![](bbox=[0.169, 0.233, 0.239, 0.29])

# JUST A MINUTE

Over years, I have tried to become an emacs enthusiast, even forcing myself to use it for an entire month. I had crib sheets of commands tapped up over my office. At the end of the month, I had attained an editing speed that was about half of my speed in vi, an editor I used thousands of times in the past 14 years I in UNIX. I think emacs has a lot going for, and generally I think modeless is better than modal software. The main obstacle I see for emacs, however, is that it's begging for pull-down menus like a Mac or Windows program. Using Control, Shift-Meta, and other weird key combinations just isn't as easy to use for me. On the other hand, your approach to editing might be different, and you might not have years of vi affecting your choice of editing environments. I encourage you to give emacs a fair shake by through all the examples I have included. You may find that it matches your working style better than vi.

# Task 13.1: Launching emacs and Inserting Text

Starting emacs is as simple as starting any other UNIX program. Simply type the name of the program, followed by any file or files you like to work. The puzzle with emacs is figuring out what is actually called on your system, if you have it. There are a couple of ways to try to identify emacs; I will demonstrate these in the “Action 2” section for this task.

Once in emacs, it's important to take a look at your keyboard. emacs requires you to use not just the Control key, but another key known as the Meta key, a sort of alternative Control key. If you have a key labeled Meta or Alt (Alternative) on your keyboard, that is the one. If not, like me, then simply press Escape every time a Meta key is identified.

Because there are both Control and Meta keys in emacs, the notation for indicating is slightly different. Throughout this book, a control-key sequence has been shown either as C-f or as M-f emacs prefers this widely, to show the difference between Control and keys. In emacs notation, f is shown as C-f, where C- always means Control. Similarly, M-x is the Meta key plus the character specified by x. If you don't have a Meta key, the sequence is Escape, followed by x. Finally, some arcane commands involve the Control and Meta keys being pressed (simultaneously with the other key) both the Control and Meta keys while typing x or if you don't have a Meta (or Alt) key, then press Escape followed by C-x.

![](bbox=[0.069, 0.903, 0.143, 0.963])

13