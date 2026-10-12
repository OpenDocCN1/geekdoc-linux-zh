# Table 2.2 (Continued)

| Public Members | Purpose |
| :--- | :--- |
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

(continued)