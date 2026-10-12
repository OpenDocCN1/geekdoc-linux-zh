+   - Dumb Dialogs
+   - Standard Dialogs
+   - Smart Dialogs

# ## 5

## Dialogs

Almost every GUI application has at least one dialog, and the majority of GUI applications have one main window with dozens or scores of dialogs. Dialogs can be used to make announcements that are too important to put in the status bar or into a log file. In such cases, they typically just have a label for the text and an OK button for the user to press when they’ve read the message. Mostly, dialogs are used to ask users questions. Some are simple and need just a yes or no answer. Others ask users to make another kind of choice—for example, what file, folder, color, or font to use. For all these, PyQt provides built-in dialogs.

Our focus in this chapter is on creating custom dialogs so that we can ask users for their requirements and preferences when none of the built-in dialogs is suitable.

One question that we do not address, concerns which widget is suitable for a particular purpose. For example, if we want a user to make a choice between three options, we might provide three radio buttons, a three-item list widget or combobox. Or we might use a tri-state checkbox. And these are not the only possibilities. For those new to GUI programming, Appendix B provides screenshots and brief descriptions of selected PyQt widgets which may be helpful when making these decisions.

Qt is supplied with *Qt Designer*, a visual design tool that makes it easy to “draw” dialogs without having to write any code for creating and laying out their widgets. It can also be used to set up some of a dialog’s behavior. We cover *Qt Designer* later, in Chapter 7. In this chapter we will create all the dialogs in code. Some developers make all their dialogs this way, and others prefer to use *Qt Designer*. This book shows both approaches so that you can decide which is best to use on a case-by-case basis.

One way to classify dialogs is by their “intelligence”, where they may be “dumb”, “standard”, or “smart”, depending on how much knowledge about the application’s data is built into them. These classifications affect how we implement and instantiate (create instances of) dialogs, and for each one we have