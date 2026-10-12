# Table 2.2 (Continued)

| Public Slots | Purpose |
|---|---|
| virtual void polish() | This slot is called after the widget has been created but before it is displayed. This is useful for performing additional initialization |
| void constPolish() | Ensures that a widget is fully initialized by calling polish(). Don't call this method from the constructor! |
| bool close() | Sends a QCloseEvent to the widget. If the event is accepted (default behavior), the widget will be hidden. Returns true if the close event was accepted |
| void raise() | Raises this widget to the top of the parent's stack if sibling widgets are obscuring it |
| void lower() | Lowers this widget in the parent's stack, possibly causing it to become obscured by sibling widgets |
| virtual void move( int x, int y ) | Moves the widget to the new coordinates, relative to the parent (and any window frame) |
| void move( const QPoint & ) | Moves the widget to the new coordinates, relative to the parent (and any window frame) |
| virtual void resize( int w, int h ) | Resizes the widget to the specified size (assuming the size is between the minimum and maximum sizes). If the widget is visible, it will receive a resize event immediately. Otherwise, it will receive a resize event before it becomes visible |
| void resize( const QSize & ) | Resizes the widget to the specified size (assuming the size is between the minimum and maximum sizes). If the widget is visible, it will receive a resize event immediately. Otherwise, it will receive a resize event before it becomes visible |
| virtual void setGeometry( int x, int y, int w, int h ) | Sets the widget's geometry to the argument values (assuming the size is between the minimum and maximum sizes) |
| virtual void setGeometry( const QRect & ) | Sets the widget's geometry to the argument values (assuming the size is between the minimum and maximum sizes) |