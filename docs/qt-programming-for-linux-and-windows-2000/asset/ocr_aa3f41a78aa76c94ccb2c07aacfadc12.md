# Table 2.2 (Continued)

| Static Public Members | Purpose |
| --- | --- |
| void setTabOrder ( QWidget *first , QWidget *second ) | Sets the widget tab order. This is done in pairs, i.e., first to second, second to third, etc. |
| QWidget * mouseGrabber() | Returns a pointer to the widget that is currently grabbing the mouse, NULL otherwise |
| QWidget * keyboardGrabber() | Returns a pointer to the widget that is currently grabbing the keyboard, NULL otherwise |
| QWidget * find ( Wid ) | Returns a pointer to the widget whose window has the argument window ID |
| Protected Members | Purpose |
| virtual bool event ( QEvent * ) | The main event handler. An event is compared to all registered event types and dispatched to a specialized event handler |
| virtual void mousePressEvent ( QMouseEvent * ) | Called when a mouse button is pressed |
| virtual void mouseReleaseEvent( QMouseEvent * ) | Called when a mouse button is released |
| virtual void mouseDoubleClickEvent( QMouseEvent * ) | Called when a mouse button is double-clicked |
| virtual void mouseMoveEvent ( QMouseEvent * ) | Called whenever the mouse moves if tracking is enabled. Otherwise, it is called whenever the mouse moves while a mouse button is pressed |
| virtual void wheelEvent ( QWheelEvent * ) | Called when the mouse wheel is rotated |
| virtual void keyPressEvent ( QKeyEvent * ) | Called when a keyboard key is pressed |
| virtual void keyReleaseEvent( QKeyEvent * ) | Called when a keyboard key is released |
| virtual void focusInEvent( QFocusEvent * ) | Called when the widget receives keyboard focus |
| virtual void focusOutEvent( QFocusEvent * ) | Called when the widget loses keyboard focus |
| virtual void enterEvent ( QEvent * ) | Called when the mouse pointer enters the widget’s region |
| virtual void leaveEvent ( QEvent * ) | Called when the mouse pointer leaves the widget’s region |
| virtual void paintEvent( QPaintEvent * ) | If updates are enabled, the function is called when a portion of the widget needs to be repainted |