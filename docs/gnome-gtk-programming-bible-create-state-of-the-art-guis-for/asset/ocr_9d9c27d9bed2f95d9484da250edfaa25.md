# GtkSocket

A **GtkSocket** widget can access widget windows from a remote process and display them as if they were local. The remote process creates a **GtkPlug** widget as the window to be made available to the **GtkSocket** of this process.

**Inheritance**

```
GtkSocket-->GtkContainer-->GtkWidget-->GKobject
```

**Functions**

```
guint gtk_socket_get_type()
gtk_widget *gtk_socket_new()
void gtk_socket_steal(GtkSocket *socket, guint32 id)
```

# GtkSpinButton

A **GtkSpinButton** widget displays a single numeric value that you can change by using the two arrow buttons to its right, or by editing the number directly.

**Inheritance**

```
GtkSpinButton-->GtkEntry-->GKEditable-->GKWidget-->GKobject
```

**Functions**

```
void gtk_spin_button_configure(GtkSpinButton *spin_button,
GtkAdjustment *adjustment, gfloat climb_rate, guint digits)
GtkAdjustment *gtk_spin_button_get_adjustment(
GtkSpinButton *spin_button)
GtkType gtk_spin_button_get_type(void)
gfloat gtk_spin_button_get_value_as_float(
GtkSpinButton *spin_button)
gint gtk_spin_button_get_value_as_int(
GtkSpinButton *spin_button)
GtkWidget *gtk_spin_button_new(GtkAdjustment *adjustment,
gfloat climb_rate, guint digits)
void gtk_spin_button_set_adjustment(
GtkSpinButton *spin_button, GtkAdjustment *adjustment)
void gtk_spin_button_set_digits(GtkSpinButton *spin_button,
guint digits)
void gtk_spin_button_set_numeric(GtkSpinButton *spin_button,
gboolean numeric)
void gtk_spin_button_set_shadow_type(
GtkSpinButton *spin_button, GtkShadowType shadow_type)
void gtk_spin_button_set_snap_to_ticks(
GtkSpinButton *spin_button, gboolean snap_to_ticks)
```