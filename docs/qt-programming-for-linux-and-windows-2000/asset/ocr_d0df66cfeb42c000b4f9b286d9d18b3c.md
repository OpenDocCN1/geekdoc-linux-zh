```
```
        e->accept();
    }
```
```

# QCustomEvent

This class provides support for user-defined events. You can generate events using the provided QApplication::postEvent() and QApplication::sendEvent() methods. Any QWidget subclass can provide a handler by implementing a QWidget::customEvent (QCustomEvent *) method.

# QDragEnterEvent

This event is sent to a QWidget when a drag and drop object is first dragged over this QWidget. This event will be followed by one or more QDragMoveEvents, so it's only necessary to provide an implementation of one or the other. See QDragMoveEvent below.

# QDragLeaveEvent

When a drag and drop object leaves the current QWidget's “airspace,” that QWidget will receive this event.

# QDragMoveEvent

This event is sent to the QWidget under the mouse while a drag and drop action is in progress. If the QWidget accepts drag and drop events via QWidget::setAcceptDrops (bool ) and the widget accepts the event via QDragMoveEvent::accept( bool ), it is eligible to receive a QDropEvent.

# QDropEvent

This event is sent to a QWidget when the drag and drop operation is completed.

# QEvent

This is the base class of all other event classes and only contains an event type parameter. These event types are enumerated values that are documented in the QEvent reference. Since the enumerated values are subject to change, you should never use the hard-coded values to refer to, or test for, a specific event.

# QFocusEvent

QFocusEvents are generated for QWidgets as a change in focus occurs. Only the two obvious methods are provided by the class, gotFocus() and lostFocus(). The following example demonstrates a modification to QLineEdit that will select all text when the line edit receives the keyboard focus. It will also deselect the text when focus is lost: