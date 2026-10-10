Table 9-2 (continued)

| Defined Event Name | Struct Used | Description |
| :--- | :--- | :--- |
| GDK_NO_EXPOSE | GdkEventNoExpose | In an image copy operation, the source window was available, so it did not require exposure. |
| GDK_PROPERTY_NOTIFY | GdkEventProperty | A window property has been changed or deleted. |
| GDK_PROXIMITY_IN | GdkEventProximity | A stylus has made physical contact with a graphics tablet. |
| GDK_PROXIMITY_OUT | GdkEventProximity | A stylus has broken physical contact with a graphics tablet. |
| GDK_SELECTION_CLEAR | GdkEventSelection | During cut-and-paste, the selected object is no longer owned by the receiver of this event. |
| GDK_SELECTION_NOTIFY | GdkEventSelection | During cut-and-paste, the new owner of a selection issues this event to indicate success or failure with ownership transfer. |
| GDK_SELECTION_REQUEST | GdkEventSelection | During cut-and-paste, another client has requested ownership of a selection. |
| GDK_UNMAP | GdkEventAny | The window is no longer being displayed (unmapped). |
| GDK_VISIBILITY_NOTIFY | GdkEventVisibility | There has been a change in the visibility of a window. |

Most widgets use their entire window as the subject for all events, but the *GnomeCanvas* carries this one step further. If the event has a location associated with it—that is, the x and y coordinates of a point in the window—the event is passed on to the item for processing. This makes it possible to use callback functions on individual items displayed in a *GnomeCanvas*.

In the header file, each struct is defined in two parts. One is to the struct itself and the other is a typedef for it. The names differ only in the initial character—the struct begins with an underscore character and the typedef does not. For example, the typedef for GdkEventAny is declared this way:

```
```c
typedef struct _GdkEventAny GdkEventAny;
```
```