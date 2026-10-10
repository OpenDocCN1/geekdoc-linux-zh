```
node = gtk_ctree_insert_node(GTK_CTREE(widget),
   parent,
   sibling,
   text,
   0,
   NULL,NULL,NULL,NULL,
   FALSE,TRUE);
return(node);
}
```

![](bbox=[0.11, 0.3, 0.34, 0.45])

Figure 21-12: A two-level GtkCTree showing selection and expansion

# GtkCurve

This widget displays a grid and traces a graph on it following a set of points. There are three kinds of traces available. You can add new points, and move existing points, interactively with the mouse.

# Inheritance

GtkCurve->GtkDrawingArea->GtkWidget->GtkObject

# Functions

```
```
GtkType gtk_curve_get_type(void)
void gtk_curve_get_vector(GtkCurve *c, int vecilen,
   gfloat vector [ ])
GtkWidget *gtk_curve_new(void)
void gtk_curve_reset(GtkCurve *c)
void gtk_curve_set_curve_type(GtkCurve *c,
   GtkCurveType new_type)
void gtk_curve_set_gamma(GtkCurve *c, gfloat gamma)
void gtk_curve_set_range(GtkCurve *curve, gfloat min_x,
   gfloat max_x, gfloat min_y, gfloat max_y)
void gtk_curve_set_vector(GtkCurve *c, int vecilen,
   gfloat vector [ ])
```
```

# Enum

```
```
typedef enum {
GTK_CURVE_TYPE_LINEAR,
GTK_CURVE_TYPE_SPLINE,
GTK_CURVE_TYPE_FREE
} GtkCurveType;
```
```