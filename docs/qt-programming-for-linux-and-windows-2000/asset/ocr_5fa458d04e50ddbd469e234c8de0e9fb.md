# Table 2.2 (Continued)

| Public Members | Purpose |
| :--- | :--- |
| `virtual void`<br>`setBackgroundcolor( const QColor & )` | Sets the widget's background color.<br>This is probably not what you want!<br>**Use setPalette()!** |
| `const QPixmap *`<br>`backgroundPixmap()` | Returns a pointer to the background pixmap |
| `virtual void`<br>`setBackgroundPixmap( const QPixmap & )` | Wrong. It sets the background pixmap |
| `const QColorGroup &`<br>`colorGroup()` | Returns the current color group |
| `const QPalette &`<br>`palette()` | Returns the current palette for the widget. If no custom palette has been set for this widget, this method returns the widget class palette, the parent's palette, or the application palette |
| `virtual void`<br>`setPalette( const QPalette & )` | Sets a new palette for this widget |
| `void`<br>`unsetPalette()` | Removes a custom palette, restoring the default |
| `QFont`<br>`font()` | Returns the current widget font |
| `virtual void`<br>`setFont( const QFont & )` | Sets a custom font for this widget |
| `void`<br>`unsetFont()` | Removes the custom font, restoring the default |
| `QFontMetrics`<br>`fontMetrics()` | Returns the current font metrics for this widget |
| `QFontInfo`<br>`fontInfo()` | Returns the current font information |
| `const QCursor &`<br>`cursor()` | Returns the current cursor used when the mouse is over this widget |
| `virtual void`<br>`setCursor( const QCursor & )` | Sets the cursor shape that will appear when the mouse pointer is over this widget |
| `virtual void`<br>`unsetCursor()` | Removes custom cursor settings, restoring the default |
| `QString`<br>`caption()` | Returns the current widget caption (window frame title bar on top-level widgets) |
| `const QPixmap *`<br>`icon()` | Returns a pointer to the pixmap that is currently set as this widget's icon |
| `QString`<br>`iconText()` | Returns the icon text (if it has been set, otherwise it returns NULL) |