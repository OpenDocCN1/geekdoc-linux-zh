
`GDK_ENTER_NOTIFY` = 8,

`GDK_LEAVE_NOTIFY` = 9,

`GDK_FOCUS_CHANGE` = 10,

`GDK_CONFIGURE` = 11,

`GDK_MAP` = 12,

`GDK_UNMAP` = 13,

`GDK_PROPERTY_NOTIFY` = 14,

`GDK_SELECT_CLEAR` = 15,

`GDK_SELECT_REQUEST` = 16,

`GDK_SELECT_NOTIFY` = 17,

`GDK_PROXIMITY_IN` = 18,

`GDK_PROXIMITY_OUT` = 19,

`GDK_DRAG_BEGIN` = 20,

`GDK_DRAG_REQUEST` = 21,

`GDK_DROP_ENTER` = 22,

`GDK_DROP_LEAVE` = 23,

`GDK_DATA_AVAIL` = 24,

`GDK_CLIENT` = 25,

`GDK_VISIBILITY_NOTIFY` = 26,

`GDK_NO_EXPOSE` = 99 /* 已弃用，请使用过滤器 */

} `GdkEventType`;

事件类型与其他类型不同，允许将其转换为特定的事件数据。所以，事件类型定义如下：

```c
struct _GdkAny {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
};

struct _GdkExpose {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  GdkRectangle area;
  gint count; /* 如果不为零，表示后续有多少事件 */
};

struct _GdkNoExpose {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  /* XXX: 有人需要 X major_code 或 minor_code 字段吗? */
struct _GdkVisibility {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  GdkVisibilityState state;
};

struct _GdkMotion {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  guint32 time;
  double x;
  double y;
  double pressure;
  double tilt;
  double ytilt;
  guint state;
  gint16 is_hint;
  GdkInputSource source;
  guint32 deviceid;
  double x_root, y_root;
};

struct _GdkButton {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  guint32 time;
  double x;
  double y;
  double pressure;
  double tilt;
  double ytilt;
  guint state;
  guint button;
  GdkInputSource source;
  guint32 deviceid;
  double x_root, y_root;
};

struct _GdkEventKey {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
};
```

# B. GDK 事件类型

```c
guint32 time;
gint state;
gint keyval;
gint length;
gchar *string;
};
```

```c
struct _GdkEventCrossing
{
  GdkEventType type;
  GdkWindow *window;
  Gint8 send_event;
  GdkWindow *subwindow;
  GdkNotifyType detail;
};
```

```c
struct _GdkEventFocus
{
  GdkEventType type;
  GdkWindow *window;
  Gint8 send_event;
  gint16 in;
};
```

```c
struct _GdkEventConfigure
{
  GdkEventType type;
  GdkWindow *window;
  Gint8 send_event;
  gint16 x, y;
  gint16 width;
  gint16 height;
};
```

```c
struct _GdkEventProperty
{
  GdkEventType type;
  GdkWindow *window;
  Gint8 send_event;
  GdkAtom atom;
  guint32 time;
  gint state;
};
```

```c
struct _GdkEventSelection
{
  GdkEventType type;
  GdkWindow *window;
  Gint8 send_event;
  GdkAtom selection;
  GdkAtom target;
  GdkAtom property;
  guint32 requestor;
  guint32 time;
};
```
/* 此事件类型极少使用。它仅重要 */

```c
struct _GdkEventDropEnter {
  GdkEventType type;
  GdkWindow *window;
};
```

# B. GDK 事件类型

```c
guint8 send_event;
guint32 requestor;
union {
  struct {
    guint protocol_version:4;
    guint sendreply:1;
    guint extended_typelist:1;
    guint reserved:26;
    long flags;
    glong allflags;
  } u;
};
```

```c
struct _GdkEventDropLeave {
  GdkEventType type;
  GdkWindow *window;
  guint8 send_event;
  guint32 requestor;
  union {
    struct {
      guint protocol_version:4;
      guint reserved:28;
      long flags;
      glong allflags;
    } u;
  };
};
```

```c
struct _GdkEventDropDataAvailable {
  GdkEventType type;
  GdkWindow *window;
  guint8 send_event;
  guint32 requestor;
  union {
    struct {
      guint protocol_version:4;
      guint isdrop:1;
      guint reserved:25;
      long flags;
      glong allflags;
    } u;
    gchar *data_type; /* MIME 类型 */
    gulong data_numbytes;
  gpointer data;
  guint32 timestamp;
  GdkPoint coords;
};
```

```c
struct _GdkClient {
  GdkEventType type;
  GdkWindow *window;
  guint8 send_event;
  GdkAtom message_type;
  gushort data_format;
  union {
```

# C. 代码示例
