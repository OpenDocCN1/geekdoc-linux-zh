| State | Assigned Bit | |---|---| | The keyboard Shift key is down. | 0x00000001 | | The keyboard Caps Lock key is on. | 0x00000002 | | The keyboard Control key is down. | 0x00000004 | | The keyboard Alt or Meta key is down. | 0x00000008 | | The first (left) mouse button is down. | 0x00000100 | | The second (middle) mouse button is down. | 0x00000200 | | The third (right) mouse button is down. | 0x00000400 |

# # Source

When the event originates with a hardware device, there is a field named source of the type GdkInputSource that is used to indicate the type of device. This is an enum, which can be one of the following values:

+   GDK_SOURCE_MOUSE  
+   GDK_SOURCE_PEN  
+   GDK_SOURCE_ERASER  
+   GDK_SOURCE_CURSOR

# # GdkEvent

The GdkEvent is a union of several event structs. Each of these structs contain the data fields necessary for one or more events. This allows the system to propagate all events as being the same type, but it also means that your software must determine which type it really is. All of the structs have type as their first field to make it easy for a program to identify the type of event, and which struct layout contains the associated data.

```
union _GdkEvent {
    GdkEventAny
    GdkEventExpose      type;
    GdkEventNoExpose    expose;
    GdkEventVisibility  no_expose;
    GdkEventMotion      visibility;
    GdkEventButton      motion;
    GdkEventKey         button;
    GdkEventCrossing    key;
    GdkEventFocus       crosssing;
    GdkEventConfigure   focus_change;
    GdkEventProperty    configure;
} property;
```