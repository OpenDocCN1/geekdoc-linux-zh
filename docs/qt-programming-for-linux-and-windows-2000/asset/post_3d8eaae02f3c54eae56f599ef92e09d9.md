
## Table 2.1 (Continued)

| Static Public Members | Purpose |
| :--- | :--- |
| bool closingDown() | Returns true if the application objects are being destroyed |
| void flushX() | Flushes the X11 event queue (only valid for X11) |
| void syncX() | Causes the Qt notion of the application display to synchronize with the X server (only valid for X11) |
| void beep() | Sounds the platform bell |
| void setDesktopSettingsAware( bool ) | When the false argument is used, Qt's default behavior of using system default fonts, colors, etc., is disabled |
| bool desktopSettingsAware() | Returns false if the standard behavior of inheriting desktop font and color settings has been disabled |
| void setCursorFlashTime( int ) | Sets the number of milliseconds for the total time period of a text cursor blink |
| int cursorFlashTime() | Returns the total time period for a text cursor blink |
| void setDoubleClickInterval( int ) | Sets the mouse's double-click interval in milliseconds |
| int doubleClickInterval() | Returns the current mouse double-click interval in milliseconds |
| void setWheelScrollLines( int ) | Sets the number of lines to scroll when the mouse wheel is rotated |
| int wheelScrollLines() | Returns the current number of lines to scroll when the mouse wheel is rotated |
| void setStartDragTime( int ) | Specifies the time delay, in milliseconds, between the time the mouse button is pressed and the time a drag event begins |
| int startDragTime() | Returns the current delay, in milliseconds, between the time the mouse button is pressed and a drag event begins |
| void setStartDragDistance( int ) | Specifies the distance the mouse must move following a mouse click before it is interpreted as a drag event |
| int startDragDistance() | Returns the distance the mouse must move following a mouse click before it is interpreted as a drag event |

## QApplication's Purposes

The QApplication class functions as the main interface between your application and the underlying window system and serves as a base object for all of the visual components of that application. The following features will give you an overview of functionality the QApplication class provides:

- QApplication encapsulates the *look and feel* of the application by means of a concept referred to as *Style*. The global style can be changed at runtime using the QApplication::setStyle() method. You can exercise per-widget style control as well, but it tends to make the interface confusing. Styles themselves are encapsulated via QStyle.

- QApplication specifies how the application will allocate and use colors via the QApplication::setColorSpec() method. *You must set the color specification before you instantiate the QApplication object itself, or the specification will have no effect.* (The Qt color allocation model is discussed below.)

- QApplication sets the default text codec (see QApplication::setDefaultCodec()), which defines how strings will be localized or translated via the QApplication::translate() method.

- QApplication encapsulates some extremely platform-dependent concepts, such as the “desktop” and the “clipboard,” so that your application will work as you expect on whatever platform you deploy it. The Trolls define this as “Troll magic”—but it’s just a lot of hard work on their part.

- QApplication provides adequate window interaction and management functionality through the methods QWidget::widgetAt(), QWidget::topLevelWidgets(), and QWidget::closeAllWindows().

- QApplication provides the event dispatch mechanisms that every application needs; i.e., it receives events from the underlying window system and sends them to the appropriate widgets. You can use QApplication::postEvent() and QApplication::sendEvent() to send your own messages to your application’s widgets. What could be more fun than that?

- QApplication manages how mouse events are handled and provides adequate control for customizing this handling via QApplication::setOverrideCursor() and QApplication::setGlobalMouseTracking(). You will hardly ever use these functions, however; you can usually accomplish the desired effect at the QWidget level.

- In X11 environments, QApplication provides methods to control the X11 protocol stream via QApplication::flushX() and QApplication::syncX().

- QApplication provides the needed framework to implement full session management control—even on a Microsoft Windows platform. This functionality is provided via the QSessionManager class and the QApplication::isSessionRestored(), QApplication::sessionId(), QApplication::commitData(), and QApplication::saveState() methods.

## Color Management

Qt provides several methods of managing color allocation for your application. If you are primarily used to X11 programming, you have no doubt read the MIT documentation on the subject and have scars from scratching your head to prove it. The X11 color models for the various visual types can be confusing. Qt makes color allocation simple and predictable for most (not all) applications, and the QApplication class plays a significant role in that simplicity.

Qt provides more options on X11 platforms than on Microsoft Windows platforms, but the usage is consistent and simple. Qt manages color allocation in one of several ways, depending on the use of QApplication::setColorSpec() and QColor::enterColorContext().

QApplication::setColorSpec() accepts an enumerated value that is one of the following:

- **QApplication::NormalColor**—This is the default. It causes your application to use the default system colors, which will work well for any application that uses very little color. This can lead to noticeable color dithering on Windows platforms.

- **QApplication::CustomColor**—This setting is useful for applications that have a small number of specific colors that must be allocated. This setting has no effect on X11 platforms as compared with the default setting. On Windows systems, this setting causes a new color palette to be created and colors are allocated from it as needed.

- **QApplication::ManyColors**—This setting is appropriate when your application will need many (even thousands of) colors.

You can gain an additional degree of color allocation control at application runtime via the QColor::enterColorContext() method, which permits the application to allocate many colors on a temporary basis. But if your application's help file refers to the name Pantone anywhere, you will need to add your own refinements to QColor to get the exact color you're after.

## QWIDGET CLASS

QWidget is the abstraction of a user interface object and is the atom of Qt interface design. QWidget provides a great deal of functionality and performs many useful tasks. It receives events from the underlying window system and provides the methods you will most likely need to put those events to work. It maintains properties such as the font and a color palette, although it doesn't directly use them. All of the visual objects in the Qt toolkit are a subclass of QWidget, so all of the visual objects inherit QWidget methods and functionality. Table 2.2 represents the methods exposed by the QWidget class:

### Table 2.2 QWidget Class Methods

| Public Members | Purpose |
| :--- | :--- |
| QWidget( QWidget *parent=0, const char *name=0, WFlags f=0 ) | Constructor. The default behavior, with a widget argument equal to zero, constructs a top-level widget |
| QWidget ( ) | Destructor |
| QWidget ID | Returns a platform-independent window ID |
| QStyle & style() | Returns the current Qt style of this widget |
| void setStyle( QStyle * ) | Sets a new style for this widget |
| bool isTopLevel( ) | Returns true if this is a top-level widget |
| bool isModal( ) | Returns true if this widget is modal (true implies top-level) |
| bool isPopup( ) | Returns true if this widget has the WType_Popup flag set |
| bool isDesktop( ) | Returns true if this widget refers to the desktop |
| bool isEnabled( ) | Returns true if this widget is enabled |
| bool isEnabledTo( QWidget * ) | Returns true if this widget would be enabled or disabled along with the argument widget |
| QRect frameGeometry( ) | Returns the geometry of this widget relative to its parent (including the window frame) |
| const QRect & geometry( ) | Returns the geometry of this widget relative to its parent |
| int x( ) | Returns the x coordinate of this widget, relative to its parent |
| int y( ) | Returns the y coordinate of this widget, relative to its parent |
| QPoint pos( ) | Returns the QPoint coordinate of this widget, relative to its parent |
| QSize frameSize( ) | Returns the size of the window system frame (only valid for top-level widgets) |
| QSize size( ) | Returns the size of the widget |
| int width( ) | Returns the width (in pixels or pels) of the widget |
| int height( ) | Returns the height (in pixels or pels) of the widget |
