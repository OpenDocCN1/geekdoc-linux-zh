
## SUMMARY

In this chapter, I glossed over the Qt widgets that are primarily intended to provide output mechanisms for your applications. The widgets provided are adequate by themselves for most applications. With a minimum of work, they can be combined or enhanced to provide most functionality you're likely to require.

Trolltech pulled some of the output-only widgets just prior to the 2.1 release. This was done to alleviate some of the creeping-bloat and its associated buginess that had begun to appear in the toolkit snapshot releases. The most exciting of these objects is the QCanvas widgets that manage animated sprites. I hope these will reappear in a future release.

## CHAPTER 5

### Qt Convenience Objects

No useful application was ever created from visual code alone. The following pages attempt to organize descriptions of those Qt classes that provide no direct user interaction, or are provided for convenience’s sake. The organization appears as follows:

- Event handling classes and parameters
- Input/Output related classes
- Collection, array, and linked-list classes
- Text and internationalization classes

As in the previous chapter, these descriptions are not intended to provide a reference to the various classes and parameters—they are more than adequately documented by the Qt online reference material and examples. This is intended as a possible “shopping list” of available Qt functionality, and nothing more.

## EVENTS AND EVENT PARAMETERS

Since Qt always uses the underlying window system’s mechanisms for receiving input or using timers and other such event-generating phenomena, and because all the supported window systems are event-driven, Qt is also event-driven and relies on the parameters passed to it by the underlying window system to receive keyboard input, mouse input, etc. An event is an asynchronous message that your application receives during normal processing of the Qt event loop. Qt provides default event loops in the QApplication::exec() and the QDialog::show() methods. These loops simply call the QApplication::processNextEvent() method repeatedly. As events occur, the underlying window system's platform-dependent event parameters are translated to the appropriate Qt platform-independent event format and then passed to your application as a Qt event. Your application can make use of the default "reaction" to those events, or you can create custom event handlers to alter your application's behavior.

This section discusses the standard event types, what causes those events to occur, and a few possible modifications.

### QChildEvent

When you insert or remove a child object from a QObject, a QChildEvent is passed to the parent QObject. You must reimplement the QObject::childEvent( QChildEvent * ) method in order to make use of it.

### QCloseEvent

The QWidget class provides a method QWidget::closeEvent( QCloseEvent * ) that is called when either the window menu (a function of the window manager) is used to close the widget or the widget's QWidget::close() method is explicitly called from within the program. The QCloseEvent parameter contains an accepts flag that can be used for cleanup functionality. The following example illustrates a typical use of QCloseEvent:

```cpp
void
MyMainWindow::closeEvent( QCloseEvent *e )
{
    if ( modified == true ) {
        int v = QMessageBox::information( this,
                                           "Whoa, Big Fellow",
                                           "You have changed the drawing!",
                                           "Save...", "Cancel", "Exit", 0, 1 );
        switch( v ) {
            case 0: // Save!
                save();
                e->accept();
                break;
            case 1: // Cancel
                e->ignore();
                break;
            default: // Exit
                e->accept();
                break;
        }
    } else {
        e->accept();
    }
}
```

### QCustomEvent

This class provides support for user-defined events. You can generate events using the provided QApplication::postEvent() and QApplication::sendEvent() methods. Any QWidget subclass can provide a handler by implementing a QWidget::customEvent (QCustomEvent *) method.

### QDragEnterEvent

This event is sent to a QWidget when a drag and drop object is first dragged over this QWidget. This event will be followed by one or more QDragMoveEvents, so it's only necessary to provide an implementation of one or the other. See QDragMoveEvent below.

### QDragLeaveEvent

When a drag and drop object leaves the current QWidget's “airspace,” that QWidget will receive this event.

### QDragMoveEvent

This event is sent to the QWidget under the mouse while a drag and drop action is in progress. If the QWidget accepts drag and drop events via QWidget::setAcceptDrops (bool ) and the widget accepts the event via QDragMoveEvent::accept( bool ), it is eligible to receive a QDropEvent.

### QDropEvent

This event is sent to a QWidget when the drag and drop operation is completed.

### QEvent

This is the base class of all other event classes and only contains an event type parameter. These event types are enumerated values that are documented in the QEvent reference. Since the enumerated values are subject to change, you should never use the hard-coded values to refer to, or test for, a specific event.

### QFocusEvent

QFocusEvents are generated for QWidgets as a change in focus occurs. Only the two obvious methods are provided by the class, gotFocus() and lostFocus(). The following example demonstrates a modification to QLineEdit that will select all text when the line edit receives the keyboard focus. It will also deselect the text when focus is lost:

SLineEdit.h

```cpp
#define _SLINEEDIT_H
#include <qlineedit.h>

class SLineEdit : public QLineEdit
{
    Q_OBJECT
public:
    SLineEdit( QWidget *p=0, const char *n=0 );

protected slots:
    virtual void focusInEvent( QFocusEvent * );
    virtual void focusOutEvent( QFocusEvent * );
};

#endif // _SLINEEDIT_H
```

SLineEdit.cpp

```cpp
#include "SLineEdit.h"

SLineEdit::SLineEdit( QWidget *parent, const char *name )
    : QLineEdit( parent, name )
{
}

void
SLineEdit::focusInEvent( QFocusEvent *e )
{
    QLineEdit::focusInEvent( e );
    selectAll();
    repaint( false );
}

void
SLineEdit::focusOutEvent( QFocusEvent *e )
{
    QLineEdit::focusOutEvent( e );
    setSelection( 0, 0 );
    repaint( false );
}

#include "SLineEdit.moc"
```

### QHideEvent

This event is sent to a QWidget *after* it is hidden using the QWidget::hide() method, but *before* the hide() method returns. This event is also generated whenever a top-level widget is iconified by the window manager.

### QKeyEvent

Any time a QWidget has the keyboard focus, it is eligible to receive QKeyEvents. This class provides the basic information needed to process most keystrokes, and can be easily tailored to provide additional information. The default QWidget implementation provides event handlers for keyPressEvent() and keyReleaseEvent().

### QMouseEvent

Surprisingly, the QMouseEvent class is the parameter that describes mouse events. The QWidget class provides handlers for mousePressEvent(), mouseReleaseEvent(), mouseDoubleClickEvent(), and mouseMoveEvent().

### QMoveEvent

When a widget is moved (relative to its parent) it receives a QMoveEvent. You can make use of the event by reimplementing the QWidget::moveEvent( QMoveEvent * ) method.

### QPaintEvent

Motif programmers will recognize this as an *expose* event. The event is generated when a widget needs to redraw itself. You can use QPaintEvent::rect() to obtain the QRect that represents the area that needs to be repainted.

### QResizeEvent

When a widget is resized, it receives a QResizeEvent via its QWidget::resizeEvent() method.

### QShowEvent

Show events can be generated by the underlying window system (external show events) or when the QWidget::show() method is called (internal show events), and are handled by the widget's showEvent() method. In the case of internal show events, the event is received *before* the widget is made visible.

### QTimerEvent

QTimerEvent describes a timer event as received by QObject::timerEvent() whenever the QObject has activated one or more timers. Currently, the only useful value is the timer ID of the particular timer that triggered this event. See the QTimer documentation.

### QWheelEvent

QWheelEvents are generated when the mouse wheel is rotated while the widget has focus. A special accept() method is provided by QWheelEvent to allow you to prevent the parent widget from receiving the same event.
