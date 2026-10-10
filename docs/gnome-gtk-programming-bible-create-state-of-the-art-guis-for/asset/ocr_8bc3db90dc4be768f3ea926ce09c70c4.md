The value of *source* is the ID of the input device. It normally is GDK_CORE_POINTER, which is the constant value 0xFECD.

```
struct _GdkEventButton {
GdkEventType button;
GdkWindow *window;
gint8 send_event;
guint32 time;
gdouble x;
gdouble y;
gdouble pressure;
gdouble xtilt;
gdouble ytilt;
guint state;
guint button;
GdkInputSource source;
guint32 deviceid;
gdouble x_root, y_root;
};
```

# GdkEventClient

You can use this event for *interprocess* (or *inter-window*) *communication*. For this event, the value of *sent_event* will always be TRUE, because events of this type are always originated in a process. To hold the communications data, a block of up to 20 bytes is included inside the event struct.

The *message_type* is used to specify the actual type of the event. It is a character string transmitted in the form of a GdAtom.

The value of *data_format* is the number of bits in each member of the data array. If it is 8, the array named *b* contains 20 bytes of data. If it is 16, the *s* array contains ten 16-bit binary values. If it is 32, the *l* array contains five 32-bit values.

```
struct _GdkEventClient {
GdkEventType type;
GdkWindow *window;
gint8 send_event;
GdAtom message_type;
gushort data_format;
union {
char b[20];
short s[10];
long l[5];
} data;
};
```