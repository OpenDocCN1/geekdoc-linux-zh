
passed a Boolean—True to stop the object emitting signals and False to resume signalling.

This completes our formal coverage of the signals and slots mechanism. We will see many more examples of signals and slots in practice in almost all the examples shown in the rest of the book. Most other GUI libraries have copied the mechanism in some form or other. This is because the signals and slots mechanism is very useful and powerful, and leaves programmers free to focus on the logic of their applications rather than having to concern themselves with the details of how the user invoked a particular operation.

# Summary

In this chapter, we saw that it is possible to create hybrid console—GUI applications. This can actually be taken much further—for example, by including all the GUI code within the scope of an if block and executing it only if PyQt is installed. This would allow us to create a GUI application that could fall back to “console mode” if some of our users did not have PyQt.

We also saw that unlike conventional batch-processing programs, GUI applications have an event loop that runs continuously, checking for user events like mouse clicks and key presses, and system events like timers timing out or windows being revealed, and terminating only when requested to do so.

The Calculate application showed us a very simple but structurally typical dialog `__init__()` method. The widgets are created, laid out, and connected, and one or more other methods are used to respond to user interaction. The Currency application used the same approach, only with a more sophisticated interface, and more complex behavior and processing. The Currency application also showed that we can connect multiple signals to a single slot without formality.

PyQt’s signals and slots mechanism allows us to handle user interaction at a much higher level of abstraction than the specific details of mouse clicks and key presses. It lets us focus on what users want to do rather than how they asked to do it. All the PyQt widgets emit signals to announce state changes and other important occurrences; and most of the time we can ignore the signals. But for those signals that we are interested in, it is easy to use `QObject.connect()` to ensure that the function or method of our choice is called when the signal is emitted so that we can respond to it. Unlike C++/Qt, which must designate certain methods specially as slots, in PyQt we are free to use any callable, that is, any function or method, as a slot.

We also saw how to connect multiple signals to a single slot, and how to use partial function application or the `sender()` method so that the slot can respond appropriately depending on which widget signalled it.

We also learned that we do not have to formally declare our own custom signals: We can simply emit them using `QObject.emit()`, along with any additional parameters we want to pass.

## Exercise

Write a dialog-style application that calculates compound interest. The application should be very similar in style and structure to the Currency application, and should look like this:

![](img/9bfe0a027fcc8793bb087287001100dd_151_0.png)

The amount should be automatically recalculated every time the user changes one of the variable factors, that is, the *principle, rate, or years*. The years combobox should have the texts “*1 year*”, “*2 years*”, “*3 years*”, and so on, so the number of years will be the combobox’s current index + 1. The compound interest formula in Python is `amount = principal * ((1 + (rate / 100.0)) ** years)`. The `QDoubleSpinBox` class has `setPrefix()` and `setSuffix()` methods which can be used for the “$” and “%” symbols. The whole application can be written in around 60 lines.

Hint: The updating can be done by connecting suitable spinbox and combobox signals to an `updateUi()` slot where the calculations are performed and the amount label is updated.

A model answer is provided in the file `chap04/interest.pyy`.

- Dumb Dialogs
- Standard Dialogs
- Smart Dialogs

# Chapter 5
## Dialogs

Almost every GUI application has at least one dialog, and the majority of GUI applications have one main window with dozens or scores of dialogs. Dialogs can be used to make announcements that are too important to put in the status bar or into a log file. In such cases, they typically just have a label for the text and an OK button for the user to press when they’ve read the message. Mostly, dialogs are used to ask users questions. Some are simple and need just a yes or no answer. Others ask users to make another kind of choice—for example, what file, folder, color, or font to use. For all these, PyQt provides built-in dialogs.

Our focus in this chapter is on creating custom dialogs so that we can ask users for their requirements and preferences when none of the built-in dialogs is suitable.

One question that we do not address, concerns which widget is suitable for a particular purpose. For example, if we want a user to make a choice between three options, we might provide three radio buttons, a three-item list widget or combobox. Or we might use a tri-state checkbox. And these are not the only possibilities. For those new to GUI programming, Appendix B provides screenshots and brief descriptions of selected PyQt widgets which may be helpful when making these decisions.

Qt is supplied with *Qt Designer*, a visual design tool that makes it easy to “draw” dialogs without having to write any code for creating and laying out their widgets. It can also be used to set up some of a dialog’s behavior. We cover *Qt Designer* later, in Chapter 7. In this chapter we will create all the dialogs in code. Some developers make all their dialogs this way, and others prefer to use *Qt Designer*. This book shows both approaches so that you can decide which is best to use on a case-by-case basis.

One way to classify dialogs is by their “intelligence”, where they may be “dumb”, “standard”, or “smart”, depending on how much knowledge about the application’s data is built into them. These classifications affect how we implement and instantiate (create instances of) dialogs, and for each one we have devoted a section of this chapter. Each of these sections begins with an explanation of what the classification means, and explains the pros and cons through a worked example.

In addition to an intelligence classification, dialogs can also be categorized by their *modality*. An **application modal** dialog is a dialog that, once invoked, is the only part of an application that the user can interact with. Until the user closes the dialog, they cannot use the rest of the application. The user is, of course, free to interact with other applications, for example, by clicking one to give it the focus.

A **window modal** dialog is one that works in a similar way to an application modal dialog, except that it only prevents interaction with its parent window, parent's parent window, and so on up to the top-level parent, as well as the parent window's sibling windows. For applications that have a single top-level window there is no practical difference between application modality and window modality. When referring to a "modal" window without specifying which kind, window modality is assumed.

The opposite of a modal dialog is a *modeless* dialog. When a modeless dialog is invoked, the user can interact with the dialog, and with the rest of the application. This has implications for how we design our code, since it may be that the user can affect program state both in the main window and in the modeless dialog, which then has an effect on the other.

Another important aspect of writing dialogs is how we handle validation. Wherever possible we try to choose suitable widgets and set their properties to avoid having to write any validation code ourselves. For example, if we need an integer we could use a *QSpinBox* and use its *setRange()* method to constrain the range to the values that are acceptable to us. We call validation that applies to individual widgets "widget-level" validation; database programmers often call this "field-level" validation. Sometimes we need to go further than widget-level validation, particularly when there are interdependencies. For example, a theater booking system might have two comboboxes, one to select a floor and the other to select a seat row. If the ground floor had seat rows A–R, and the first floor had seat rows M–T, then clearly not some floor and seat row combinations are valid. For these cases, we must perform "form-level" validation; database programmers often call this "record-level" validation.

Another validation issue concerns when the validation takes place. Ideally we don't want users to be able to enter invalid data at all, but sometimes this can be quite tricky to prevent. We break validation into two broad categories: "post-mortem", which is validation that takes place at the point when the user wants to have their settings accepted, and "preventative", which takes place as the user manipulates editing widgets.

Since dialogs can have different levels of intelligence, three kinds of modality, and a variety of validation strategies, it would appear that there are many possible combinations to choose from. In practice, the combinations we use
