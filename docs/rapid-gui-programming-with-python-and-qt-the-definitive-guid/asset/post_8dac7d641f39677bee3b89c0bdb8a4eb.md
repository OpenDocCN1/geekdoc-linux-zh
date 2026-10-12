
# 10

## The Event-Handling Mechanism
## Reimplementing Event Handlers
## Using the Clipboard
## Drag and Drop

# Events, the Clipboard, and Drag and Drop

In this short chapter we begin by describing the key concepts involved in event handling. In the second section we build on this knowledge to show how to control a widget's behavior and appearance by reimplementing low-level event handlers. Later chapters build on the material covered in the first two sections, particularly Chapter 11, which shows how to create custom widgets.

The chapter's third section shows how to use the clipboard, and in particular how to pass and retrieve plain text, HTML, and images to and from the system's global clipboard. The last section shows how to implement drag and drop, both by using PyQt's easy-to-use built-in functionality, and by handling it ourselves to drag and drop custom data. The exercise builds on the coverage of dragging and dropping custom data to allow the user to choose whether to move or copy when dropping.

# The Event-Handling Mechanism

PyQt provides two mechanisms for dealing with events: the high-level signals and slots mechanism, and low-level event handlers. The signals and slots approach is ideal when we are concerned with what actions the user wants to perform, without getting bogged down in the details of how specifically they asked. Signals and slots can also be used to customize some aspects of how widgets behave. But when we need to go deeper, particularly when creating custom widgets, we need to use low-level event handlers.

PyQt provides a rich variety of event handlers, some concerned with widget behavior, such as those that handle key presses and mouse events, and others concerned with widget appearance, such as those that handle paint events and resize events.

PyQt's event-handling mechanism works in the logical way we would expect. For example, if the user clicks the mouse or presses a key on a widget with keyboard focus, the widget is given the event. If the widget handles the event, that is the end of the story. But if the widget does not handle the event, the event is propagated to the widget’s parent—another benefit of PyQt’s parent-child hierarchy. This passing of unhandled events from child to parent continues right up to the top-level widget, and if that doesn’t handle the event, the event is simply thrown away.

PyQt provides five different ways of intercepting and handling events. The first two approaches are the most heavily used, with the others needed rarely, if ever.

The simplest approach is to reimplement a specific event handler. So far, we have seen just one example of this: the reimplementation of a widget’s closeEvent(). As we will see in this chapter and in subsequent chapters, we can control a widget’s behavior by reimplementing other event handlers—for example, keyPressEvent(), mousePressEvent(), and mouseReleaseEvent(). We can also control a widget’s appearance by reimplementing releaseEvent() and paintEvent(). When we reimplement these events we often don’t call the base class implementation since we want our own code executed only as a result of the event handler being called.

Before any specific event handler is called, the event() event handler is called. Reimplementing this method allows us to handle events that cannot be handled properly in the specific event handlers (in particular, overriding the Tab key’s keyboard focus changing behavior), or to implement events for which no specific handler exists, such as QEvent.ToolBarChange. When we reimplement this handler, we call the base class implementation for any events we don’t handle ourselves.

The third and fourth approaches use event filters. We can call installEventFilter() on any QObject. This will mean that all events for the QObject are passed to our event filter first; we can discard or modify any of the events before they reach the target object. An even more powerful version of this approach is to install an event filter on the QApplication object, although its only practical uses are for debugging and for handling mouse events sent to disabled widgets. It is possible to install multiple event filters on an object or on Q-application, in which case they are executed in order from most to least recently installed.

Event filters provide a very powerful means of handling events, and newcomers to PyQt programming are often tempted to use them. But we recommend avoiding the use of event filters, at least until you have a lot of PyQt programming experience. If very large numbers of event filters are installed, application performance can suffer; also, they can considerably increase code complexity compared with simply reimplementing specific event handlers, or the event() handler. We will not look at any event filter examples, since they should be avoided in general PyQt programming—they are really relevant only when creating custom widgets—and even then they are rarely necessary.

![](img/9bfe0a027fcc8793bb087287001100dd_318_0.png)

The fifth approach is to subclass QApplication and reimplement its notify() method. This method is called before any event filter or event handler, so it provides the ultimate in control. In practice, this would be done only for debugging, and even then, using event filters is probably more flexible.

# Reimplementing Event Handlers

The screenshot in Figure 10.1 shows a QWidget subclass that has some reimplemented event handlers. The Events application in chap19/events.pyw reports certain events and conditions, and we will use it to see how event handling is done in PyQt. Later chapters use the same techniques that we describe here to do much more sophisticated and realistic event handling. We will begin by looking at an extract from the application's initializer to see its instance data.

![](img/9bfe0a027fcc8793bb087287001100dd_319_0.png)

```python
class Widget(QWidget):
    def __init__(self, parent=None):
        super(Widget, self).__init__(parent)
        self.justDoubleClicked = False
        self.key = QString()
        self.text = QString()
        self.message = QString()
```

We hold the text of the most recent key press in key, the text to be painted—for example, "The mouse is at…"—in text, and a message text in message. We also keep track of whether the user has just done a double-click.

The first event handler we will consider is the paint event. We will defer a proper discussion of painting to Chapter 11.

```python
def paintEvent(self, event):
    text = self.text
    i = text.indexOf("\n\n")
    if i >= 0:
        text = text.left(i)
    if not self.key.isEmpty():
        text += "\nYou pressed: %s" % self.key
    painter = QPainter(self)
    painter.setRenderHint(QPainter.TextAntialiasing)
    painter.drawText(self.rect(), Qt.AlignCenter, text)
    if self.message:
        painter.drawText(self.rect(),
                         Qt.AlignBottom|Qt.AlignHCenter, self.message)
        QTimer.singleShot(5000, self.message.clear)
    QTimer.singleShot(5000, self.update)
```

The text to be displayed consists of two parts. The first part usually contains the mouse coordinates, and the second part (which may be empty) contains the last key that the user pressed. In addition, `message` text may be painted at the bottom of the widget, in which case the single-shot timers clear the message text after 5 seconds and schedule a paint event to repaint the widget without the message text.

In paint events it is quite common to ignore the event as we have done here. (The event can tell us the exact region that needs repainting so it can be used to optimize painting by just painting the region that needs updating, a technique we will use in Chapter 16.) The `rect()` method returns a `QRect` with the widget’s dimensions, so we simply draw the text centered in the given rectangle. We do not call the base class’s paint event; this is standard practice in PyQt paint event handlers, and in any case, the `QWidget` paint event does nothing.

```python
def resizeEvent(self, event):
    self.text = (QString('Resized to QSize(%d, %d)' %
                     event.size().width(),
                     event.size().height()))
    self.update()
```

Whenever the widget is resized—for example, by the user dragging a corner or side—a resize event is generated. We set our instance text to show the new size, and call `update()` to schedule a paint event. A resize event also has the previous size, available from the `QResizeEvent.oldSize()` method. We do not call the base class’s resize event, since it does nothing.

```python
def keyPressEvent(self, event):
    self.key = QString()
    if event.key() == Qt.Key_Home:
        self.key = "Home"
    elif event.key() == Qt.Key_End:
        self.key = "End"
    elif event.key() == Qt.Key_PageUp:
        if event.modifiers() & Qt.ControlModifier:
            self.key = "Ctrl+PageUp"
        else:
            self.key = "PageUp"
    elif event.key() == Qt.Key_PageDown:
        if event.modifiers() & Qt.ControlModifier:
            self.key = "Ctrl+PageDown"
```
