If you have friends who send you mail in HTML format that you cannot conveniently read with your MUA, this little-known tip will make you happy.

⇒ To view a selection of HTML source code as rendered text, do the following:

+   1. Select the source code to render by left-clicking and dragging the mouse pointer over it (see Recipe 10.3 [Manipulating Selections of Text], page 253).
+   2. Start Lynx in a terminal so that it reads from standard input:
+      $ lynx -stdin RET
+   3. Paste the text in the terminal that is running Lynx, by clicking the middle mouse button in that terminal.
+   4. End the input to Lynx by typing CTRL-D in that terminal.

When you do this, Lynx will render and display the HTML code.

NOTES: Lynx will still be running after it displays the code, and you will then have to type Q to quit and exit Lynx. Alternately, include the -dump option to have Lynx display the rendered HTML to its standard output and then immediately exit.

Whenever you have HTML code coming out of a stream, you can pipe it to lynx -stdin -dump to display the rendered code to the standard output.

This technique is also good for testing out arbitrary selections of HTML code.

# 33.2.7 Specifying Key Bindings in Lynx

You can specify special key bindings in Lynx, so that the movement commands work just like in your favorite editor: use the -emacskeys option to enable Emacs-style key bindings, and use the -vikeys option to enable Vi-style key bindings.

⇒ To start Lynx with the URL http://nostarch.com/, using Vi-style key bindings for movement, type:

```
$ lynx -vikeys http://nostarch.com/ RET
```

# 33.2.8 Using Lynx with a Mouse

To use Lynx with the mouse, give the -use_mouse option to lynx. If your version of Lynx has mouse support enabled, giving this option will let you follow a link by just clicking on it with the left mouse button; right-click the mouse anywhere in the window to move back to the last page you visited.