Table 2.2 QWidget Class Methods 

 Public Members | Purpose 
 QWidget( QWidget *parent=0, const char *name=0, WFlags f=0 ) | Constructor. The default behavior, with a widget argument equal to zero, constructs a top-level widget 
 QWidget ( ) | Destructor 
 QWidget ID | Returns a platform-independent window ID 
 QStyle & style() | Returns the current Qt style of this widget 
 void setStyle( QStyle * ) | Sets a new style for this widget 
 bool isTopLevel( ) | Returns true if this is a top-level widget 
 bool isModal( ) | Returns true if this widget is modal (true implies top-level) 
 bool isPopup( ) | Returns true if this widget has the WType_Popup flag set 
 bool isDesktop( ) | Returns true if this widget refers to the desktop 
 bool isEnabled( ) | Returns true if this widget is enabled 
 bool isEnabledTo( QWidget * ) | Returns true if this widget would be enabled or disabled along with the argument widget 
 QRect frameGeometry( ) | Returns the geometry of this widget relative to its parent (including the window frame) 
 const QRect & geometry( ) | Returns the geometry of this widget relative to its parent 
 int x( ) | Returns the x coordinate of this widget, relative to its parent 
 int y( ) | Returns the y coordinate of this widget, relative to its parent 
 QPoint pos( ) | Returns the QPoint coordinate of this widget, relative to its parent 
 QSize frameSize( ) | Returns the size of the window system frame (only valid for top-level widgets) 
 QSize size( ) | Returns the size of the widget 
 int width( ) | Returns the width (in pixels or pels) of the widget 
 int height( ) | Returns the height (in pixels or pels) of the widget