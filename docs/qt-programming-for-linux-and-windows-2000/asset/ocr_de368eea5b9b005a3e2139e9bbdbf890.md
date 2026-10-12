# Table 2.2 (Continued)

| Protected Members | Purpose |
| --- | --- |
| virtual void create( WId = 0, bool initializeWindow = TRUE, bool destroyOldWindow = TRUE ) | Creates a new widget window if the window ID argument is zero, otherwise the widget is moved to the window with that ID. The initializeWindow argument specifies whether the new window's geometry will be initialized or not. If the destroyOldWindow argument is true, the previous window will be destroyed |
| virtual void destroy( bool destroyWindow = TRUE, bool destroySubWindows = TRUE ) | Destroys the widget window if destroyWindow is true. If destroySubWindows is true, destroy( ) is called recursively for child widgets |
| WFlags getWFlags( ) | Retrieves the current widget flags |
| virtual void setWFlags( WFlags ) | Sets the specified widget flag |
| void clearWFlags( WFlags ) | Resets (clears) the specified widget flag |
| virtual bool focusNextPrevChild( bool next ) | Finds a new widget to accept keyboard focus in the current tab order. Returns true if successful, false otherwise |
| QFocusData * focusData( ) | Returns a pointer to the focus data for the top-level widget ancestor of this widget |
| virtual void setKeyCompression( bool ) | Enables/disables key event compression. When enabled, more than one key event can be processed in a single event, useful for multi-character unicode input. The default is disabled |
| virtual void setMicroFocusHint( int x, int y, int w, int h, bool text=TRUE ) | Sets the focus position and size for platform-dependent input methods |


# Parent/Child Relationship

QWidget maintains a list of its child widgets (accessible via the QWidget::children( ) method). A child of a given widget is a new widget whose parent widget (passed as the first argument to the constructor) is the given widget. The default QWidget destructor will delete all of its children before it deletes itself. All you need to do to delete a chain of widgets is delete the parent.