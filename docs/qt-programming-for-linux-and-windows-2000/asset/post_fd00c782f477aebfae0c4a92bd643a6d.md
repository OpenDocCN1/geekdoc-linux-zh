
## Chapter 2 Creating Your First Qt Application

### Table 2.2 (Continued)

| Public Members | Purpose |
| :--- | :--- |
| QRect rect() | Returns the internal geometry of the widget, without a window frame |
| QRect childrenRect() | Returns the geometry of the bounding rectangle of this widget's children |
| QRegion childrenRegion() | Returns the combined region of this widget's children |
| QSize minimumSize() | Returns the current minimum size for this widget |
| QSize maximumSize() | Returns the current maximum size for this widget |
| int minimumWidth() | Returns the current minimum width for this widget |
| int minimumHeight() | Returns the current minimum height for this widget |
| int maximumWidth() | Returns the current maximum width of this widget |
| int maximumHeight() | Returns the current maximum height of this widget |
| void setMinimumSize( const QSize & ) | Sets the minimum size of this widget |
| virtual void setMinimumSize( int minw, int minh ) | Sets the minimum width and height of this widget |
| void setMaximumSize( const QSize & ) | Sets the maximum size of this widget |
| virtual void setMaximumSize( int maxw, int maxh ) | Sets the maximum width and height of this widget |
| void setMinimumWidth( int ) | Sets the minimum width of this widget |
| void setMinimumHeight( int ) | Sets the minimum height of this widget |
| void setMaximumWidth( int ) | Sets the maximum width of this widget |
| void setMaximumHeight( int ) | Sets the maximum height of this widget |
| QSize sizeIncrement() | Returns the current size increment value (ignored on Microsoft Windows, probably ignored by the window manager) |
| void setSizeIncrement( const QSize & ) | Sets the resize increment value. Windows will resize in steps of this amount (ignored on Microsoft Windows, probably ignored by the window manager) |
| virtual void setSizeIncrement( int w, int h ) | Sets the resize increment width and height. Windows will resize in steps of this amount (ignored on Microsoft Windows, probably ignored by the window manager) |
| QSize baseSize() | Returns the current base widget size (only useful for size increments) |
| void setBaseSize( const QSize & ) | Sets the widget's base size (only useful for size increments) |
| void setBaseSize( int w, int h ) | Sets the widget's base width and height (only useful for size increments) |
| void setFixedSize( const QSize & ) | Sets a fixed size for the widget. |
| void setFixedSize( int w, int h ) | Sets a fixed width and height for the widget |
| void setFixedWidth( int ) | Sets a fixed width for the widget |
| void setFixedHeight( int ) | Sets a fixed height for the widget |
| QPoint mapToGlobal( const QPoint & ) | Translates the argument widget-relative coordinate to a global (window system) coordinate |
| QPoint mapFromGlobal( const QPoint & ) | Translates the argument global (window system) coordinate to a widget-relative coordinate |
| QPoint mapToParent( const QPoint & ) | Translates the argument widget-relative coordinate to a coordinate in the parent widget. |
| QPoint mapFromParent( const QPoint & ) | Translates the argument parent widget coordinate to a coordinate relative to this widget. |
| QWidget * topLevelWidget() | Returns a pointer to the top-level widget that is an ancestor of this widget. |
| BackgroundMode backgroundMode() | Returns the current background mode. The default is PaletteBackground |
| virtual void setBackgroundMode( BackgroundMode ) | Sets the current background mode |
| const QColor & backgroundColor() | Returns the current background color of this widget |
| const QColor & foregroundColor() | Returns the current foreground color of this widget |
| virtual void setBackgroundColor( const QColor & ) | Sets the widget's background color. This is probably not what you want! Use setPalette()! |
| const QPixmap * backgroundPixmap() | Returns a pointer to the background pixmap |
| virtual void setBackgroundPixmap( const QPixmap & ) | Wrong. It sets the background pixmap |
| const QColorGroup & colorGroup() | Returns the current color group |
| const QPalette & palette() | Returns the current palette for the widget. If no custom palette has been set for this widget, this method returns the widget class palette, the parent's palette, or the application palette |
| virtual void setPalette( const QPalette & ) | Sets a new palette for this widget |
| void unsetPalette() | Removes a custom palette, restoring the default |
| QFont font() | Returns the current widget font |
| virtual void setFont( const QFont & ) | Sets a custom font for this widget |
| void unsetFont() | Removes the custom font, restoring the default |
| QFontMetrics fontMetrics() | Returns the current font metrics for this widget |
| QFontInfo fontInfo() | Returns the current font information |
| const QCursor & cursor() | Returns the current cursor used when the mouse is over this widget |
| virtual void setCursor( const QCursor & ) | Sets the cursor shape that will appear when the mouse pointer is over this widget |
| virtual void unsetCursor() | Removes custom cursor settings, restoring the default |
| QString caption() | Returns the current widget caption (window frame title bar on top-level widgets) |
| const QPixmap * icon() | Returns a pointer to the pixmap that is currently set as this widget's icon |
| QString iconText() | Returns the icon text (if it has been set, otherwise it returns NULL) |
| bool hasMouseTracking() | Returns true if mouse tracking is enabled for the widget. |
| virtual void setMask( const QBitmap& ) | Sets a widget mask from the argument bitmap that controls how the widget is clipped (this is how you create round buttons). |
| virtual void setMask( const QRegion& ) | Sets a widget mask from the argument region information that controls how the widget is clipped. |
| void clearMask() | Disables widget masking from a previous setMask() |
| bool isActiveWindow() | Returns true if this widget is in the active window |
| virtual void setActiveWindow() | Sets this window to be active |
| bool isFocusEnabled() | Returns true if this widget can receive keyboard focus |
| FocusPolicy focusPolicy() | Returns the current focus policy of the widget. |
| virtual void setFocusPolicy( FocusPolicy ) | Sets or changes the current focus policy of the widget |
| bool hasFocus() | Returns true if this widget has keyboard focus |
| virtual void setFocusProxy( QWidget * ) | Sets the argument widget to proxy keyboard focus for this widget |
| QWidget* focusProxy() | Returns the widget that proxies the keyboard focus for this widget (Null if none) |
| void grabMouse() | Grabs the mouse input. No other widget will receive mouse input until releaseMouse() is called |
| void grabMouse( const QCursor& ) | Grabs the mouse input and changes the mouse appearance to that of the argument. No other widget will receive mouse input until releaseMouse() is called |
| void releaseMouse() | Releases the mouse after a widget has called grabMouse() |
| void grabKeyboard() | Grabs the keyboard input. No other widget will receive keyboard input until releaseKeyboard() is called |
| void releaseKeyboard() | Releases the keyboard after a widget has called grabKeyboard() |
| bool isUpdatesEnabled() | Returns true if updates to this widget are enabled |
| virtual bool close( bool ) | Closes the widget. If the argument is true, the widget will be deleted along with its children |
| bool isVisible() | Returns true if the widget is (or could be) visible. A widget obscured by another widget could be visible in this sense |
| bool isVisibleTo( QWidget * ) | Returns true if this widget would become visible if the argument ancestor widget is made visible |
| QRect visibleRect() | Returns the currently visible rectangle of the widget |
| bool isMinimized() | Returns true if this widget is minimized |
| virtual QSize sizeHint() | Usually overridden in a subclass, this method returns a suitable size for this widget |
| virtual QSize minimumSizeHint() | Usually overridden in a subclass, this method returns the smallest usable size for this widget |
| virtual QSizePolicy sizePolicy() | Returns the current size policy of this widget. Widgets such as QPushButton and QLineEdit "like" to grow/shrink horizontally but not vertically. This is an effect of QSizePolicy values |
| virtual int heightForWidth( int ) | Returns a preferred height, given an argument width. The default returns zero (doesn't care). This does not take layouts into account. |
| virtual void adjustSize() | Adjusts the size of this widget to fit the content underneath. Uses sizeHint() if it's valid, otherwise it attempts to fit the bounding rectangles of child widgets |
| QLayout * layout() | Returns a pointer to the QLayout that manages this widget's children or NULL if no layout is in use |
| void updateGeometry() | Notifies a layout that this widget's geometry has changed. |
| virtual void reparent( QWidget *parent, WFlags, const QPoint & bool show=FALSE ) | Reparents the argument widget to this widget, positioning it at the argument point and applying the argument window flags to it. If show == true, the widget will be shown immediately |
